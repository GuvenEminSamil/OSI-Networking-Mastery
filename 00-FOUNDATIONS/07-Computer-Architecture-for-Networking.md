# 00-07 Ağ için Bilgisayar Mimarisi (Computer Architecture for Networking)

> Önkoşullar: 00-05, 00-06 | Tahmini süre: ~2 saat | CCNA: dolaylı (v1.1 1.4 arayüz sayaçları, 1.10 istemcide doğrulama ve 1.5'in altyapısı)

## Öğrenme Hedefleri

- Bir çerçeve alınırken NIC, DMA, RAM, kesme (interrupt) ve CPU'nun rollerini sırasıyla anlatmak.
- Halka tamponun (ring buffer) nasıl çalıştığını ve dolduğunda ne olduğunu açıklamak; kesme ile yoklamayı (polling) karşılaştırmak.
- Sürücünün, işletim sistemi ağ yığınının ve soketin görevlerini; çekirdek alanı ile kullanıcı alanı ayrımını açıklamak.
- Donanım yük boşaltmanın (offload) Wireshark yakalamalarını nasıl etkilediğini açıklamak.
- Tampon kaynaklı kayıpları host'ta ve Cisco `show interfaces` çıktısında kablo hatalarından ayırt etmek.

## 1. Sezgisel Giriş

Bir kargo deposu düşün. Kamyonlar (kablo) sürekli paket getirir. Rampadaki görevli (NIC) paketleri kamyondan indirir ve depo müdürünü (CPU) her paket için çağırmadan, numaralı raflara (RAM'deki tamponlar) yerleştirir. Raflar dolmaya başlayınca bir zil çalar (kesme). Müdür gelir, raflardaki paketleri toplu hâlde alır, etiketlerine bakar ve her birini doğru alıcının posta kutusuna (soket) bırakır. Raflar müdür gelmeden dolarsa, yeni gelen paketler için yer kalmaz ve kamyondan inen paketler kapıda bırakılır.

Gerçek bir bilgisayar bunu saniyede yüz binlerce, hatta milyonlarca çerçeve için yapar. Bu dosya, kablodaki bitlerin uygulamana nasıl ulaştığını ve yolda nerede kaybolabileceğini anlatır.

## 2. Neden Var?

İletişim, sonunda bir bilgisayarın içindeki bir uygulamada biter. Kablo ile uygulama arasında donanım ve işletim sistemi vardır. Bu katmanı bilmeden şu durumlar açıklanamaz:

- Kablo hatası yokken yoğun trafikte paketlerin düşmesi.
- Wireshark'ın kendi gönderdiğin paketlerde "checksum incorrect" uyarısı vermesi (H02).
- Aynı bilgisayardaki tarayıcının, oyunun ve güncelleme servisinin gelen paketleri karıştırmaması (soketler, 04-01).
- Bir router'ın veri düzlemini neden özel donanımda çalıştırdığı (03-07).

## 3. Mekanizma

### 3.1 Temel bileşenler

| Bileşen | Görevi |
|---|---|
| **CPU** | Komutları çalıştırır. Yazmaçları ve küçük, hızlı önbellekleri (SRAM, 00-05) vardır |
| **RAM** | Ana bellek (DRAM). Programlar, işletim sistemi ve ağ tamponları buradadır |
| **Veri yolu (bus)** | Bileşenler arasındaki bağlantı. Bugün NIC'ler genellikle **PCIe** üzerinden bağlanır ya da yongaya gömülüdür |
| **NIC (network interface card)** | Kablo ile bilgisayar arasındaki arayüz: L1 (PHY) ve L2'nin MAC işlevleri |

Bu bileşenlerin hızları çok farklıdır. **[BASİTLEŞTİRME]** Yalnızca büyüklük mertebeleri verilmiştir:

| İşlem | Yaklaşık süre |
|---|---|
| CPU'da bir komut, önbellekten bir okuma | ~1 ns |
| RAM'den bir okuma | ~100 ns |
| SSD'den bir okuma | ~10–100 µs |
| İnternet üzerinden bir gidiş-dönüş (RTT) | ~1–100 ms |

### 3.2 NIC ne yapar?

NIC; kablodaki sinyali bitlere çevirir (PHY, 01-01), çerçevenin sınırlarını bulur, FCS'i kontrol eder ve bozuk çerçeveyi atar (02-04). Ayrıca **adres filtrelemesi** yapar: Varsayılan olarak yalnızca hedefi kendi MAC adresi, yayın (broadcast) ya da abone olduğu çoklu yayın (multicast) adresleri olan çerçeveleri kabul eder; diğerlerini CPU'yu hiç rahatsız etmeden atar. Wireshark'ın kullandığı **promiscuous mod** bu filtreyi kapatır (02-02).

NIC'in kendi üzerinde yalnızca küçük bir FIFO belleği vardır. Gelen çerçeveleri hızla RAM'e aktarmak zorundadır.

### 3.3 DMA ve halka tampon

En basit yöntemde CPU, NIC'teki her baytı tek tek okuyup RAM'e kopyalar. Bu, CPU'yu tamamen meşgul eder. Çözüm **DMA (direct memory access)**: NIC, CPU'ya sormadan çerçeveyi doğrudan RAM'e yazar.

Peki RAM'in neresine? Sürücü, açılışta RAM'de bir **halka tampon (ring buffer)** hazırlar. Bu, her biri RAM'deki boş bir tampona işaret eden **tanımlayıcılardan (descriptor)** oluşan dairesel bir dizidir:

```
                 sürücü buradan okur (tüketici)
                        ↓
   ┌──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┐
   │  D0  │  D1  │  D2  │  D3  │  D4  │  D5  │  D6  │  D7  │
   │ boş  │ boş  │ dolu │ dolu │ dolu │ boş  │ boş  │ boş  │
   └──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┘
                                       ↑
                      NIC buraya yazar (üretici); D7'den sonra D0'a döner
```

*Ne görüyoruz:* NIC, sıradaki boş tanımlayıcının gösterdiği tampona bir çerçeve yazar ve onu "dolu" işaretler. Sürücü dolu tanımlayıcıları sırayla işler, tamponları ağ yığınına verir ve yerlerine yeni boş tamponlar koyar. İki taraf aynı halkada birbirini kovalar.

Sürücü yetişemezse NIC halkanın sonuna gelir ve yazacak boş tanımlayıcı bulamaz. **Yeni gelen çerçeveler düşürülür.** Kabloda hiçbir hata yoktur; kayıp bilgisayarın içinde olur. Bunu gösteren sayaçlar Bölüm 7'de.

### 3.4 Kesme, yoklama ve NAPI

NIC, yeni çerçeveler geldiğini CPU'ya bir **kesme (interrupt)** ile bildirir: CPU o anki işini bırakır, sürücünün kesme işleyicisini çalıştırır ve sonra işine döner.

Az trafikte bu iyi çalışır. Ama her çerçeve için bir kesme üretmek, yüksek hızlarda CPU'nun bütün zamanını kesmelere harcamasına yol açar. İki çözüm birlikte kullanılır:

- **Kesme birleştirme (interrupt coalescing / moderation):** NIC, belirli sayıda çerçeve birikene ya da kısa bir süre (mikrosaniyeler) geçene kadar bekler, sonra tek bir kesme üretir.
- **NAPI (Linux):** İlk kesme gelince sürücü kesmeleri kapatır ve halkayı **yoklama (polling)** ile, her turda belirli bir "bütçe" kadar çerçeve işleyerek boşaltır. Halka boşalınca kesmeleri yeniden açar [LNX-NAPI]. Böylece az trafikte kesmenin hızlı tepkisi, yoğun trafikte yoklamanın verimliliği elde edilir.

Bedeli küçük bir gecikmedir: Çerçeve, birleştirme süresi kadar halkada bekleyebilir. Bu, İnternet gecikmesinin (milisaniyeler) yanında ihmal edilebilir; ama veri merkezlerinde ve düşük gecikme isteyen uygulamalarda ayarlanır.

> **[DERİN]** Modern NIC'lerin birden fazla alma ve gönderme kuyruğu vardır. NIC, her çerçevenin başlığından bir özet (hash) hesaplayıp onu bir kuyruğa ve dolayısıyla bir CPU çekirdeğine atar (RSS, receive side scaling). Aynı bağlantının çerçeveleri hep aynı kuyruğa gider; böylece sıraları bozulmaz.

### 3.5 Sürücü, ağ yığını ve soket

- **Sürücü (driver):** Belirli bir NIC modelinin yazmaçlarını ve halkalarını bilen yazılım. İşletim sistemine standart bir arayüz sunar; böylece yığın, NIC'in markasını bilmek zorunda kalmaz.
- **Ağ yığını (network stack):** İşletim sisteminin çekirdeğinde Ethernet, ARP, IP, TCP ve UDP'yi gerçekleştiren kod. Başlıkları okur, kontrol eder ve çıkarır (decapsulation, 00-09).
- **Çekirdek alanı ve kullanıcı alanı (kernel space / user space):** Uygulamalar NIC'e ya da yığının içine doğrudan erişemez. **Sistem çağrılarıyla (system call)** çekirdekten hizmet isterler. Bu ayrım güvenlik ve kararlılık sağlar; bedeli her geçişte küçük bir maliyettir.
- **Soket (socket):** Bir uygulamanın ağ iletişimi için açtığı uç noktadır. İşletim sistemi açısından bir dosyaya benzer bir nesnedir (Linux'ta bir dosya tanımlayıcısı, file descriptor). Gelen bir TCP ya da UDP segmenti, başlığındaki **port numaraları** ve adreslerle doğru sokete, dolayısıyla doğru uygulamaya teslim edilir. Ayrıntılar 04-01'de, soket API'si 04-07'de.

Bir çerçevenin kablodan uygulamaya yolculuğu:

```mermaid
flowchart LR
    W["Kablo"] --> PHY["NIC: PHY<br/>sinyal → bit"]
    PHY --> MAC["NIC: MAC<br/>FCS kontrolü, adres filtresi"]
    MAC -->|DMA| RING["RAM: RX halka tamponu"]
    RING -->|kesme + NAPI| DRV["Sürücü"]
    DRV --> STK["Çekirdek ağ yığını<br/>Ethernet → IP → TCP/UDP"]
    STK --> SOCK["Soketin alma tamponu"]
    SOCK -->|"recv() sistem çağrısı"| APP["Uygulama<br/>(kullanıcı alanı)"]
```

*Ne görüyoruz:* Yolun ilk iki adımı NIC'in donanımında, son adımı kullanıcı alanında olur; arada her şey çekirdektedir. Gönderme yönü bunun tersidir: `send()` → soket gönderme tamponu → yığın başlıkları ekler → sürücü TX halkasına koyar → NIC, DMA ile okuyup kabloya gönderir.

### 3.6 Donanım yük boşaltma (offload)

CPU'nun yükünü azaltmak için bazı işler NIC'e bırakılır:

- **Checksum offload:** IP, TCP ve UDP checksum'larını NIC hesaplar.
- **Segmentasyon offload (TSO/GSO):** Yığın NIC'e büyük bir veri bloğu verir; NIC onu MTU'ya uygun segmentlere böler (04-06).
- **Alma birleştirme (GRO/LRO):** Aynı bağlantının ardışık segmentleri yığına tek bir büyük paket olarak verilir.

Wireshark'a etkisi önemlidir. Wireshark paketleri **yığın ile sürücü arasında** yakalar. Gönderen bilgisayarda yakalama yapıyorsan:

- Giden paketlerin checksum'ı henüz hesaplanmamıştır; Wireshark "incorrect checksum" der. **Bu bir hata değildir**; NIC, checksum'ı kabloya çıkmadan hesaplar.
- TSO açıksa MTU'dan büyük "paketler" görürsün; kabloda bunlar zaten parçalara bölünmüş olarak gider.

## 4. Teknik Ayrıntı: Saniyede kaç çerçeve?

Ethernet'te her çerçeve kabloda ayrıca 8 bayt preamble ve SFD ile 12 baytlık çerçeveler arası boşluk (IFG) kaplar (02-03). Bu 20 baytı da sayarak:

| Bağlantı | Çerçeve boyutu | Kablodaki bit | Saniyede çerçeve | Çerçeve başına süre |
|---|---|---|---|---|
| 1 Gbps | 1518 bayt (en büyük) | (1518 + 20) × 8 = 12.304 | ≈ 81.274 | ≈ 12,3 µs |
| 1 Gbps | 64 bayt (en küçük) | (64 + 20) × 8 = 672 | ≈ 1.488.095 | 672 ns |
| 10 Gbps | 1518 bayt | 12.304 | ≈ 812.744 | ≈ 1,23 µs |
| 10 Gbps | 64 bayt | 672 | ≈ 14.880.952 | 67,2 ns |

Son satıra bak: 10 Gbps'ta en küçük çerçeveler her 67 ns'de bir gelir. Bu, tek bir RAM okumasından (Bölüm 3.1) bile kısadır. 3 GHz'lik bir çekirdeğin her çerçeve için yaklaşık 3 × 10⁹ / 14,88 × 10⁶ ≈ **200 saat çevrimi** vardır. Genel amaçlı bir CPU'nun her paketi tek tek işleyerek bu hıza yetişmesi çok zordur. Bu yüzden:

- **Host'lar** DMA, halka tamponlar, kesme birleştirme, NAPI, çok kuyruk ve offload kullanır.
- **Router ve switch'ler** veri düzlemini ASIC'lerde çalıştırır (00-05, Bölüm 4.1). CPU'ya yalnızca cihazın kendisine gelen trafik (SSH, OSPF, kendi adresi için ARP) ve istisnalar (ör. TTL'si biten paketler) gider. 03-07'de bu ayrımı "hızlı yol" ve "yavaş yol" olarak göreceksin.

## 5. Gerçek Dünya Örnekleri

- **Yoğun bir sunucu:** Bir video sunucusu kampanya saatinde paket kaybediyor; switch portunda hiç hata yok. `ethtool -S` çıktısında alma tarafındaki "missed" ya da "no buffer" sayaçları artıyor. Halka tamponu büyütmek ya da yükü daha fazla kuyruğa ve çekirdeğe dağıtmak sorunu çözüyor.
- **Wireshark'ta paniğe gerek yok:** Dizüstü bilgisayarında yakalama yapan bir öğrenci, giden her TCP paketinde kırmızı "checksum incorrect" satırları görüyor. Neden checksum offload'dur; karşı tarafta yakalama yapılsaydı checksum'lar doğru görünürdü.
- **Oyun bilgisayarı:** Bazı oyuncular gecikmeyi azaltmak için NIC'in "Interrupt Moderation" ayarını kapatır. Kazanç mikrosaniyelerle ölçülür; İnternet üzerindeki onlarca milisaniyelik gecikmenin yanında genellikle hissedilmez.

## 6. Diğer Konularla Bağlantı

| Bu dosyadaki fikir | Nerede derinleşiyor |
|---|---|
| NIC'in adres filtrelemesi, promiscuous mod, offload'lar | 02-02 |
| FCS kontrolü | 02-04 |
| Preamble, SFD ve IFG | 02-03 |
| Router'da hızlı ve yavaş yol | 03-07 |
| Portlar, soketler, çoklama | 04-01 |
| Soket API'si ve çekirdek tamponları | 04-07 |
| TSO ve segmentasyon | 04-06 |
| Kontrol ve veri düzlemi | 03-01, 15-04 |
| Checksum offload uyarısı | H02 |

## 7. Cisco ve Pratik

### 7.1 Cisco: tampon kaynaklı sayaçlar

**[CISCO-ÖZEL]** `show interfaces` çıktısındaki giriş sayaçlarının bir kısmı kablo hatalarını, bir kısmı ise cihazın kapasitesini gösterir:

```
Router# show interfaces GigabitEthernet0/0
...
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  ...
     1567 packets input, 210345 bytes, 0 no buffer
     Received 12 broadcasts (0 IP multicasts)
     0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
```

| Sayaç | Anlamı | Hangi dosya? |
|---|---|---|
| CRC, frame, runts, giants | Çerçeve bozuk ya da boyutu hatalı geldi: kablo, gürültü, duplex | 01-10 |
| **overrun** | Alıcı donanım, gelen veriyi bir donanım tamponuna aktaramadı | Bu dosya |
| **ignored** | Arayüz donanımının iç tamponları tükendi | Bu dosya |
| **no buffer** | Ana sistemde paketi koyacak tampon kalmadı | Bu dosya |
| Input queue drops | CPU'ya gidecek paketlerin kuyruğu doldu | 03-07 |

CRC sayacı sıfırken overrun, ignored ya da no buffer artıyorsa sorun kablo değil, **kapasitedir**: Trafik, cihazın işleyebileceğinden fazladır [CISCO-IFCOUNT]. `show interfaces` PT'de desteklenir (✅); sayaçları LAB-007'de okuyacaksın. **[PT-SINIRI]** PT tampon taşmasını simüle etmez; bu sayaçlar PT'de genellikle 0 kalır.

### 7.2 Host: Fedora ve Windows

Arayüzünün adını önce `ip link` (Fedora) ya da `Get-NetAdapter` (Windows) ile bul. Aşağıda `enp3s0` ve `"Ethernet"` örnek addır.

```
# Fedora
$ ip -s link show enp3s0                 # paket, hata ve düşürme (dropped) sayaçları
$ ethtool -i enp3s0                      # sürücü adı ve sürümü
$ ethtool -g enp3s0                      # RX/TX halka tampon boyutları
$ ethtool -k enp3s0 | grep -i checksum   # checksum offload açık mı?
$ ethtool -S enp3s0                      # NIC'e özgü ayrıntılı sayaçlar
$ ss -tunap                              # açık soketler ve sahip süreçler (diğer kullanıcılarınki için sudo)
```

```
# Windows PowerShell
PS> Get-NetAdapter                                     # arayüzler, hız, durum
PS> Get-NetAdapterStatistics -Name "Ethernet"          # alınan, gönderilen ve atılan paketler
PS> Get-NetAdapterAdvancedProperty -Name "Ethernet"    # sürücü ayarları: offload, receive buffers, interrupt moderation
PS> netstat -ano                                       # soketler ve süreç kimlikleri (PID)
```

`ethtool -S` ve `Get-NetAdapterAdvancedProperty` çıktılarındaki adlar sürücüye göre değişir. Kablosuz arayüzlerde bazı `ethtool` alanları boş gelebilir.

## 8. Yaygın Yanılgılar

| Yanılgı | Doğrusu |
|---|---|
| "CPU, kablodan gelen her baytı kendisi okur." | NIC, çerçeveleri DMA ile doğrudan RAM'deki halka tampona yazar; CPU yalnızca bitmiş çerçeveleri işler. |
| "Paket kaybı her zaman kablodan ya da ağdan kaynaklanır." | Kayıp, alıcı bilgisayarın ya da cihazın içinde de olabilir: halka tampon dolar, CPU yetişemez. CRC sıfırken artan overrun, ignored ve no buffer sayaçları bunu gösterir. |
| "Wireshark'taki 'checksum incorrect' uyarısı paketlerin bozuk gittiğini gösterir." | Gönderen bilgisayarda yakalama yapılıyorsa checksum'ı henüz NIC hesaplamamıştır (offload). Kablodaki paket doğrudur. |
| "Switch portu ile TCP portu aynı şeydir." | Switch portu fiziksel bir arayüzdür (L1/L2). TCP/UDP portu, bir host içindeki uygulamayı tanımlayan 16 bitlik bir sayıdır (L4). |
| "Ne kadar çok kesme, o kadar hızlı ağ." | Her çerçeve için kesme, yüksek hızlarda CPU'yu boğar. Kesme birleştirme ve NAPI daha az kesmeyle daha fazla çerçeve işler. |

## 9. Arıza Giderme Yaklaşımı

| Belirti | Olası neden | İlk kontrol |
|---|---|---|
| Yoğun trafikte kayıp var, CRC sıfır | Halka tampon ya da cihaz kapasitesi yetmiyor | Host: `ethtool -S`, `ip -s link`. Cisco: overrun, ignored, no buffer |
| Sürücü güncellemesinden sonra bağlantı düşük hızda ya da kopuk | Sürücü hatası ya da değişen ayarlar | `ethtool -i`; Windows'ta Aygıt Yöneticisi ve `Get-NetAdapterAdvancedProperty` |
| Wireshark'ta giden paketlerde checksum hatası ya da MTU'dan büyük paketler | Offload (normal davranış) | Karşı tarafta ya da arada yakala; gerekirse yakalama süresince offload'u kapat |
| Bir sunucu programı "address already in use" hatası veriyor | Aynı portu başka bir süreç dinliyor | `ss -tlnp` ya da `netstat -ano` ile portu ve PID'i bul |

## 10. CCNA Bağlantısı

CCNA DMA ya da NAPI sormaz. Ama `show interfaces` çıktısındaki sayaçları yorumlamak v1.1 1.4'ün (arayüz ve kablo sorunları) parçasıdır ve "kablo mu, kapasite mi?" ayrımı bu dosyadan gelir. İstemci işletim sistemlerinde ağ ayarlarını doğrulamak (v1.1 1.10) Bölüm 7.2'deki araçlarla başlar (ayrıntılar 11-03). Soket kavramı, v1.1 1.5'teki TCP ve UDP karşılaştırmasının altyapısıdır.

## 11. Kendini Kontrol Et

1. DMA olmasaydı gelen bir çerçeveyi RAM'e kim kopyalardı? Bunun sakıncası ne olurdu?
   <details><summary>Cevap</summary>
   CPU, NIC'teki baytları tek tek okuyup RAM'e yazardı. Yüksek hızlarda CPU'nun zamanının neredeyse tamamı kopyalamaya giderdi. DMA ile NIC çerçeveyi kendisi yazar; CPU yalnızca bitmiş çerçeveleri işler.
   </details>

2. RX halka tamponu dolduğunda ne olur? Bunu Linux'ta ve bir Cisco router'da hangi sayaçlarda görürsün?
   <details><summary>Cevap</summary>
   NIC yazacak boş tanımlayıcı bulamaz ve yeni çerçeveleri düşürür. Linux'ta <code>ip -s link</code> çıktısındaki dropped ve <code>ethtool -S</code>'teki missed/no buffer türü sayaçlar; Cisco'da overrun, ignored ve no buffer artar. CRC sayacı ise artmaz, çünkü çerçeveler bozuk değildir.
   </details>

3. 10 Gbps'lık bir bağlantıda en küçük çerçevelerle saniyede yaklaşık kaç çerçeve gelir? Router'ların veri düzlemi için neden ASIC kullandığını bu sayıyla açıkla.
   <details><summary>Cevap</summary>
   (64 + 20) × 8 = 672 bit; 10¹⁰ / 672 ≈ <b>14,88 milyon</b> çerçeve/s, yani her ~67 ns'de bir. Bu, tek bir RAM erişiminden kısadır ve 3 GHz'lik bir çekirdeğe çerçeve başına ~200 çevrim bırakır. ASIC, iletim kararını paralel kapılarla ve TCAM aramasıyla her çerçeve için sabit ve çok kısa sürede verir.
   </details>

4. Kendi bilgisayarında yaptığın yakalamada giden TCP paketlerinin checksum'ı "incorrect" görünüyor. Bu bir sorun mu?
   <details><summary>Cevap</summary>
   Büyük olasılıkla hayır. Checksum offload açıkken yığın checksum alanını boş bırakır ve NIC, paketi kabloya göndermeden hemen önce hesaplar. Wireshark paketi bundan önce yakalar. Karşı tarafta yapılan bir yakalamada checksum doğru görünür.
   </details>

5. "Switch'in 24 portu var" ile "web sunucusu 443 numaralı portu dinliyor" cümlelerindeki "port" sözcükleri arasındaki fark nedir?
   <details><summary>Cevap</summary>
   İlki fiziksel bir arayüzdür (kablonun takıldığı yer, L1/L2). İkincisi, host içindeki bir uygulamayı (soketi) tanımlayan 16 bitlik mantıksal bir sayıdır (L4).
   </details>

## 12. Uygulama

Fedora'da ve Windows'ta Bölüm 7.2'deki komutları çalıştır ve şunları bul:

1. NIC'inin sürücü adı ve RX halka tamponunun boyutu (Fedora).
2. Checksum offload'un açık olup olmadığı (iki sistemde).
3. Tarayıcında bir site açıkken `ss -tunap` ya da `netstat -ano` çıktısında 443 numaralı uzak porta giden bağlantıları ve bunların hangi sürece ait olduğunu.

Not etmen gereken bir şey yok; amaç bu çıktılara bir kez bakmış olmak. H02'de Wireshark'la bu dosyaya geri döneceksin.

## 13. Ustalık Kontrol Listesi

- [ ] Bir çerçevenin kablodan uygulamaya yolculuğunu (PHY, MAC, DMA, halka, kesme/NAPI, sürücü, yığın, soket) kaynağa bakmadan çizebiliyorum.
- [ ] Halka tamponun nasıl çalıştığını ve dolduğunda kayıpların hangi sayaçlarda görüneceğini açıklayabiliyorum.
- [ ] Kesme birleştirme ve NAPI'nin neden gerektiğini saniyedeki çerçeve sayısıyla gerekçelendirebiliyorum.
- [ ] Checksum offload ve TSO'nun Wireshark yakalamalarını nasıl etkilediğini söyleyebiliyorum.
- [ ] `show interfaces` çıktısında kablo kaynaklı sayaçları kapasite kaynaklı sayaçlardan ayırabiliyorum.

## Kaynaklar

- [LNX-NAPI] Linux kernel documentation, *NAPI*: kesme ile başlayıp yoklamayla süren işleme, bütçe, kesme maskeleme.
- [TOOL-LINUX] `ip`, `ss` ve `ethtool` man sayfaları.
- [TOOL-WINNET] Microsoft, NetAdapter PowerShell modülü belgeleri (`Get-NetAdapter`, `Get-NetAdapterStatistics`, `Get-NetAdapterAdvancedProperty`).
- [CISCO-IFCOUNT] Cisco belgeleri: `show interfaces` çıktısındaki overrun, ignored ve no buffer sayaçlarının anlamı.
- [IEEE-8023] Preamble ve SFD (8 bayt), çerçeveler arası boşluk (96 bit süresi = 12 bayt).
- [TXT-HARRIS] Digital Design and Computer Architecture: bellek hiyerarşisi ve G/Ç (ek okuma).
- [TXT-KUROSE] Computer Networking: A Top-Down Approach: host içindeki ağ yığını (ek okuma).

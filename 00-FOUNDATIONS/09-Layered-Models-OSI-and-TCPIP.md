# 00-09 Katmanlı Modeller: OSI ve TCP/IP (Layered Models: OSI and TCP/IP)

> Önkoşullar: 00-08 | Tahmini süre: ~2 saat | CCNA: dolaylı (sınavın "L2", "L3" dili, PDU adları ve kapsülleme; 11-01'in altyapısı)

## Öğrenme Hedefleri

- Katmanlı tasarımın gerekçelerini ve bedelini açıklamak.
- OSI'nin yedi katmanını görevleri, örnek protokolleri ve PDU adlarıyla sıralamak; TCP/IP modelinin (RFC 1122) dört katmanıyla eşlemek.
- Kapsülleme (encapsulation) ve açmayı (decapsulation) genel hatlarıyla anlatmak; alıcının yükü hangi alana bakarak bir üst katmana verdiğini söylemek.
- ARP, ICMP, OSPF, DHCP ve TLS gibi protokollerin katmanlara neden tam oturmadığını açıklamak.
- Bir referans modeli ile gerçek bir uygulamanın (implementation) farkını açıklamak.

## 1. Sezgisel Giriş

Kazan'dan İstanbul'a bir mektup gönderdiğini düşün. Sen mektubu yazarsın; kargo şirketi gönderiyi takip eder ve kaybolursa yeniden gönderir; dağıtım merkezleri adrese bakıp şehirden şehre yönlendirir; her kamyon gönderiyi yalnızca bir sonraki depoya götürür. Her aşama yalnızca kendi işini bilir: Sen kamyonu bilmezsin, şoför mektubu okumaz. Her aşama altındakinin hizmetini kullanır ve üstündekine hizmet verir. **Katmanlı model (layered model)** ağ iletişimini böyle böler.

## 2. Neden Var?

1970'lerde her bilgisayar üreticisinin kendi kapalı ağ mimarisi vardı (ör. IBM'in SNA'sı, DEC'in DECnet'i). Farklı üreticilerin cihazları birbiriyle konuşamıyordu. İki şeye ihtiyaç vardı: herkesin uyacağı ortak protokoller ve bu protokolleri tartışmak için ortak bir dil.

Katmanlama bu büyük problemi bağımsız parçalara böler. Katmanlar olmasaydı bakırdan fibere geçmek web tarayıcısını yeniden yazmayı gerektirebilirdi.

## 3. Mekanizma

### 3.1 Katmanlamanın ilkeleri

- **Hizmet ve arayüz:** Her katman bir üstüne belirli bir hizmet sunar ve bir altının hizmetini kullanır. İki katman arasındaki arayüz tanımlıdır; bir katmanın içi değişse de arayüz aynı kaldıkça komşuları etkilenmez.
- **Eşdüzey iletişim (peer communication):** Bir katman, karşı taraftaki **aynı katmanla** kendi protokolüyle "konuşur". Göndericinin TCP'si alıcının TCP'si için bir başlık yazar; aradaki katmanlar bu başlığı okumaz. Bu konuşma mantıksaldır; fiziksel olarak veri aşağı iner, kablodan geçer ve karşı tarafta yukarı çıkar.

Katmanlamanın faydaları:

| Fayda | Örnek |
|---|---|
| **Soyutlama ve modülerlik** | Wi-Fi'den Ethernet'e geçmek tarayıcıyı ve TCP'yi değiştirmez |
| **Birlikte çalışabilirlik** | Bir üreticinin NIC'i, başka bir üreticinin işletim sistemiyle çalışır |
| **Bağımsız gelişim** | Ethernet 10 Mbps'tan yüzlerce Gbps'a çıkarken IP aynı kaldı |
| **Arıza giderme** | "Link ışığı yanıyor mu? (L1) IP adresi var mı? (L3) Ad çözülüyor mu? (L7)" (11-01) |
| **Ortak dil** | "Bu bir L2 sorunu", "L4 yük dengeleyici", "L3 switch" |

Bedelleri de vardır:

- **Başlık yükü (overhead):** Her katman kendi başlığını ekler (Bölüm 4.1).
- **İşlev tekrarı:** Örneğin hem Ethernet (FCS) hem TCP (checksum) hata kontrolü yapar.
- **Gizlenen bilgi:** Performans uğruna sınırlar zaman zaman aşılır: TCP segment boyutunu MTU'ya göre seçer (03-12), NIC TCP checksum'ını hesaplar (00-07). RFC 3439, aşırı katmanlamanın işlev tekrarına ve karmaşıklığa yol açabileceğini tartışır [RFC 3439 §3].

### 3.2 OSI modeli

**[OSI-TEORİ]** ISO'nun açık sistemlerin birbirine bağlanması (Open Systems Interconnection) için hazırladığı model 1984'te ISO 7498 olarak yayımlandı; bugün geçerli metni **ISO/IEC 7498-1:1994**'tür ve ITU-T **X.200 (07/1994)** ile aynıdır [ISO-7498, ITU-X200]. OSI'nin protokol ailesi piyasada büyük ölçüde TCP/IP'ye yenildi (bugün yaşayan nadir örneklerden biri IS-IS'tir, 03-13); model ise ağ dünyasının ortak dili olarak kaldı.

| # | Katman | Görevi | Bugünkü örnekler | PDU |
|---|---|---|---|---|
| 7 | **Uygulama (Application)** | Ağ hizmetlerini uygulamalara sunar | HTTP, DNS, DHCP, SMTP, SSH | Veri (data) |
| 6 | **Sunum (Presentation)** | Verinin gösterimi: kodlama, sıkıştırma, şifreleme | İşlevleri bugün UTF-8, JPEG, TLS gibi biçim ve protokollerde (06-*) | Veri |
| 5 | **Oturum (Session)** | Diyaloğu kurar, sürdürür, senkronize eder | İşlevleri bugün TCP, TLS ve uygulamaların içinde (05-*) | Veri |
| 4 | **Taşıma (Transport)** | Uçtan uca, süreçten sürece teslim; isteğe bağlı güvenilirlik ve akış kontrolü; portlar | TCP, UDP | **Segment** (TCP), **datagram** (UDP) |
| 3 | **Ağ (Network)** | Mantıksal adresleme ve ağlar arası yönlendirme | IPv4, IPv6, ICMP | **Paket (packet)** |
| 2 | **Veri Bağlantı (Data Link)** | Aynı ortamdaki komşular arasında çerçeve teslimi; MAC adresleme; hata tespiti | Ethernet, 802.11, PPP | **Çerçeve (frame)** |
| 1 | **Fiziksel (Physical)** | Bitleri sinyale çevirir; kablo, konnektör, gerilim, zamanlama | 1000BASE-T, fiber, radyo | **Bit** |

Sırayı hatırlamak için aşağıdan yukarıya Türkçe bir cümle: **"F**iziksel **V**eri **A**ğda **T**aşınır; **O**turum **S**unumla **U**ygulanır." Sınavda İngilizce adlar geçer; bilinen İngilizce cümle aşağıdan yukarıya "**P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way"dir.

Katman 2 için "Veri Bağı Katmanı" adı da kullanılır (USR-OSI-NOTES'ta bu ad geçer).

### 3.3 TCP/IP modeli

TCP/IP, 1970'lerde ABD Savunma Bakanlığı'nın araştırma ajansı DARPA'nın desteklediği ARPANET çalışmalarından doğdu. OSI'den önemli bir farkı vardır: **Önce protokoller yazıldı ve çalıştırıldı, model sonra tarif edildi.** RFC 1122 İnternet mimarisini dört katmanla tanımlar: **Application, Transport, Internet, Link** [RFC 1122 §1.1.3]. Bağlantı (Link) katmanı, host'un doğrudan bağlı olduğu ağla haberleşmek için gereken her şeyi kapsar.

```
   OSI (ISO/IEC 7498-1)       TCP/IP (RFC 1122)        Ders kitaplarında yaygın
                                                       5 katmanlı model
 ┌──────────────────────┐  ┌─────────────────────┐   ┌─────────────────────┐
 │ 7 Uygulama           │  │                     │   │                     │
 ├──────────────────────┤  │                     │   │                     │
 │ 6 Sunum              │  │  Application        │   │  Uygulama           │
 ├──────────────────────┤  │                     │   │                     │
 │ 5 Oturum             │  │                     │   │                     │
 ├──────────────────────┤  ├─────────────────────┤   ├─────────────────────┤
 │ 4 Taşıma             │  │  Transport          │   │  Taşıma             │
 ├──────────────────────┤  ├─────────────────────┤   ├─────────────────────┤
 │ 3 Ağ                 │  │  Internet           │   │  Ağ                 │
 ├──────────────────────┤  ├─────────────────────┤   ├─────────────────────┤
 │ 2 Veri Bağlantı      │  │                     │   │  Veri Bağlantı      │
 ├──────────────────────┤  │  Link               │   ├─────────────────────┤
 │ 1 Fiziksel           │  │                     │   │  Fiziksel           │
 └──────────────────────┘  └─────────────────────┘   └─────────────────────┘
```

*Ne görüyoruz:* TCP/IP, OSI'nin üst üç katmanını tek bir uygulama katmanında, alt iki katmanını tek bir bağlantı katmanında toplar. Kurose ve Odom gibi birçok ders kitabı ise bağlantı katmanını yeniden ikiye bölen beş katmanlı bir karma model kullanır.

**Hangi modeli kullanıyoruz?** Gerçek protokoller TCP/IP ailesindendir, ama sektör katmanlara **OSI numaralarıyla** ad verir: "L2 switch", "L4 yük dengeleyici", "L7 güvenlik duvarı". Bu müfredat da öyle yapar ve 5. ile 6. katmanları ayrı modüllerde (05-*, 06-*) inceler: O işlevler kaybolmadı, başka yerlere taşındı.

### 3.4 PDU adları

Her katmanın veri birimine genel olarak **PDU (protocol data unit)** denir. Bir PDU, o katmanın başlığı ile üst katmandan gelen yükün (payload) toplamıdır.

| Katman | PDU | Not |
|---|---|---|
| L5–L7 | Veri (data) | |
| L4 | Segment (TCP), datagram (UDP) | UDP'nin adı zaten "User Datagram Protocol"dür [RFC 768] |
| L3 | Paket (packet) | **Kaynaklar arasında fark:** RFC 791 IP'nin veri birimine "internet datagram" der; Cisco ve CCNA "packet" der [RFC 791] |
| L2 | Çerçeve (frame) | Başlığa ek olarak sonda bir **trailer** (Ethernet'te FCS) taşır |
| L1 | Bit | |

> **[DERİN]** OSI terminolojisinde N-PDU = N-PCI (kontrol bilgisi, yani başlık) + N-SDU (üst katmandan gelen hizmet veri birimi). Katmanların birbirine hizmet verdiği noktalara SAP (service access point) denir; port numaraları ve EtherType bu fikrin TCP/IP'deki karşılıklarıdır [ISO-7498].

### 3.5 Kapsülleme ve açma: genel bakış

**Gönderen tarafta (kapsülleme, encapsulation)** veri yukarıdan aşağıya iner ve her katman kendi başlığını ekler:

```
 Uygulama                         [          Veri (ör. bir HTTP isteği)       ]
 Taşıma                 [TCP başl.][                  Veri                    ]  ← segment
 Ağ           [IP başl.][TCP başl.][                  Veri                    ]  ← paket
 Veri Bağ. [Eth][IP başl.][TCP başl.][                Veri                 ][FCS]  ← çerçeve
 Fiziksel   preamble + çerçevenin bitleri → sinyal                               ← bitler
```

*Ne görüyoruz:* Her katman, üstünden aldığı her şeyi içi açılmayan bir yük olarak kabul eder ve önüne kendi başlığını koyar. Yalnızca veri bağlantı katmanı ayrıca sona bir trailer (FCS) ekler. Başlıkların alan alan görünümü ve boyutları 08-01'de.

**Alan tarafta (açma, decapsulation)** her katman kendi başlığını okur, kontrol eder, çıkarır ve yükü bir üst katmana verir. Peki hangi üst katmana? Her başlıkta, yükün kime ait olduğunu söyleyen bir alan vardır:

| Başlık | Alan | Örnek değer → anlamı |
|---|---|---|
| Ethernet | EtherType | 0x0800 → IPv4, 0x0806 → ARP, 0x86DD → IPv6 |
| IPv4 | Protocol | 1 → ICMP, 6 → TCP, 17 → UDP [IANA-PROTO] |
| TCP / UDP | Hedef port | 443 → HTTPS sunucusu, 53 → DNS sunucusu |

00-06, Bölüm 4'teki bayt dökümünde gördüğün `08 00` ve `06` değerleri tam olarak bu alanlardı.

**Ara cihazlar** veriyi yalnızca kendi işlerine yetecek kadar açar:

| Cihaz | Hangi katmana kadar açar? | Ne değiştirir? |
|---|---|---|
| Hub | L1 | Hiçbir şey; bitleri tekrarlar |
| Switch | L2 | Hiçbir şey; çerçeveyi olduğu gibi doğru porta iletir |
| Router | L3 | Eski L2 başlığını atar, TTL'yi azaltır, IPv4 checksum'ını yeniden hesaplar, **yeni** bir L2 başlığıyla gönderir (00-08, Bölüm 3.7) |
| Host | L7 | Hedefse her şeyi açar ve veriyi uygulamaya verir |

### 3.6 Protokoller katmanlara neden tam oturmaz?

**[TCP/IP-GERÇEK]** Bir protokolün katmanı iki farklı ölçüte göre belirlenebilir: (a) **hangi katmanın içinde taşındığı** ve (b) **hangi katmana hizmet ettiği.** Çoğu protokolde ikisi aynı katmanı gösterir; bazılarında göstermez:

| Protokol | İşlevi | İçinde taşındığı | Tartışma | Ayrıntı |
|---|---|---|---|---|
| **ARP** | IP adresini MAC adresine çevirir | Doğrudan Ethernet çerçevesi (EtherType 0x0806); IP başlığı yok | L3'e hizmet eder, L2'de taşınır: "L2,5" denir | 02-10 |
| **ICMP** | IP'nin hata ve kontrol mesajları (ping, traceroute) | IP paketi (protokol 1) | RFC 1122, ICMP'yi IP'nin ayrılmaz bir parçası sayar; ama mimari olarak IP'nin üstünde katmanlandığını belirtir [RFC 1122 §1.1.3] | 03-11 |
| **OSPF** | Yönlendirme bilgisi dağıtır | IP paketi (protokol 89) | L3 işlevi, L3 içinde taşınır | 03-14 |
| **BGP** | Ağlar arası yönlendirme bilgisi dağıtır | TCP (port 179) | L3'ün işini yapan bir uygulama protokolü | 03-13 |
| **DHCP** | Host'a IP adresi ve ağ ayarlarını verir | UDP (port 67 ve 68) | L3'ü yapılandırır, L7 protokolüdür | 07-03 |
| **TLS** | Şifreleme ve bütünlük; oturum kurma | TCP üzerinde, uygulamanın altında | OSI'de sunum ve oturum işlevleri; TCP/IP'de bir katman değil | 06-06 |

Bir de net olanı: **DNS bir uygulama katmanı (L7) protokolüdür.** Adresleri "çözmesi" onu ağ katmanına koymaz; UDP ya da TCP 53 üzerinde çalışan bir uygulamadır (07-02).

Bu tablo bir başarısızlık değildir; RFC 1122'nin kendisi de katı katmanlamanın "kusurlu bir model" olduğunu söyler [RFC 1122 §1.3.1]. Bir protokolü tek bir kutuya zorla koymak yerine **nerede taşındığını ve ne işe yaradığını** ayrı ayrı söyleyebilmek, sınavdaki tuzaklı sorulardan da korur.

### 3.7 Model ile uygulama farkı

Model bir **başvuru çerçevesidir**; bir yazılımın nasıl yazılacağını dikte etmez. Linux ve Windows'ta L2–L4 çekirdekte, L5–L7 uygulamanın ve kütüphanelerin içinde çalışır (00-07); NIC'ler L3–L4 işlerini üstlenebilir (offload); QUIC, taşıma katmanının işlevlerini kullanıcı alanında, UDP'nin üzerinde gerçekleştirir (04-06). Model, neyin nerede olduğunu düşünmek ve konuşmak için bir araçtır; arıza giderirken sorulacak soru "Hangi katmanın işi aksıyor?" sorusudur (11-01).

## 4. Teknik Ayrıntı

### 4.1 Başlık yükü (overhead)

Ethernet üzerinde, seçeneksiz IPv4 ve TCP başlıklarıyla:

| Durum | TCP yükü | TCP + IP | Ethernet başlık + FCS | Çerçeve | Kablodaki toplam (+20 bayt preamble/SFD ve IFG) | Verimlilik |
|---|---|---|---|---|---|---|
| Dosya aktarımı | 1460 bayt | 40 | 18 | 1518 | 1538 | 1460 / 1538 ≈ **%94,9** |
| Telnet'te tek tuş vuruşu | 1 bayt | 40 | 18 | 59 → **64** (en küçük çerçeveye dolgu) | 84 | 1 / 84 ≈ **%1,2** |

Birinci satırın sonucu: 1 Gbps'lık bir bağlantıda TCP ile elde edilebilecek en yüksek uygulama verimi yaklaşık 0,949 × 1000 ≈ **949 Mbps**, yani yaklaşık 118,7 MB/s'tır. 00-02'deki "1 Gbps = 125 MB/s (ham)" değeri ile indirme programında gördüğün değer arasındaki farkın bir kısmı buradan gelir. İkinci satır, küçük mesajların ağda neden pahalı olduğunu gösterir. 00-06'daki G.711 paketlerinde de verimlilik 160 / 238 ≈ %67'dir.

## 5. Gerçek Dünya Örnekleri

- **"İnternet yok" bileti:** Teknisyen aşağıdan yukarıya ilerler: Link ışığı yanıyor mu (L1)? Arayüz up/up mı (L2)? Bilgisayarın IP adresi ve ağ geçidi var mı, ağ geçidine ping gidiyor mu (L3)? `8.8.8.8`'e ping gidip alan adları çözülmüyorsa sorun DNS'tedir (L7). Her soru bir katmanı eler.
- **Yük dengeleyiciler:** Bir "L4 yük dengeleyici" bağlantıları IP adresine ve porta bakarak dağıtır. Bir "L7 yük dengeleyici" ise HTTP isteğinin içindeki adrese (URL) bakar; `/api` isteklerini bir sunucu grubuna, `/images` isteklerini başka birine gönderebilir. Adlar, cihazın hangi katmanın başlığını okuduğunu söyler (04-01, 07-01).

## 6. Diğer Konularla Bağlantı

| Bu dosyadaki fikir | Nerede derinleşiyor |
|---|---|
| Kapsüllemenin tam modeli, başlık boyutları | 08-01 |
| Katman katman arıza giderme | 11-01 |
| ARP'nin katmanı | 02-10 |
| ICMP | 03-11 |
| Yönlendirilen (IP) ve yönlendirme (OSPF, BGP) protokolleri | 03-13 |
| Oturum ve sunum işlevlerinin bugünkü yerleri | 05-02, 06-01, 06-06 |
| Mevcut notlardaki OSI'ye giriş ve PDU bölümleri | Notlar §1–2 (USR-OSI-NOTES) |

## 7. Cisco ve Pratik

**Packet Tracer:** Simulation Mode'da bir PDU'ya tıkladığında açılan pencerede **OSI Model** sekmesi, cihazın her katmanda ne yaptığını (in layers / out layers) gösterir (✅). Bunu LAB-002'de ayrıntılı kullanacaksın.

**Wireshark:** Paket ayrıntıları panelindeki satırlar katmanları sırayla gösterir: `Frame` (yakalama bilgisi), `Ethernet II` (L2), `Internet Protocol Version 4` (L3), `Transmission Control Protocol` (L4) ve varsa uygulama protokolü (L7). H02'de bu satırları açacaksın.

**[CISCO-ÖZEL]** `show ip interface brief` çıktısındaki iki sütun iki katmanı gösterir:

```
Router# show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.1.1     YES manual up                    up
GigabitEthernet0/1     10.0.0.1        YES manual down                  down
GigabitEthernet0/2     unassigned      YES unset  administratively down down
```

| Status / Protocol | Anlamı |
|---|---|
| up / up | L1 ve L2 çalışıyor |
| down / down | L1 sorunu: kablo yok, karşı taraf kapalı |
| up / down | L1 tamam, L2 sorunu (ör. seri hatlarda kapsülleme uyuşmazlığı) |
| administratively down / down | Arayüz `shutdown` ile kapatılmış |

Bu çıktı PT'de desteklenir (✅); ayrıntıları 01-10'da ve LAB-007'de.

## 8. Yaygın Yanılgılar

| Yanılgı | Doğrusu |
|---|---|
| "İnternet OSI modeliyle çalışır." | İnternet TCP/IP protokollerini kullanır. OSI bir başvuru modelidir; sektör onun katman numaralarını ortak dil olarak kullanır. |
| "Her protokol tek bir katmana aittir." | ARP, ICMP, BGP, DHCP ve TLS gibi protokollerin taşındığı katman ile hizmet ettiği katman farklıdır (Bölüm 3.6). |
| "DNS adresleri çözdüğü için ağ katmanında çalışır." | DNS bir uygulama katmanı (L7) protokolüdür; UDP/TCP 53 üzerinde çalışır. |
| "Router yalnızca L3'te çalışır; switch yalnızca L2'de." | Cihazın **iletim kararı** o katmandadır; ama her cihaz alt katmanları da uygular ve yönetim için L7 protokolleri çalıştırır. L3 switch'ler ayrıca yönlendirme yapar. |
| "Kapsülleme, verinin şifrelenmesi ya da sıkıştırılmasıdır." | Kapsülleme, her katmanın yükün önüne kendi başlığını (L2'de ayrıca sonuna trailer) eklemesidir. Yük değişmeden taşınır. |

## 9. Arıza Giderme Yaklaşımı

Katmanlar, bir arızayı sistematik olarak daraltmanın iskeletidir; yöntemler (bottom-up, top-down, divide and conquer) 11-01'de. Başlangıç için:

| Gözlem | Büyük olasılıkla sorunlu katman | İlk kontrol |
|---|---|---|
| Link ışığı yanmıyor; arayüz down/down | L1 | Kablo, port, karşı cihaz |
| Arayüz up/down | L2 | Kapsülleme, L2 ayarları |
| IP adresiyle ping gidiyor, adla gitmiyor | L7 (DNS) | `nslookup` |
| Ağ geçidine ping gitmiyor | L3 (ya da altı) | IP adresi, maske, ağ geçidi; ardından L2 (VLAN) |
| Ping gidiyor ama bir web sitesi açılmıyor | L4–L7 | Port engeli, TLS, uygulama |

## 10. CCNA Bağlantısı

v1.1 konu listesinde OSI ayrı bir madde olarak geçmez; ama sınav "L2", "L3", "L4" dilini her konuda kullanır. PDU adları, kapsülleme sırası, protokol ve cihazların katmanlarla ilişkisi ve `show ip interface brief` yorumu doğrudan sorulabilir.

## 11. Kendini Kontrol Et

1. OSI'nin yedi katmanını aşağıdan yukarıya sırala ve her biri için PDU adını yaz.
   <details><summary>Cevap</summary>
   1 Fiziksel (bit), 2 Veri Bağlantı (çerçeve), 3 Ağ (paket), 4 Taşıma (segment / datagram), 5 Oturum, 6 Sunum, 7 Uygulama (veri).
   </details>

2. RFC 1122'nin dört katmanı nelerdir? Her biri OSI'nin hangi katmanlarına karşılık gelir?
   <details><summary>Cevap</summary>
   Application (OSI 5–7), Transport (4), Internet (3), Link (1–2).
   </details>

3. Bir Ethernet çerçevesi alan bilgisayar, yükü IPv4'e vermesi gerektiğini nereden anlar? IP katmanı yükün TCP'ye ait olduğunu nereden anlar?
   <details><summary>Cevap</summary>
   Ethernet başlığındaki <b>EtherType</b> alanından (0x0800 = IPv4). IPv4 başlığındaki <b>Protocol</b> alanından (6 = TCP). TCP ise yükü <b>hedef port</b> numarasına göre doğru sokete verir.
   </details>

4. ARP'nin katmanı neden tartışmalıdır? DNS'in katmanı için aynı tartışma geçerli mi?
   <details><summary>Cevap</summary>
   ARP, L3'e hizmet eder (IP adresini MAC'e çevirir) ama IP başlığı olmadan doğrudan Ethernet çerçevesinde taşınır. DNS için tartışma yoktur: UDP/TCP üzerinde çalışan bir uygulama (L7) protokolüdür.
   </details>

5. 1460 baytlık TCP yükleriyle 1 Gbps Ethernet üzerinde elde edilebilecek en yüksek uygulama verimi yaklaşık nedir? Hesabını göster.
   <details><summary>Cevap</summary>
   Kabloda her segment için 1460 + 20 (TCP) + 20 (IP) + 18 (Ethernet ve FCS) + 20 (preamble, SFD, IFG) = 1538 bayt süresi kullanılır. 1460 / 1538 ≈ 0,949 → yaklaşık <b>949 Mbps</b> (~118,7 MB/s).
   </details>

## 12. Uygulama

1. Kaynağa bakmadan boş bir kâğıda OSI ve TCP/IP modellerini yan yana çiz. Her OSI katmanının yanına PDU adını ve iki örnek protokol yaz. Sonra Bölüm 3.2 ve 3.3 ile karşılaştır.
2. Bölüm 3.6'daki tabloyu kapat ve ARP, ICMP, OSPF, BGP, DHCP, TLS ve DNS için "taşındığı yer" ve "hizmet ettiği katman" sütunlarını kendin doldur.
3. Bölüm 4.1'deki hesabı 100 Mbps bir bağlantı için tekrarla.

## 13. Ustalık Kontrol Listesi

- [ ] Katmanlı tasarımın en az iki gerekçesini ve bir bedelini örnekle söyleyebiliyorum.
- [ ] OSI'nin yedi katmanını görevleri ve PDU adlarıyla, TCP/IP'nin dört katmanıyla eşleyerek kaynağa bakmadan yazabiliyorum.
- [ ] Kapsüllemeyi ve açmayı anlatabiliyor; alıcının EtherType, Protocol ve port alanlarıyla yükü nasıl yukarı verdiğini açıklayabiliyorum.
- [ ] ARP, ICMP, BGP, DHCP ve TLS'in katmanlara neden tam oturmadığını iki ölçütle (taşındığı yer, hizmet ettiği katman) açıklayabiliyorum.
- [ ] `show ip interface brief` çıktısındaki status ve protocol sütunlarını katmanlarla yorumlayabiliyorum.

## Kaynaklar

- [ISO-7498] ISO/IEC 7498-1:1994, OSI temel başvuru modeli; [ITU-X200] ITU-T X.200 (07/1994), aynı metin.
- [RFC 1122 §1.1.3] İnternet protokol ailesinin katmanları; ICMP'nin IP ile ilişkisi. [RFC 1122 §1.3.1] Katı katmanlamanın kusurlu bir model olması.
- [RFC 3439 §3] Katmanlamanın sakıncaları.
- [RFC 791] "Internet datagram" terimi; [RFC 768] UDP.
- [IANA-PROTO] IP protokol numaraları (1, 6, 17, 89).
- [IEEE-RA] EtherType değerleri (0x0800, 0x0806, 0x86DD).
- [TXT-KUROSE] Computer Networking: A Top-Down Approach, Bölüm 1.5: beş katmanlı model (ek okuma).
- [TXT-TANENBAUM] Computer Networks: OSI ve TCP/IP başvuru modellerinin karşılaştırması (ek okuma).

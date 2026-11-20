# 00-08 Ağ Temelleri (Networking Fundamentals)

> Önkoşullar: 00-07 | Tahmini süre: ~2 saat | CCNA: v1.1 1.1 (a–h)

## Öğrenme Hedefleri

- Ağın ne olduğunu açıklamak; LAN, WLAN ve WAN'ı ayırt etmek.
- v1.1 1.1'deki bileşenlerin (router, L2/L3 switch, NGFW/IPS, AP, kontrolcü, uç cihaz, sunucu, PoE) rolünü ve iletim kararını hangi bilgiyle verdiğini söylemek.
- İstemci-sunucu ve eşler arası (P2P) modelleri karşılaştırmak; protokol ile standart farkını ve standart kuruluşlarının alanlarını söylemek.
- Bant genişliği, verim, gecikmenin dört bileşeni ve jitter'ı tanımlamak; iletim ve yayılma gecikmesini hesaplamak.
- MAC adresi ile IP adresinin farklı işlerini açıklamak: Bir router'dan geçerken hangisi değişir, hangisi değişmez?

## 1. Sezgisel Giriş

Telefonunla bir video açtığında veri en az üç farklı ağdan geçer: Telefon, havadan evdeki kablosuz ağa bağlanır. Evdeki kutu veriyi İnternet servis sağlayıcının (İSS) ağına verir. İSS de onu, videoyu barındıran şirketin veri merkezine kadar başka ağlar üzerinden taşır. İnternet, tek bir ağ değil, **birbirine bağlanmış ağların ağıdır**.

Yolda her cihazın belirli bir işi vardır: Biri aynı odadaki cihazları bağlar, biri ağlar arasında yol bulur, biri kötü niyetli trafiği durdurur. Bu dosya bu rolleri ve temel ölçüleri tanıtır.

## 2. Neden Var?

Önceki dosyalar tek bir bilgisayarın içinde kaldı. Bu dosya dışarı çıkar ve ağın parçalarına ad verir; CCNA'nın ilk konusu (v1.1 1.1) doğrudan budur. CE-00'daki "IP adresi router'da değişir mi?" türünden sorulara ilk cevap da burada; mekanizmalar Faz 3 ve 4'te.

## 3. Mekanizma

### 3.1 Ağ nedir?

Bir **ağ (network)**, ortak kurallarla (protokollerle) veri alışverişi yapan iki ya da daha fazla cihazdır. Ağdaki her cihaza **düğüm (node)** denir. Düğümler iki gruba ayrılır:

- **Uç cihazlar (end devices, host):** Verinin kaynağı ya da hedefi. Bilgisayar, telefon, yazıcı, IP kamera, sunucu.
- **Ara cihazlar (intermediary devices):** Veriyi uç cihazlar arasında taşır. Switch, router, erişim noktası, güvenlik duvarı.

### 3.2 Ağ türleri

| Tür | Kapsadığı alan | Altyapının sahibi | Tipik teknoloji |
|---|---|---|---|
| **LAN** (local area network, yerel ağ) | Bir oda, bina ya da kampüs | Kurumun kendisi | Ethernet (IEEE 802.3) |
| **WLAN** (wireless LAN, kablosuz yerel ağ) | LAN ile aynı | Kurumun kendisi | Wi-Fi (IEEE 802.11) |
| **WAN** (wide area network, geniş alan ağı) | Şehirler, ülkeler | Genellikle bir servis sağlayıcı; kurum kiralar | Fiber hatlar, MPLS, İnternet üzerinden VPN |

Şehir ölçeğindeki MAN ve Bluetooth gibi PAN terimlerini de duyacaksın. WAN mimarileri 15-01'de.

### 3.3 Ağ bileşenleri ve rolleri (v1.1 1.1)

Aşağıdaki "Karar bilgisi" sütunu, cihazın veriyi **nereye ileteceğine** hangi bilgiye bakarak karar verdiğini gösterir. **[BASİTLEŞTİRME]** Bu, cihazın yalnızca o katmanda çalıştığı anlamına gelmez: Her cihaz alt katmanları da uygular; bir router'ın her arayüzünde L1 ve L2 vardır ve router yönetim için SSH, SNMP gibi L7 protokolleri çalıştırır.

| Bileşen | Görevi | Karar bilgisi | Ayrıntı |
|---|---|---|---|
| **Uç cihaz (endpoint)** | Veriyi üretir ve tüketir: PC, telefon, IP telefon, yazıcı, kamera, IoT cihazı | — | 03-06 |
| **Sunucu (server)** | Başka cihazlara hizmet veren bir host: web, DNS, DHCP, dosya. Sunucu bir donanım türü değil, bir **roldür** | — | 07-01 |
| **Hub** | Bir porttan gelen bitleri diğer bütün portlara tekrarlar. Bugün kullanılmaz; tarihsel karşılaştırma için önemlidir | Yok (L1) | 01-10, 02-07 |
| **L2 switch** | Aynı LAN içindeki cihazlar arasında çerçeveleri yalnızca ilgili porta iletir | Hedef **MAC adresi** (L2) | 02-06 |
| **L3 switch (multilayer)** | Switch işlevine ek olarak VLAN'lar arasında donanımda yönlendirme yapar | MAC adresi ve **IP adresi** | 03-10 |
| **Router** | Farklı ağlar arasında paketleri iletir; LAN'ı WAN'a bağlar; yayınları (broadcast) bir ağdan diğerine geçirmez | Hedef **IP adresi** (L3) | 03-07 |
| **Erişim noktası (AP, access point)** | Kablosuz istemcileri kablolu LAN'a bağlar | Kablosuz ve kablolu taraf arasında köprü (L2) | 02-15 |
| **Kontrolcüler (controllers)** | **WLC (wireless LAN controller)**: Birçok AP'yi merkezden yönetir. **Cisco Catalyst Center** (eski adı DNA Center): Kurum ağının tamamı için merkezi yönetim ve SDN kontrolcüsü | Politika ve yapılandırma | 02-16, 15-04 |
| **Güvenlik duvarı ve NGFW** | Trafiğe bir güvenlik politikasına göre izin verir ya da engeller; bağlantıların durumunu izler (stateful). **NGFW (next-generation firewall)** buna uygulama tanıma, URL filtreleme ve tümleşik IPS ekler | IP, port, bağlantı durumu; NGFW'de uygulama (L3–L7) | 14-01, 14-03 |
| **IPS (intrusion prevention system)** | Trafiği saldırı imzalarına ve anormalliklere göre inceler; saldırıyı trafik akarken (inline) engeller. Yalnızca uyarı veren türüne IDS denir | Paket içeriği (L3–L7) | 14-01 |
| **PoE (Power over Ethernet)** | Bir cihaz değil, bir yetenek: Switch (güç kaynağı, PSE), Ethernet kablosu üzerinden AP, IP telefon ve kameraya (güç alan cihaz, PD) DC güç verir | — | 00-04, 01-06 |

İki ayrım sık sorulur:

- **Switch ve router:** Switch, bir ağın *içinde* MAC adresine göre iletir ve yayınları bütün portlara gönderir. Router, ağlar *arasında* IP adresine göre iletir ve yayınları durdurur; her router arayüzü ayrı bir yayın alanı (broadcast domain) başlatır (02-07).
- **Ev router'ı:** Evdeki kutu, tek cihazda birleşmiş birkaç roldür: router, küçük bir switch, AP, DHCP sunucusu, NAT ve basit bir güvenlik duvarı. Kurumsal ağlarda bu roller ayrı cihazlardadır.

### 3.4 İstemci-sunucu ve eşler arası

| Model | Nasıl çalışır? | Örnekler | Güçlü yanı | Zayıf yanı |
|---|---|---|---|---|
| **İstemci-sunucu (client-server)** | İstemci isteği başlatır; sunucu bekler (dinler) ve yanıt verir | Web, e-posta, DNS | Merkezi yönetim, güvenlik ve yedekleme kolay | Sunucu tek arıza noktası olabilir; yük sunucuda toplanır |
| **Eşler arası (P2P, peer-to-peer)** | Her düğüm hem istemci hem sunucudur | BitTorrent; bazı görüntülü görüşme ve oyunlarda medya akışı | Katılımcı arttıkça kapasite de artar | Yönetim ve güvenlik zor; eşler gelip gider |

Birçok P2P uygulaması eşleri bulmak için yine bir sunucu kullanır (07-01).

### 3.5 Protokol ve standart

00-01'de protokolü "bitlerin anlamı üzerindeki ortak anlaşma" olarak tanımlamıştık. Daha ayrıntılı olarak bir **protokol (protocol)** üç şeyi tanımlar: mesajların **biçimi** (hangi alan nerede, kaç bit), **anlamı** (her değer ne demek) ve **sırası ile zamanlaması** (kim önce konuşur, ne kadar beklenir).

Bir **standart (standard)**, tanınmış bir kuruluşun yayımladığı ve farklı üreticilerin cihazlarının birlikte çalışmasını sağlayan belgedir.

| Kuruluş | Alanı | Örnek |
|---|---|---|
| **IEEE** (802 komitesi) | L1 ve L2: Ethernet, Wi-Fi, VLAN, STP | 802.3, 802.11, 802.1Q |
| **IETF** | İnternet protokolleri; belgeleri **RFC**'lerdir | RFC 791 (IPv4), RFC 9293 (TCP) |
| **ISO** (ISO/IEC) | Genel uluslararası standartlar | ISO/IEC 7498-1 (OSI modeli, 00-09) |
| **ITU-T** | Telekomünikasyon | G.711 (00-06), X.200 (OSI modelinin ITU karşılığı) |
| **IANA** | Numaraların kaydı: port numaraları, protokol numaraları, adres blokları | Port 443 = HTTPS |
| **TIA** | Yapısal kablolama | TIA-568 (01-06) |
| **Wi-Fi Alliance** | 802.11 cihazlarının birlikte çalışma sertifikası; WPA2 ve WPA3 | "Wi-Fi 6" adlandırması |

**[CISCO-ÖZEL]** Bazı protokoller Cisco tarafından geliştirilmiştir ve sınavda açık standart karşılıklarıyla birlikte sorulur: CDP ↔ LLDP (IEEE 802.1AB), HSRP ↔ VRRP (RFC 5798).

### 3.6 Performans ölçüleri

- **Bant genişliği (bandwidth):** Bir bağlantının saniyede taşıyabileceği en fazla bit sayısı (bps). Ağ dilinde "hız" denince genellikle bu kastedilir. (01-02'de göreceğin gibi fizikte "bant genişliği" hertz cinsinden bir frekans aralığıdır; ikisi ilişkilidir ama aynı şey değildir.)
- **Verim (throughput):** Gerçekte ölçülen aktarım hızı. Başlıklar, yeniden iletimler ve tıkanıklık yüzünden bant genişliğinden düşüktür. Uygulamaya ulaşan yararlı veriye ayrıca **goodput** denir.
- **Gecikme (latency, delay):** Bir bitin ya da paketin kaynaktan hedefe varma süresi. Her atlamada dört bileşeni vardır:

| Bileşen | Nedeni | Formül ya da tipik değer |
|---|---|---|
| **İletim (serileştirme, transmission/serialization)** | Paketin bütün bitlerini hatta "itmek" | Paket boyutu (bit) / bant genişliği (bps) |
| **Yayılma (propagation)** | Sinyalin ortamda yol alması | Mesafe / sinyal hızı; bakır ve fiberde ≈ 5 µs/km (00-04) |
| **Kuyruklama (queuing)** | Çıkış portu meşgulken paketin tamponda beklemesi | Değişken; tıkanıklıkta artar (03-21) |
| **İşleme (processing)** | Cihazın başlığı inceleyip karar vermesi | Donanımda mikrosaniyenin altında (00-07) |

- **RTT (round-trip time):** Gidiş-dönüş süresi. `ping` bunu ölçer.
- **Jitter:** Paketler arasındaki gecikme farkı. Ses ve görüntü için ortalama gecikme kadar önemlidir (03-21).
- **Paket kaybı (packet loss):** Hedefe hiç ulaşmayan paketlerin oranı.

Bant genişliği ile yayılma gecikmesi bağımsızdır: Bir otoyola şerit eklemek (bant genişliği) saatte geçen araç sayısını artırır, ama bir aracın varma süresini (yayılma) kısaltmaz.

### 3.7 MAC ve IP adresine ilk bakış

| | MAC adresi | IPv4 adresi |
|---|---|---|
| Uzunluk | 48 bit, ör. `00:1A:2B:3C:4D:5E` (Cisco yazımı: `001a.2b3c.4d5e`) | 32 bit, ör. `192.168.1.10` |
| Kim atar? | Üretici NIC'e atar; işletim sistemi değiştirebilir ya da rastgeleleştirebilir | Yönetici ya da DHCP |
| Yapısı | Düz (konumla ilgisi yok) | Hiyerarşik: ağ kısmı + host kısmı (00-03'teki maske) |
| Geçerlilik alanı | Yalnızca **aynı yerel bağlantıda** (aynı L2 ağında) | **Uçtan uca**: kaynaktan hedefe |
| Katman | L2 | L3 |

Bir mektup düşün. Zarfın üzerindeki alıcı adresi (IP), mektup yolculuk boyunca hiç değişmez. Ama mektup her postaneden bir sonrakine giderken yeni bir kurye çantasına konur ve çantanın üzerine yalnızca **bir sonraki postanenin** adı yazılır (MAC). Her durakta eski çanta atılır, yenisi hazırlanır.

```
  PC1 ─────────── Switch ─────────── R1 ─────────── Switch ─────────── Sunucu
  192.168.1.10                  G0/0 │ G0/1                        203.0.113.10
  MAC: A                        MAC: B │ MAC: C                    MAC: D

            1. bağlantı                             2. bağlantı
  ┌────────────────────────────────────┐  ┌────────────────────────────────────┐
  │ Kaynak MAC A  →  Hedef MAC B       │  │ Kaynak MAC C  →  Hedef MAC D       │
  │ Kaynak IP 192.168.1.10             │  │ Kaynak IP 192.168.1.10   (aynı)    │
  │ Hedef IP  203.0.113.10             │  │ Hedef IP  203.0.113.10   (aynı)    │
  └────────────────────────────────────┘  └────────────────────────────────────┘
```

*Ne görüyoruz:* PC1, sunucunun başka bir ağda olduğunu kendi maskesiyle anlar ve çerçeveyi **varsayılan ağ geçidinin (default gateway)**, yani R1'in MAC adresine (B) gönderir. R1, çerçeveyi açar, IP başlığındaki hedefe bakar ve paketi **yeni bir çerçeveyle** (kaynak C, hedef D) gönderir. MAC adresleri her bağlantıda değişir; IP adresleri değişmez. (Router ayrıca TTL'yi bir azaltır.)

Bu kuralın bir istisnası vardır: Ev router'larında olduğu gibi NAT yapan bir cihaz, kaynak IP adresini değiştirir (03-20). Yerel/uzak kararının nasıl verildiği 03-06'da, router'ın MAC adresinin nasıl öğrenildiği (ARP) 02-10'da.

## 4. Teknik Ayrıntı: Gecikme ve süre hesapları

**İletim gecikmesi.** 1500 baytlık bir paket = 12.000 bit:

| Bağlantı | Hesap | İletim gecikmesi |
|---|---|---|
| 2 Mbps WAN hattı | 12.000 / 2 × 10⁶ | 6 ms |
| 10 Mbps | 12.000 / 10⁷ | 1,2 ms |
| 100 Mbps | 12.000 / 10⁸ | 120 µs |
| 1 Gbps | 12.000 / 10⁹ | 12 µs |

**Yayılma gecikmesi.** Kazan ile İstanbul arası kuş uçuşu yaklaşık 2.200 km'dir:

> 2.200 km × 5 µs/km ≈ 11 ms (tek yön) → RTT için **teorik alt sınır ≈ 22 ms**

Gerçek ping daha yüksektir: Fiber güzergâhı kuş uçuşundan uzundur ve her atlamada iletim, kuyruklama ve işleme gecikmesi eklenir. Ama hiçbir bant genişliği artışı RTT'yi bu alt sınırın altına indiremez.

**Aktarım süresi.** 1 GB'lık (10⁹ bayt) bir dosya, 100 Mbps'lık bir bağlantıda en iyi durumda 8 × 10⁹ / 10⁸ = **80 saniyede** iner. Başlıklar ve TCP davranışı yüzünden gerçek süre daha uzundur (00-02, Bölüm 4.9; 04-05).

## 5. Gerçek Dünya Örnekleri

- **Ev (SOHO):** Tek kutu router, switch, AP, DHCP ve NAT görevlerini birlikte yapar. Kablosuz yazıcıya erişebiliyor ama İnternet'e çıkamıyorsan sorun büyük olasılıkla kutunun WAN tarafındadır, LAN tarafında değil.
- **Kurumsal kampüs:** Katlarda PoE destekli access switch'ler IP telefonlara ve tavandaki AP'lere güç verir; AP'leri bir WLC yönetir. Dağıtım katmanındaki L3 switch'ler VLAN'lar arasında yönlendirme yapar; kenarda bir NGFW, kurumu İnternet'ten ayırır.

## 6. Diğer Konularla Bağlantı

| Bu dosyadaki fikir | Nerede derinleşiyor |
|---|---|
| Hub, çarpışma ve yayın alanları | 01-10, 02-07 |
| Switch ve router iletimi | 02-06, 03-07 |
| Varsayılan ağ geçidi ve yerel/uzak kararı | 03-06 |
| MAC ve IPv4 adreslerinin yapısı | 02-02, 03-03 |
| AP, WLC ve kablosuz mimariler | 02-15, 02-16 |
| Güvenlik duvarı, IPS, ACL | 14-01, 14-03 |
| Kampüs, WAN ve SOHO mimarileri | 15-01 |
| Kuyruklama ve jitter | 03-21 |

## 7. Cisco ve Pratik

Packet Tracer'da bir cihazın rolünü ve adreslerini şu komutlarla görürsün (hepsi PT'de desteklenir ✅; LAB-001'de kullanılacak):

```
Router# show version                     ! model, IOS sürümü, arayüz sayısı
Router# show ip interface brief          ! arayüzler, IP adresleri, durumları
Switch# show mac address-table           ! switch'in öğrendiği MAC adresleri ve portları
PC> ipconfig /all                        ! PT'de PC'nin IP, maske, ağ geçidi ve MAC'i
```

Kendi bilgisayarında:

```
# Windows
> ipconfig /all          # "Physical Address" = MAC, "Default Gateway" = router
# Fedora
$ ip addr                # link/ether = MAC, inet = IPv4 adresi ve önek uzunluğu
$ ip route               # "default via ..." satırı = varsayılan ağ geçidi
```

## 8. Yaygın Yanılgılar

| Yanılgı | Doğrusu |
|---|---|
| "Switch ve router aynı işi yapar; router yalnızca daha büyüktür." | Switch bir ağın içinde MAC adresine göre iletir ve yayınları geçirir. Router ağlar arasında IP adresine göre iletir ve yayınları durdurur. |
| "Bir paket router'dan geçerken IP adresleri değişir, MAC adresleri aynı kalır." | Tam tersi: MAC adresleri her bağlantıda yeniden yazılır; IP adresleri (NAT yoksa) uçtan uca aynı kalır. |
| "Bant genişliğini artırırsam bitler kabloda daha hızlı gider." | Sinyal hızı ortama bağlıdır ve değişmez. Bant genişliği saniyede gönderilen bit sayısını artırır; iletim gecikmesi azalır, yayılma gecikmesi aynı kalır. |
| "Sunucu, özel bir bilgisayar türüdür." | Sunucu bir roldür. Hizmet veren her cihaz sunucudur; dizüstü bilgisayarın da bir web sunucusu çalıştırabilir. |
| "Ev router'ı yalnızca bir router'dır." | Router, switch, AP, DHCP sunucusu, NAT ve güvenlik duvarı rollerini tek kutuda birleştirir. |

## 9. Arıza Giderme Yaklaşımı

Bu dosyadaki rol bilgisi, bir arızanın **nerede** olabileceğini daraltır:

| Belirti | Daraltma | Ayrıntı |
|---|---|---|
| Aynı LAN'daki yazıcıya erişim var, İnternet yok | LAN (switch) çalışıyor; sorun ağ geçidi, router'ın WAN tarafı ya da DNS | 03-06, 07-02 |
| Kablosuza bağlı ama geçerli IP adresi yok | Kablosuz ilişkilendirme tamam; DHCP'ye bak | 07-03 |
| Uzak bir sunucuya ping yüksek ve dalgalı | Sabit yüksek değer: yayılma (mesafe) ya da yavaş hat. Dalgalanma: kuyruklama (tıkanıklık) | 03-11, 03-21 |

## 10. CCNA Bağlantısı

Bu dosya v1.1 1.1'in bütün alt maddelerine ilk cevabı verir:

| v1.1 | Konu | Bölüm |
|---|---|---|
| 1.1.a | Router | 3.3, 3.7 |
| 1.1.b | L2 ve L3 switch | 3.3 |
| 1.1.c | NGFW ve IPS | 3.3 |
| 1.1.d | Erişim noktası | 3.3 |
| 1.1.e | Kontrolcüler (Catalyst Center/DNA Center, WLC) | 3.3 |
| 1.1.f | Uç cihazlar | 3.1, 3.3 |
| 1.1.g | Sunucular | 3.3, 3.4 |
| 1.1.h | PoE | 3.3 (ayrıntı 00-04, 01-06) |

Sınavda bu konu genellikle "Hangi cihaz ...?" biçiminde çoktan seçmeli sorularla gelir. Özellikle geleneksel güvenlik duvarı ile NGFW'nin ve IPS ile IDS'nin farkını bil.

## 11. Kendini Kontrol Et

1. 1500 baytlık bir paketin 10 Mbps ve 1 Gbps bağlantılardaki iletim gecikmesi nedir?
   <details><summary>Cevap</summary>
   12.000 bit / 10⁷ bps = <b>1,2 ms</b>; 12.000 bit / 10⁹ bps = <b>12 µs</b>.
   </details>

2. İki şehir arasında 3.000 km fiber var. Tek yön yayılma gecikmesi ve RTT için alt sınır nedir? Bağlantıyı 1 Gbps'tan 10 Gbps'a çıkarmak bu değerleri değiştirir mi?
   <details><summary>Cevap</summary>
   3.000 × 5 µs = <b>15 ms</b> tek yön, RTT alt sınırı <b>30 ms</b>. Hayır; bant genişliği yayılma gecikmesini değiştirmez, yalnızca iletim gecikmesini azaltır.
   </details>

3. Hub, switch ve router'dan hangisi yayın (broadcast) trafiğini bir ağdan diğerine geçirmez? Neden?
   <details><summary>Cevap</summary>
   <b>Router</b>. Router, IP adresine göre ağlar arasında iletim yapar; yayınlar yalnızca bir ağın içinde anlamlıdır. Hub ve switch yayınları bütün portlarına gönderir.
   </details>

4. Bölüm 3.7'deki şekilde PC1'den sunucuya giden paket R1'den geçtiğinde hangi adres alanları değişir? Hangileri değişmez?
   <details><summary>Cevap</summary>
   Değişen: kaynak MAC (A → C) ve hedef MAC (B → D); ayrıca TTL bir azalır. Değişmeyen: kaynak ve hedef IP adresleri (NAT yoksa).
   </details>

5. Protokol ile standart arasındaki fark nedir? 802.11 ve TCP'nin belgelerini hangi kuruluşlar yayımlar?
   <details><summary>Cevap</summary>
   Protokol, iletişimin kurallarıdır (biçim, anlam, sıra). Standart, bu kuralların tanınmış bir kuruluşça yayımlanmış ve farklı üreticilerin uyduğu hâlidir. 802.11'i <b>IEEE</b>, TCP'yi (RFC 9293) <b>IETF</b> yayımlar.
   </details>

## 12. Uygulama

1. Kendi bilgisayarında `ipconfig /all` (Windows) ya da `ip addr` ve `ip route` (Fedora) ile MAC adresini, IP adresini ve varsayılan ağ geçidini bul.
2. Önce ağ geçidine, sonra `8.8.8.8`'e ping at. İki RTT arasındaki farkı Bölüm 3.6'daki dört gecikme bileşeniyle açıkla: Fark büyük ölçüde hangisinden geliyor?
3. Evindeki kutunun hangi rolleri (router, switch, AP, DHCP, NAT) üstlendiğini listele. Kutunun arkasındaki portlardan hangisinin WAN, hangilerinin LAN tarafı olduğunu bul.

## 13. Ustalık Kontrol Listesi

- [ ] v1.1 1.1'deki sekiz bileşenin rolünü ve iletim kararını hangi bilgiyle verdiğini kaynağa bakmadan söyleyebiliyorum.
- [ ] Switch ile router arasındaki farkı yayın alanı kavramıyla açıklayabiliyorum.
- [ ] İletim ve yayılma gecikmesini hesaplayabiliyor, bant genişliğinin yayılma gecikmesini neden değiştirmediğini anlatabiliyorum.
- [ ] İki alt ağ arasındaki bir pakette her bağlantıdaki MAC ve IP adreslerini yazabiliyorum.
- [ ] IEEE, IETF, ISO, ITU-T ve IANA'nın alanlarını birer örnekle söyleyebiliyorum.

## Kaynaklar

- [CISCO-V11] Cisco, CCNA Exam v1.1 (200-301): konu 1.1 ve alt maddeleri (a–h).
- [IEEE-8023] Ethernet; [IEEE-80211] Wi-Fi; [IEEE-8021AB] LLDP.
- [RFC 791] IPv4; [RFC 9293] TCP; [RFC 5798] VRRPv3; [RFC 5737] dokümantasyon adresleri.
- [IANA-PORTS] Port numarası kayıtları.
- [TXT-KUROSE] Computer Networking: A Top-Down Approach, Bölüm 1: gecikmenin dört bileşeni (ek okuma).
- [TXT-ODOM] CCNA 200-301 Official Cert Guide: ağ bileşenleri (ek okuma).

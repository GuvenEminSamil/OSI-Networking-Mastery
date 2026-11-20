# 00-06 Veri Temsili (Data Representation)

> Önkoşullar: 00-02 (00-03 yardımcı olur) | Tahmini süre: ~1,5–2 saat | CCNA: dolaylı (başlık alanlarının okunuşu; ses trafiği ve QoS, v1.1 2.1 voice VLAN ve 4.7)

## Öğrenme Hedefleri

- Aynı bayt dizisinin farklı anlamlara gelebildiğini bir örnekle göstermek.
- Bir alanın bit genişliğinden alabileceği değer aralığını hesaplamak ve bunun protokol sınırlarını nasıl belirlediğini açıklamak.
- Big-endian ve little-endian ayrımını ve ağ bayt sırasını (network byte order) açıklamak; çok baytlı bir değeri kabloda gidecek sırayla yazmak.
- Metin, görüntü, ses ve video için gereken bit hızını hesaplamak; ses için Nyquist koşulunu söylemek.
- Her dosyanın bir bayt dizisi olduğunu ve türünün nasıl anlaşıldığını açıklamak.

## 1. Sezgisel Giriş

Şu dört bayta bak: `C0 A8 01 01`. Bunlar ne anlama gelir?

| Yorum | Sonuç |
|---|---|
| Bir IPv4 adresi (her bayt bir oktet) | **192.168.1.1** |
| 32 bitlik işaretsiz bir sayı (big-endian) | 3.232.235.777 |
| Aynı sayı, ters bayt sırasıyla okunursa (little-endian) | 16.885.952 |
| Bir pikselin rengi (kırmızı, yeşil, mavi) + opaklık (alpha) | Hardal sarısına yakın bir renk; opaklık 1/255, yani neredeyse tamamen saydam |

Baytlar kendi anlamlarını taşımaz. Anlamı, iki tarafın önceden üzerinde anlaştığı **yorum kuralı** verir. 00-01'deki "veri ile bilgi" ayrımının pratikteki karşılığı budur ve protokollerin var olma nedeni de budur.

## 2. Neden Var?

Ağdaki her başlık alanı, belirli genişlikte ve belirli bir bayt sırasıyla yazılmış bir sayıdır. Başlıkların arkasındaki yük (payload) ise metin, görüntü, ses ya da bir dosya olabilir. Bu dosyayı bilmeden:

- Wireshark'taki onaltılık dökümü okuyamazsın (H02).
- "Neden en fazla 4094 VLAN var?" sorusunu ezberle cevaplarsın.
- Bir sesli görüşmenin hattan ne kadar bant genişliği istediğini hesaplayamazsın (03-21).

## 3. Mekanizma

### 3.1 Tamsayılar ve alan genişliği

00-02'deki kural: **n bit, 2ⁿ farklı değer** taşır.

- **İşaretsiz (unsigned):** 0 … 2ⁿ − 1. Ağ başlıklarındaki alanların neredeyse tamamı işaretsizdir.
- **İşaretli (signed), ikiye tümleyen:** −2ⁿ⁻¹ … 2ⁿ⁻¹ − 1 (00-03, Bölüm 3.3).

Bir alanın genişliği, protokolün sınırını belirler:

| Alan | Genişlik | Değer aralığı | Ayrıntı |
|---|---|---|---|
| IPv4 TTL | 8 bit | 0–255 | 03-02 |
| 802.1Q VLAN kimliği (VID) | 12 bit | 0–4.095; 0 ve 4.095 ayrılmıştır → **1–4.094** kullanılabilir | 02-09 |
| TCP/UDP port numarası | 16 bit | 0–65.535 | 04-01 |
| IPv4 Total Length | 16 bit | En fazla 65.535 bayt | 03-02 |
| TCP sıra numarası | 32 bit | 0–4.294.967.295; sonra 0'a döner (00-03, taşma) | 04-04 |
| IPv4 adresi | 32 bit | ~4,3 milyar | 03-03 |
| MAC adresi | 48 bit | ~2,8 × 10¹⁴ | 02-02 |
| IPv6 adresi | 128 bit | ~3,4 × 10³⁸ | 03-16 |

"Neden 4094 VLAN?" sorusunun cevabı bir ezber değil, bir hesaptır: 2¹² = 4096 değer, eksi ayrılmış iki değer [IEEE-8021Q].

### 3.2 Bayt sırası (endianness)

Bir değer birden fazla bayt tutuyorsa, baytların hangi sırayla saklanacağına ya da gönderileceğine karar vermek gerekir. 32 bitlik `0x12345678` değeri için:

```
 Adres / gönderim sırası →    1.     2.     3.     4.
 Big-endian (önce büyük uç):  [12]   [34]   [56]   [78]    ← ağ bayt sırası
 Little-endian (önce küçük):  [78]   [56]   [34]   [12]    ← x86 belleği
```

*Ne görüyoruz:* Değer aynıdır; yalnızca baytların sırası farklıdır. Big-endian'da en anlamlı bayt (0x12) önce gelir; insanlar sayıları da böyle yazar.

- **[TCP/IP-GERÇEK]** İnternet protokolleri çok baytlı alanları **big-endian** gönderir. Buna **ağ bayt sırası (network byte order)** denir. RFC 791, oktetlerin diyagramlarda soldan sağa, yukarıdan aşağıya okunduğu sırayla iletildiğini tanımlar [RFC 791, Ek B].
- Bugünkü kişisel bilgisayarların çoğu (x86 ve tipik yapılandırmasıyla ARM) belleği **little-endian** kullanır.
- Bu yüzden ağ programları, bir değeri pakete yazmadan önce ağ bayt sırasına çevirir. Soket API'sindeki `htons()` ("host to network short", 16 bit) ve `htonl()` (32 bit) işlevleri bunu yapar; `ntohs()` ve `ntohl()` tersini yapar (04-07).

Terimler, Danny Cohen'in 1980 tarihli bir yazısından gelir. Cohen, Gulliver'in Gezileri'nde yumurtanın hangi ucundan kırılacağı yüzünden savaşan iki halkın adlarını bu tartışmaya uyarlamıştır [PAPER-COHEN].

**Somut bir hata:** Port 443, 16 bit olarak `0x01BB`'dir ve kabloda `01 BB` sırasıyla gider. Little-endian bir bilgisayarda bellekte `BB 01` olarak durur. Program `htons()` çağırmayı unutursa belleği olduğu gibi pakete kopyalar ve kabloya `BB 01` gider. Karşı taraf bunu `0xBB01` = **47.873** olarak okur. Bağlantı kurulmaz, Wireshark'ta da 47873 numaralı porta giden bir paket görünür.

> **[DERİN]** Bayt sırası ile **bit sırası** ayrı konulardır. Ethernet her baytın bitlerini en az anlamlı bitten başlayarak gönderir [IEEE-8023]. Bu ayrıntı, bir MAC adresinin ilk baytındaki I/G bitinin neden kabloya ilk çıkan bit olduğunu açıklar (02-02).

### 3.3 Metin

Metin, her karaktere bir sayı karşılık getiren bir tabloyla temsil edilir: **karakter kodlaması (character encoding)**.

- **ASCII** 7 bitlik bir tablodur (0–127). Örnekler: `A` = 0x41 (65), `0` = 0x30 (48), boşluk = 0x20, satır sonu için CR = 0x0D ve LF = 0x0A.
- Türkçe karakterler (ş, ğ, ı, İ) ASCII'de yoktur. Bunlar için önce bölgesel kod sayfaları (Windows-1254, ISO-8859-9), bugün ise **Unicode** ve onun bayt düzeyindeki kodlaması **UTF-8** kullanılır. UTF-8'de bir karakter 1 ile 4 bayt arasında yer tutar; ASCII karakterler 1, "ş" gibi karakterler 2 bayttır.

Ayrıntılar ve bozuk Türkçe metin (mojibake) örnekleri 06-02'de. Burada bilmen gereken şu: HTTP, SMTP ve FTP gibi birçok uygulama protokolü komutlarını **ASCII metin** olarak gönderir. Örneğin bir HTTP isteği `GET / HTTP/1.1` satırıyla ve CR LF ile biter. Bu yüzden şifrelenmemiş bir bağlantıyı Wireshark'ta okunabilir metin olarak görürsün (07-04).

### 3.4 Görüntü

Bir **raster görüntü**, piksellerden oluşan bir ızgaradır. Her pikselin rengi genellikle kırmızı, yeşil ve mavi (RGB) için 8'er bit, yani 24 bitle tutulur. 2²⁴ ≈ 16,7 milyon renk eder.

> 1920 × 1080 piksel × 3 bayt = 6.220.800 bayt ≈ **6,2 MB** (sıkıştırılmamış tek bir Full HD kare)

PNG bu veriyi kayıpsız, JPEG ise insan gözünün fark etmediği ayrıntıları atarak kayıplı sıkıştırır (06-04).

### 3.5 Ses: örnekleme, Nyquist ve PCM

00-01'de analog bir sinyalin iki adımda dijitale çevrildiğini gördün: **örnekleme (sampling)** ve **nicemleme (quantization)**. Kaç örnek yeterlidir?

**Nyquist koşulu:** Bir sinyaldeki en yüksek frekans f_max ise örnekleme frekansı **2 × f_max'tan büyük** olmalıdır. Daha seyrek örneklenirse yüksek frekanslar sahte düşük frekanslar gibi görünür (aliasing). Bu yüzden ses örneklenmeden önce süzgeçten geçirilir ve f_max'ın üstü atılır [CISCO-PCM]. Teoremin türetilmesi 01-02'de.

| Uygulama | f_max (yaklaşık) | Örnekleme | Örnek başına bit | Kanal | Bit hızı |
|---|---|---|---|---|---|
| Telefon (G.711 PCM) | 3,4 kHz | 8.000 örnek/s | 8 | 1 | 8.000 × 8 = **64 kbps** |
| Müzik CD'si | 20 kHz | 44.100 örnek/s | 16 | 2 | 44.100 × 16 × 2 = **1.411,2 kbps** |

Telefon sesinin bu yöntemle sayısallaştırılmasına **PCM (pulse code modulation)** denir ve ITU-T G.711'de tanımlıdır [ITU-G711]. IP telefonların varsayılan kodeklerinden biri hâlâ G.711'dir.

### 3.6 Video

Video, saniyede belirli sayıda görüntüden (kare, frame) oluşur. Sıkıştırılmamış 1080p, 30 kare/s bir video:

> 6.220.800 bayt × 30 kare/s × 8 bit ≈ **1,49 Gbps**

Bir video akış servisi aynı görüntüyü tipik olarak birkaç Mbps ile gönderir; yani sıkıştırma oranı yüzlerle ifade edilir. Bunu **kodekler (codec)** sağlar (H.264, H.265, AV1). Kodek iki fazlalıktan yararlanır:

- **Kare içi (spatial):** Bir karede yan yana duran pikseller birbirine benzer.
- **Kareler arası (temporal):** Ardışık kareler birbirine çok benzer. Kodek ara sıra tam bir kare (I-frame) gönderir; arada yalnızca değişen kısımları (P- ve B-frame) gönderir.

Ağdaki sonucu: Kayıp bir I-frame, bir sonrakine kadar görüntünün bozulmasına yol açar. Kayba toleransı ve gecikme gereksinimi, videonun TCP mi UDP mi kullanacağını etkiler (04-06).

### 3.7 Her dosya bir bayt dizisidir

Bir disk ya da ağ için fotoğraf, belge ve program arasında fark yoktur: Hepsi bir **bayt dizisidir**. Türü belirleyen, dizinin nasıl yorumlanacağıdır:

- **Dosya uzantısı** (`.png`, `.pdf`) yalnızca bir ipucudur; değiştirilebilir.
- Birçok biçim dosyanın ilk baytlarına sabit bir **imza (magic number)** koyar. Örneğin her PNG dosyası şu 8 baytla başlar: `89 50 4E 47 0D 0A 1A 0A` [STD-PNG §5.2]. 2.–4. baytlar ASCII'de "PNG" demektir. PDF dosyaları ise ASCII `%PDF-` metniyle başlar.
- Ağda türü **protokol** bildirir. HTTP, yükün türünü `Content-Type: image/png` gibi bir başlıkla söyler (MIME türleri, 06-03).

Bu bağımsızlık önemli bir tasarım ilkesidir: Ağın alt katmanları taşıdıkları baytların ne olduğuyla ilgilenmez; yorum en üst katmana bırakılır (00-09).

## 4. Teknik Ayrıntı: Bir paketin baytlarını okumak

Aşağıda bir bilgisayarın bir web sunucusuna gönderdiği ilk TCP paketinin başı var. **[BASİTLEŞTİRME]** Satırlar alanlara göre bölündü (Wireshark her satırda 16 bayt gösterir); MAC adresleri ve checksum `xx` ile gizlendi.

```
Ethernet  xx xx xx xx xx xx  xx xx xx xx xx xx  08 00
IPv4      45 00 00 3c 1c 46 40 00 40 06 xx xx  c0 a8 01 0a  cb 00 71 0a
TCP       c9 3a 01 bb ...
```

| Baytlar | Yorum | Nasıl? |
|---|---|---|
| `08 00` | EtherType = IPv4 | 0x0800 (00-02) |
| `45` | Sürüm 4, başlık uzunluğu 5 × 4 = 20 bayt | Üst nibble = 4, alt nibble = 5 (00-02, Bölüm 4.4) |
| `00 3c` | Toplam uzunluk 60 bayt | 0x003C, big-endian |
| `40` (9. bayt) | TTL = 64 | 0x40 |
| `06` | Üst protokol = TCP | IANA protokol numarası 6 [IANA-PROTO] |
| `c0 a8 01 0a` | Kaynak IP 192.168.1.10 | Her bayt bir oktet |
| `cb 00 71 0a` | Hedef IP 203.0.113.10 | Dokümantasyon adresi [RFC 5737] |
| `c9 3a` | Kaynak port 51.514 | 0xC93A |
| `01 bb` | Hedef port 443 (HTTPS) | 0x01BB |

Bu tabloyu bir kez kendi başına doldurabildiğinde, H02'de Wireshark'ın alt panelindeki onaltılık dökümü korkmadan okuyabilirsin. Alanların ne işe yaradığı 03-02 ve 04-03'te.

## 5. Gerçek Dünya Örnekleri

- **IP telefon planlaması:** G.711'in 64 kbps'ı yalnızca ses verisidir. Varsayılan 20 ms'lik paketlerde her pakette 160 bayt ses taşınır ve saniyede 50 paket gider. Her pakete RTP (12) + UDP (8) + IP (20) = 40 bayt başlık eklenir: (160 + 40) × 8 × 50 = **80 kbps**. Ethernet başlığı ve FCS (toplam 18 bayt) de eklenince **87,2 kbps** olur [CISCO-VOIP-BW]. 20 eş zamanlı görüşme taşıyacak bir WAN bağlantısı bu yüzden 20 × 64 kbps ile değil, gerçek değerle planlanır (03-21).
- **Video akışı:** Bir dizi izlerken ağ yavaşlarsa oynatıcı çözünürlüğü düşürür. Kodek, daha az bitle daha düşük kaliteli kareler göndermeye geçer.
- **Kendi yazdığın sunucu:** Little-endian bir makinede port numarasını `htons()` olmadan yazan bir Python ya da C programı, Bölüm 3.2'deki gibi yanlış porta bağlanmaya çalışır.

## 6. Diğer Konularla Bağlantı

| Bu dosyadaki fikir | Nerede derinleşiyor |
|---|---|
| Alan genişlikleri ve başlık okuma | 02-03, 02-09, 03-02, 04-03 |
| Ağ bayt sırası, `htons()` | 04-07 |
| Bit sırası ve MAC adresinin I/G biti | 02-02 |
| Karakter kodlaması, UTF-8, mojibake | 06-02 |
| Serileştirme ve MIME türleri | 06-03 |
| Kayıpsız ve kayıplı sıkıştırma, kodekler | 06-04 |
| Nyquist teoremi | 01-02 |
| Ses ve video trafiğinin önceliklendirilmesi | 02-08 (voice VLAN), 03-21 |

## 7. Pratik: Baytları kendi gözünle gör

Bu dosyanın Cisco komutu yoktur; araçlar senin bilgisayarında. Bir PNG ya da PDF dosyasının ilk baytlarına bak:

```
# Fedora
$ xxd resim.png | head -2
$ file resim.png                 # imzaya bakarak türü söyler, uzantıya değil

# Windows PowerShell
PS> Format-Hex -Path .\resim.png | Select-Object -First 2
```

Dosyanın uzantısını değiştir (`resim.png` → `resim.txt`) ve `file` komutunu yeniden çalıştır. Sonuç değişmez, çünkü `file` imzaya bakar.

## 8. Yaygın Yanılgılar

| Yanılgı | Doğrusu |
|---|---|
| "Dosyanın türünü uzantısı belirler." | Uzantı bir ipucudur. Tür, baytların yorumundan anlaşılır: dosyanın imzası ya da ağda protokolün bildirdiği tür (`Content-Type`). |
| "Bilgisayar ağ verisini kendi bayt sırasıyla gönderir." | İnternet protokolleri big-endian (ağ bayt sırası) kullanır; little-endian bir bilgisayar çok baytlı alanları göndermeden önce çevirmek zorundadır. |
| "Bir G.711 görüşmesi 64 kbps kullanır." | 64 kbps yalnızca ses verisidir. Başlıklarla IP düzeyinde 80 kbps, Ethernet üzerinde 87,2 kbps eder. |
| "Bir karakter her zaman bir bayttır." | Bu yalnızca ASCII için doğrudur. UTF-8'de bir karakter 1–4 bayttır; Türkçe harflerin çoğu 2 bayttır. |
| "Örnekleme frekansını artırmak her zaman daha iyi ses verir." | 2 × f_max'ı geçtikten sonra o frekans bandı için yeni bilgi eklenmez; yalnızca veri miktarı artar. |

## 9. Arıza Giderme Yaklaşımı

| Belirti | Bu dosyaya göre olası neden | Nereye bak |
|---|---|---|
| Türkçe karakterler "ÅŸ" gibi bozuk görünüyor | Gönderen ve alan farklı karakter kodlaması kullanıyor | 06-02 |
| Kendi uygulaman bağlanamıyor; yakalamada beklenmedik bir port numarası var | Bayt sırası çevrilmemiş | Port numarasını onaltılık yaz ve baytları ters çevir |
| Ses kesik kesik geliyor; bağlantı hızı "yeterli" görünüyordu | Bant genişliği başlıklar hesaba katılmadan planlanmış | Bölüm 5'teki hesap, 03-21 |
| İkili bir dosya FTP ile aktarıldıktan sonra açılmıyor | FTP ASCII modunda satır sonlarını değiştirip dosyayı bozdu | 07-07 |

## 10. CCNA Bağlantısı

CCNA bayt sırası sormaz. Ama başlık alanlarının genişlikleri (VLAN kimliği 12 bit, port 16 bit, TTL 8 bit) sınavda doğrudan sorulur ve bu dosyadaki hesaptan gelir. Ses trafiğinin özellikleri (sabit ve küçük paketler, gecikmeye duyarlılık) v1.1 2.1'deki voice VLAN ve 4.7'deki QoS konularının temelidir.

## 11. Kendini Kontrol Et

1. 16 bitlik işaretsiz bir alan en fazla hangi değeri taşır? 12 bitlik VLAN kimliği alanıyla kaç VLAN kullanılabilir, neden?
   <details><summary>Cevap</summary>
   2¹⁶ − 1 = <b>65.535</b>. VLAN alanı 2¹² = 4096 değer taşır; 0 ve 4095 ayrılmış olduğu için <b>4094</b> VLAN (1–4094) kullanılabilir.
   </details>

2. `0x0A0B0C0D` değerini big-endian ve little-endian olarak bayt bayt yaz. Hangisi kabloda gönderilir?
   <details><summary>Cevap</summary>
   Big-endian: <code>0A 0B 0C 0D</code>. Little-endian: <code>0D 0C 0B 0A</code>. Kabloda ağ bayt sırası, yani big-endian gönderilir.
   </details>

3. Port 80 kabloda hangi iki baytla gider? Little-endian bir programcı `htons()` kullanmayı unutursa karşı taraf hangi portu görür?
   <details><summary>Cevap</summary>
   80 = 0x0050, kabloda <code>00 50</code>. Çevrilmezse bellekteki sıra (<code>50 00</code>) gider; karşı taraf 0x5000 = <b>20.480</b> görür.
   </details>

4. Tek kanallı bir ses 16.000 örnek/s ve örnek başına 16 bitle kaydediliyor. Bit hızı nedir? Bu kayıt en fazla hangi frekansı temsil edebilir?
   <details><summary>Cevap</summary>
   16.000 × 16 = <b>256 kbps</b>. Nyquist koşuluna göre 8 kHz'in altındaki frekansları temsil edebilir.
   </details>

5. `rapor.pdf` adlı bir dosyanın ilk baytları `89 50 4E 47 0D 0A 1A 0A`. Bu dosya gerçekte nedir? Bunu nasıl anladın?
   <details><summary>Cevap</summary>
   Bir <b>PNG görüntüsüdür</b>. Bu 8 bayt PNG imzasıdır; uzantı yalnızca bir addır. Bir PDF dosyası <code>%PDF-</code> ile başlardı.
   </details>

## 12. Uygulama

1. Bölüm 7'deki komutlarla bilgisayarındaki bir PNG ve bir PDF dosyasının imzasını bul.
2. Bölüm 4'teki tabloyu kâğıda kopyala, cevap sütunlarını kapat ve baytlardan yeniden doldur.
3. 10 eş zamanlı G.711 görüşmesinin Ethernet üzerinde kaç kbps gerektirdiğini hesapla.

## 13. Ustalık Kontrol Listesi

- [ ] Aynı baytların farklı yorumlarla farklı anlamlara geldiğini kendi seçtiğim bir örnekle gösterebiliyorum.
- [ ] Bir alanın bit genişliğinden değer aralığını hesaplayıp VLAN, port ve TTL sınırlarını açıklayabiliyorum.
- [ ] Çok baytlı bir değeri big-endian ve little-endian yazabiliyor, ağ bayt sırasının neden gerektiğini anlatabiliyorum.
- [ ] Ses için Nyquist koşulunu söyleyip G.711 ve sıkıştırılmamış video bit hızlarını hesaplayabiliyorum.
- [ ] Bir dosyanın türünün uzantıdan değil, imzadan ya da protokolün bildirdiği türden anlaşıldığını açıklayabiliyorum.

## Kaynaklar

- [RFC 791, Ek B] Data Transmission Order: oktetlerin iletim sırası (ağ bayt sırası).
- [PAPER-COHEN] D. Cohen, "On Holy Wars and a Plea for Peace", IEN 137 (1980): big-endian ve little-endian terimleri.
- [IEEE-8021Q] VLAN kimliği alanı ve ayrılmış değerler (0 ve 4095).
- [IEEE-8023] Oktet içindeki bitlerin iletim sırası.
- [ITU-G711] ITU-T G.711: 8.000 örnek/s, örnek başına 8 bit.
- [CISCO-PCM] Cisco, *Waveform Coding Techniques*: örnekleme öncesi süzme, PCM ve 64 kbps.
- [CISCO-VOIP-BW] Cisco, *Voice Over IP – Per Call Bandwidth Consumption* (belge 7934): G.711, 20 ms, 50 pps, Ethernet üzerinde 87,2 kbps.
- [STD-PNG §5.2] W3C, *Portable Network Graphics (PNG) Specification*: PNG imzası.
- [IANA-PROTO] IANA Protocol Numbers: 6 = TCP.
- [RFC 5737] IPv4 dokümantasyon adresleri (203.0.113.0/24).

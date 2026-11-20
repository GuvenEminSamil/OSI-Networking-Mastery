# 00-05 Transistörler ve Dijital Mantık (Transistors and Digital Logic)

> Önkoşullar: 00-03, 00-04 | Tahmini süre: ~2 saat | CCNA: dolaylı (Bölüm 7'deki Cisco bellek türleri ilk labdan itibaren kullanılır)

## Öğrenme Hedefleri

- Transistörün (MOSFET) gerilimle kontrol edilen bir anahtar olarak nasıl çalıştığını açıklamak.
- CMOS NOT ve NAND kapılarını transistörlerle çizmek; CMOS'un beklerken neden çok az güç harcadığını açıklamak.
- Mantık seviyelerinden (VIL, VIH, VOL, VOH) gürültü payını hesaplamak.
- Bir bitin SRAM, DRAM ve flash'ta nasıl saklandığını karşılaştırmak; saat sinyalinin (clock) neden gerektiğini söylemek.
- Bir Cisco cihazında RAM, NVRAM, flash ve ROM'un rolünü ve `copy running-config startup-config` komutunun neden gerektiğini açıklamak.

## 1. Sezgisel Giriş

Duvardaki ışık anahtarının iki durumu vardır ve bu iki durum bir biti temsil edebilir. Bir **transistör (transistor)** de bir anahtardır; farkı, onu parmağının değil **bir gerilimin** açıp kapatmasıdır. Hareketli parçası yoktur, saniyede milyarlarca kez durum değiştirebilir ve bir transistörün çıkışı başka bir transistörü kontrol edebilir. Bütün dijital mantık bu fikirden doğar.

Bu dosyanın sonunda şu sorunun cevabını bileceksin: Bir Cisco router'ı yapılandırıp kaydetmeden fişini çekersen yapılandırma neden kaybolur?

## 2. Neden Var?

00-01 bitin bir karar olduğunu, 00-03 bu kararlar üzerinde AND, OR, NOT ve XOR işlemlerini, 00-04 de gerilimi anlattı. Bu dosya üçünü birleştirir: Gerilimler nasıl mantık kararlarına dönüşür ve bitler nasıl hatırlanır?

Bu temel olmadan "switch MAC tablosunu donanımda arar", "tampon doldu, paketler düştü" ya da "kaydetmediğin yapılandırma yeniden başlatınca gider" gibi ifadeler ezber olarak kalır.

## 3. Mekanizma

### 3.1 Yarı iletken

Silisyum (silicon) bir **yarı iletkendir (semiconductor)**: İletkenliği, içine çok az miktarda başka element eklenerek (katkılama, doping) ve üzerine uygulanan gerilimle kontrol edilebilir. **[BASİTLEŞTİRME]** Yarı iletken fiziğine girmiyoruz; ağ mühendisi için gereken sonuç, gerilimle açılıp kapanan bir anahtar yapılabilmesidir.

### 3.2 MOSFET: gerilimle kontrol edilen anahtar

Bugünkü yongaların neredeyse tamamı **MOSFET (metal-oxide-semiconductor field-effect transistor)** kullanır. Bir MOSFET'in üç ucu vardır:

- **Kapı (gate):** Kontrol girişi.
- **Kaynak (source)** ve **akaç (drain):** Anahtarın iki ucu. Akım bu ikisi arasında akar.

Kapı, kanaldan çok ince bir yalıtkan oksit tabakasıyla ayrılmıştır. Bu yüzden kapıdan neredeyse hiç akım akmaz. Kapıdaki gerilim, bir **elektrik alanı (field)** oluşturarak altındaki kanalı açar ya da kapatır; adındaki "field-effect" buradan gelir.

İki tür MOSFET vardır ve birbirinin tersi gibi çalışır:

| Tür | Kapı gerilimi yüksekken (mantık 1) | Kapı gerilimi düşükken (mantık 0) |
|---|---|---|
| **nMOS** | İletir (anahtar kapalı) | İletmez (anahtar açık) |
| **pMOS** | İletmez | İletir |

nMOS'un iletime geçmesi için kapı geriliminin bir **eşik geriliminin (threshold voltage)** üzerine çıkması gerekir. Transistör arada da çalışabilir; ama 00-01'de gördüğün gibi dijital devreler onu yalnızca iki uçta, tam iletimde ya da tam kesimde kullanır. Kapı akım çekmediği için bir kapının çıkışı başka birçok kapının girişini zorlanmadan sürebilir (**fan-out**).

### 3.3 CMOS NOT kapısı

**CMOS (complementary MOS)**, bir pMOS ile bir nMOS'u birbirini tamamlayacak şekilde kullanır. En basit örnek NOT kapısıdır, yani **evirici (inverter)**:

```
              VDD (besleme, mantık 1)
               │
             ┌─┴─┐
   A ──┬─────┤ P │   pMOS: A = 0 iken iletir
       │     └─┬─┘
       │       ├────────── Y (çıkış)
       │     ┌─┴─┐
       └─────┤ N │   nMOS: A = 1 iken iletir
             └─┬─┘
               │
              GND (toprak, mantık 0)
```

*Ne görüyoruz:* İki transistör, besleme (VDD) ile toprak arasında seri bağlıdır; ikisinin kapısı da aynı A girişine bağlıdır. Çıkış Y, ikisinin ortasından alınır.

- **A = 0:** pMOS iletir, nMOS iletmez. Y, VDD'ye bağlanır: **Y = 1**.
- **A = 1:** nMOS iletir, pMOS iletmez. Y, toprağa bağlanır: **Y = 0**.

Bu, 00-03'teki NOT işleminin doğruluk tablosunun ta kendisidir.

İki önemli sonuç:

1. **Beklerken neredeyse güç harcamaz.** Kararlı durumda transistörlerden biri her zaman kapalıdır; VDD'den toprağa doğrudan akım yolu yoktur. Güç esas olarak **durum değişirken** harcanır (Bölüm 4.2).
2. **Her kapı sinyali yeniler.** Giriş biraz gürültülü olsa da eşik aşıldığı sürece çıkış tam olarak VDD'ye ya da toprağa çekilir. Her kapı, 00-01'deki yenileme (regeneration) işini küçük ölçekte yapar; bu yüzden milyarlarca kapıdan geçen bir bit bozulmaz.

### 3.4 NAND, NOR ve diğer kapılar

İki girişli bir **NAND** kapısı dört transistörle kurulur:

```
       VDD ──┬────────────┐
           ┌─┴──┐       ┌─┴──┐
     A ────┤ P  │  B ───┤ P  │     iki pMOS paralel: biri iletirse Y = 1
           └─┬──┘       └─┬──┘
             └─────┬──────┘
                   ├─────────── Y
                 ┌─┴──┐
           A ────┤ N  │            iki nMOS seri: ikisi de iletirse Y = 0
                 └─┬──┘
                 ┌─┴──┐
           B ────┤ N  │
                 └─┬──┘
                  GND
```

*Ne görüyoruz:* Çıkışı toprağa bağlayan yol, iki nMOS'un **ikisinin birden** iletmesini gerektirir; bu ancak A = 1 ve B = 1 iken olur. Diğer bütün durumlarda paralel pMOS'lardan en az biri iletir ve Y = 1 olur. Bu, NAND'ın doğruluk tablosudur.

CMOS'ta tersleyen kapılar (NOT, NAND, NOR) doğaldır. AND elde etmek için NAND'ın arkasına bir NOT eklenir:

| Kapı | Transistör sayısı (statik CMOS) |
|---|---|
| NOT | 2 |
| NAND, NOR | 4 |
| AND, OR | 6 (NAND/NOR + NOT) |

NAND'ın evrensel olması (00-03) ve en az transistörle kurulması, onu yonga tasarımının temel yapı taşı yapar.

### 3.5 Mantık seviyeleri ve eşikler

Gerçek bir devrede "1" ve "0" tek bir gerilim değeri değil, birer **aralıktır**. Bir mantık ailesinin veri sayfası dört değer verir:

| Değer | Anlamı |
|---|---|
| **VOH** | Çıkışın "1" verirken garanti ettiği en düşük gerilim |
| **VOL** | Çıkışın "0" verirken garanti ettiği en yüksek gerilim |
| **VIH** | Girişin "1" olarak kabul ettiği en düşük gerilim |
| **VIL** | Girişin "0" olarak kabul ettiği en yüksek gerilim |

Klasik 5 V TTL uyumlu seviyeler örneğinde [STD-TI-LOGIC]:

```
 Gerilim
  5,0 V ┤
        │   çıkış "1" ise gerilim bu bölgededir
  2,4 V ┤ ─────────────────────────────────────── VOH
        │   ↕ NMH = VOH − VIH = 0,4 V
  2,0 V ┤ ─────────────────────────────────────── VIH  (giriş bunu ve üstünü "1" sayar)
        │   tanımsız bölge: alıcı hiçbir şey garanti etmez
  0,8 V ┤ ─────────────────────────────────────── VIL  (giriş bunu ve altını "0" sayar)
        │   ↕ NML = VIL − VOL = 0,4 V
  0,4 V ┤ ─────────────────────────────────────── VOL
        │   çıkış "0" ise gerilim bu bölgededir
  0 V   ┤
```

*Ne görüyoruz:* Gönderici, alıcının beklediğinden daha "temiz" bir sinyal üretmeyi garanti eder. Aradaki fark **gürültü payıdır (noise margin)**. Bu örnekte iki seviye için de 0,4 V'tur. Yolda eklenen gürültü 0,4 V'u aşmadıkça alıcı doğru karar verir. Bu, 00-01'deki gürültü payı fikrinin veri sayfasındaki karşılığıdır.

Modern işlemci çekirdekleri yaklaşık 1 V ile çalışır (nedeni Bölüm 4.2'de); bedeli, gürültü paylarının da küçülmesidir.

### 3.6 Bir biti hatırlamak: geri besleme

Şimdiye kadarki kapılar **kombinasyonel (combinational)** devrelerdir: Çıkış yalnızca o anki girişlere bağlıdır. Giriş değişince çıkış da değişir; devre geçmişi hatırlamaz.

Hatırlamak için **geri besleme (feedback)** gerekir. İki eviriciyi bir halka şeklinde birbirine bağla:

```
     ┌──────[NOT]──────┐
     │                 │
     Q                 Q̄
     │                 │
     └──────[NOT]──────┘
```

*Ne görüyoruz:* Q = 1 ise eviricilerden biri Q̄ = 0 üretir; diğeri bu 0'ı yeniden 1'e çevirip Q'ya geri verir. Halka kendi durumunu destekler; Q = 0 durumu da aynı şekilde kararlıdır.

İki kararlı durumu olan (bistable) bu devre, elektrik verildiği sürece bir biti saklar. Durumu değiştirmek için giriş eklenir: İki NOR kapısının çapraz bağlanmasıyla **SR latch** (set/reset) kurulur. **D flip-flop** ise D girişindeki değeri yalnızca **saat sinyalinin kenarında** yakalar ve sonraki kenara kadar tutar. İşlemci yazmaçları (register) ve bir NIC'in bitleri sırayla gönderip aldığı kaydırmalı yazmaçlar (shift register) flip-flop'lardan oluşur.

### 3.7 Saat sinyali (clock)

Kapıların çıkışları anında değişmez; her kapının küçük bir **yayılma gecikmesi (propagation delay)** vardır. Bir hesaplama birçok kapıdan geçtiği için sonuçlar farklı anlarda hazır olur. Ara değerler "yarış" hâlindeyken bir flip-flop'un sonucu yakalaması hatalı olur.

Çözüm, bütün flip-flop'lara aynı anda "şimdi yakala" diyen periyodik bir kare dalgadır: **saat sinyali (clock)**. İki saat kenarı arasında kombinasyonel mantık sonuçlanır; kenar geldiğinde sonuç flip-flop'lara yazılır. Saat periyodu, en uzun kapı zincirinin (kritik yol, critical path) gecikmesinden uzun olmalıdır. **[BASİTLEŞTİRME]** Kritik yolda her biri 50 ps (pikosaniye) gecikmeli 20 kapı varsa yol 1 ns sürer; saat en fazla yaklaşık 1 / 1 ns = **1 GHz** olabilir (tel gecikmeleri ihmal edildi).

Saat sinyali genellikle bir **kuvars kristal osilatörden (crystal oscillator)** gelir. Ağdaki önemli sonucu şudur: **Bir kablonun iki ucundaki cihazların saatleri ayrıdır** ve hiçbir zaman tam olarak aynı frekansta çalışmaz. Alıcı, göndericinin saatini sinyalin içinden geri kurmak zorundadır. Ethernet çerçevesinin başındaki preamble bu yüzden vardır (01-04, 02-03).

### 3.8 Bellek türleri: SRAM, DRAM ve flash

| Tür | Bir bit nasıl saklanır? | Elektrik kesilince | Hız ve yoğunluk | Ağ cihazındaki tipik kullanım |
|---|---|---|---|---|
| **SRAM** | Bölüm 3.6'daki iki evirici + iki erişim transistörü (6 transistör) | **Silinir** | Çok hızlı; bit başına pahalı, az yoğun | İşlemci önbellekleri; switch ASIC'indeki tablolar |
| **DRAM** | Bir transistör + bir **kapasitör (capacitor)**; kapasitör doluysa 1 | **Silinir** | SRAM'den yavaş; çok yoğun ve ucuz | Ana bellek; router'ın RAM'i, paket tamponları, running-config |
| **Flash** | Yalıtılmış bir kapıda hapsedilmiş yük | **Kalır** | Okuma hızlı, yazma yavaş; yazma sayısı sınırlı | SSD'ler; Cisco'da `flash:` (IOS imajı) |
| **ROM** | Üretimde sabitlenmiş | Kalır | — | Açılış programı (bootstrap) |

DRAM'in kapasitörü zamanla yük kaybeder (sızıntı). Bu yüzden bellek denetleyicisi her hücreyi periyodik olarak okuyup yeniden yazar; buna **yenileme (refresh)** denir. DDR4'te her hücre en geç 64 ms'de bir yenilenir; sıcaklık yüksekse daha sık [STD-JEDEC-DDR4, SEC-DRAM]. "Dinamik" adı buradan gelir: Hücre, sürekli bakım gerektirir. SRAM'de ise halka kendi durumunu korur; buna "statik" denir.

Ortak ders: **SRAM ve DRAM elektrik kesilince silinir**; kalıcılık için flash gibi uçucu olmayan (non-volatile) bellek gerekir.

## 4. Teknik Ayrıntı

### 4.1 Bir switch'in içinde neler var?

Bu dosyadaki kavramların bir ağ cihazındaki karşılıkları:

| Bileşen | Ne yapar? | Dayandığı kavram | Ayrıntı |
|---|---|---|---|
| PHY yongası | Bitleri kablodaki sinyale çevirir ve geri alır | Mantık seviyeleri, saat kurtarma | 01-01, 01-04 |
| ASIC (application-specific integrated circuit) | Çerçeveleri ve paketleri donanımda, kapı düzeyinde iletir (**veri düzlemi**) | Kombinasyonel mantık, flip-flop'lar | 02-06, 03-07 |
| TCAM ve SRAM tabloları | MAC tablosu, ACL ve rota aramaları | Bellek hücreleri, paralel karşılaştırma | 02-06, 14-03 |
| CPU | Yönetim, protokol işlemleri (**kontrol düzlemi**) | Saat, yazmaçlar | 00-07, 15-04 |
| DRAM | Paket tamponları, running-config, yönlendirme ve ARP tabloları | Uçucu bellek | Bölüm 7 |
| Flash | İşletim sistemi imajı, kalıcı dosyalar | Uçucu olmayan bellek | Bölüm 7, 07-07 |

> **[DERİN]** **TCAM (ternary content-addressable memory)** ters çalışan bir bellektir: Ona bir veri verirsin, o da eşleşen kaydı **bütün kayıtlarda aynı anda** arayıp tek adımda bulur. Her bit 0, 1 ya da "önemsiz" (X) olabildiği için "192.168.10.0/24" gibi bir önek tek kayıtla temsil edilir; bu, 00-03'teki maskelemenin donanımdaki karşılığıdır. Her hücrede karşılaştırma devresi olduğu için TCAM pahalıdır ve çok güç harcar; switch'lerdeki ACL ve rota kapasitesinin sınırlı olmasının bir nedeni budur (02-06).

### 4.2 [DERİN] CMOS neden ısınır?

Her kapı çıkışı, sürdüğü girişler ve tellerle birlikte küçük bir kapasitans oluşturur (00-04, Bölüm 4.2). Her geçişte bu kapasitans dolar ya da boşalır. Harcanan **dinamik güç (dynamic power)** yaklaşık olarak P ≈ α × C × V² × f'dir (α: durum değiştiren kapıların oranı, C: kapasitans, V: besleme gerilimi, f: saat frekansı). Gerilimi yarıya indirmek gücü dörtte bire indirir; çekirdek gerilimlerinin 5 V'tan 1 V civarına inmesinin nedeni budur. Trafik ve frekans arttıkça güç doğrusal olarak artar; yoğun trafik altındaki bir switch ASIC'i daha çok ısınır.

## 5. Gerçek Dünya Örnekleri

- **Kaydedilmemiş yapılandırma:** Bir stajyer, sabah boyunca bir router'ı yapılandırıyor ve her şey çalışıyor. Öğleden sonra bir elektrik kesintisinden sonra router fabrika ayarına yakın bir yapılandırmayla açılıyor. Neden: Yaptığı değişiklikler RAM'deki running-config'teydi ve `copy running-config startup-config` ile kalıcı belleğe yazılmamıştı.
- **Veri merkezi switch'i:** Veri sayfasındaki "MAC tablosu kapasitesi" ve "paket tamponu" değerleri, bu dosyadaki bellek türlerinin fiziksel sınırlarıdır. Tampon dolduğunda yeni gelen paketler düşürülür (00-07, 03-21).
- **Ev router'ı:** Havalandırması kapanmış bir modemin aşırı ısınması ya da yaşlanmış bir güç kaynağı, "her akşam kendi kendine yeniden başlıyor" türünden zor teşhis edilen arızalara yol açar. Sıcaklık arttıkça transistörlerin davranışı ve DRAM hücrelerinin yük tutma süresi kötüleşir.

## 6. Diğer Konularla Bağlantı

| Bu dosyadaki fikir | Nerede kullanılıyor |
|---|---|
| Gürültü payı ve mantık seviyeleri | 00-01, 01-04 |
| İki ucun saatlerinin ayrı olması | 01-03, 01-04, 02-03 (preamble) |
| ASIC, CAM, TCAM | 02-06, 03-07 |
| Bellek türleri ve tamponlar | 00-07, 03-21 (kuyruklama) |
| Kontrol ve veri düzlemi | 03-01, 15-04 |
| Yapılandırmanın kaydedilmesi (pratik) | LAB-006 |
| IOS imajı ve yapılandırma dosyalarının yönetimi | 07-07 |

## 7. Cisco ve Pratik

**[CISCO-ÖZEL]** Cisco router ve switch'lerinde dört bellek türü bulunur [CISCO-NETACAD]:

| Bellek | İçeriği | Elektrik kesilince |
|---|---|---|
| **ROM** | POST (açılış donanım testi), bootstrap, ROMMON | Kalır |
| **Flash** | IOS imajı (ör. `flash:` içindeki `.bin` dosyası) | Kalır |
| **NVRAM** | **startup-config**: Cihaz açılırken yüklenen yapılandırma | Kalır |
| **RAM (DRAM)** | Çalışan IOS, **running-config**, yönlendirme ve ARP tabloları, paket tamponları | **Silinir** |

`configure terminal` ile yaptığın her değişiklik anında running-config'e, yani RAM'e yazılır. Kalıcı olması için kopyalaman gerekir:

```
Router# copy running-config startup-config
Destination filename [startup-config]?        ← Enter'a bas
Building configuration...
[OK]
```

Doğrulama:

```
Router# show running-config        ! RAM'de çalışan yapılandırma
Router# show startup-config        ! NVRAM'de kayıtlı yapılandırma
Router# show version               ! IOS sürümü, bellek miktarları, açılış nedeni
Router# show flash:                ! Flash'taki dosyalar
```

Bu komutlar Packet Tracer'da desteklenir (✅). `write memory` (kısaca `wr`) eski ama hâlâ çalışan bir eşdeğerdir.

**[CISCO-ÖZEL]** Catalyst 2960 gibi switch'lerde startup-config, flash'ta `config.text` adlı bir dosya olarak tutulur; VLAN veritabanı da flash'taki `vlan.dat` dosyasındadır. Bu yüzden bir switch'i tamamen sıfırlamak için `erase startup-config` yetmez; `vlan.dat` dosyasının da silinmesi gerekir (02-08).

## 8. Yaygın Yanılgılar

| Yanılgı | Doğrusu |
|---|---|
| "Bilgisayar beklerken de çalışırken kadar güç harcar." | CMOS kapılar kararlı durumda neredeyse hiç güç harcamaz. Güç esas olarak durum değişimlerinde harcanır; bu yüzden yük ve frekans arttıkça tüketim artar. |
| "RAM'deki bilgi, bilgisayar kapanınca diske kaydedilir." | RAM uçucudur; kaydetmediğin her şey elektrik kesildiği anda gider. Cisco'da running-config'i startup-config'e kopyalamadıkça değişiklikler kalıcı olmaz. |
| "1 her zaman 5 V'tur, 0 her zaman 0 V'tur." | 1 ve 0 birer gerilim **aralığıdır**; aralarında tanımsız bir bölge vardır. Değerler mantık ailesine göre değişir. |
| "Bir kablonun iki ucundaki cihazlar aynı saatle çalışır." | Her cihazın kendi osilatörü vardır. Alıcı, göndericinin saatini sinyalden geri kurar (01-04). |

## 9. Arıza Giderme Yaklaşımı

| Belirti | Bu dosyaya göre olası neden | İlk kontrol |
|---|---|---|
| Cihaz yeniden başladıktan sonra yapılandırma eski hâline döndü | running-config kaydedilmemişti | `show startup-config` ile karşılaştır |
| Cihaz açılmıyor, ROMMON istemine düşüyor | Flash'ta geçerli bir IOS imajı bulunamadı | `show flash:` (ya da ROMMON'da `dir flash:`) |
| Yoğun trafikte paket kayıpları var, kablo hatası yok | Tamponlar doluyor (bellek sınırı) | `show interfaces` çıktısındaki drop ve buffer sayaçları (00-07, Bölüm 7) |

## 10. CCNA Bağlantısı

CCNA transistör ya da kapı sorusu sormaz. Ama running-config ile startup-config farkı ve `copy running-config startup-config` her lab sorusunun parçasıdır; 03-07'deki donanım iletimi (ASIC, TCAM) de bu dosyaya dayanır.

## 11. Kendini Kontrol Et

1. Bir nMOS ile bir pMOS'un kapısına aynı anda mantık 1 uygulanırsa her biri ne yapar?
   <details><summary>Cevap</summary>
   nMOS iletir (anahtar kapalı), pMOS iletmez (anahtar açık). İkisi her zaman birbirinin tersini yapar; CMOS'taki "tamamlayıcı" (complementary) sözcüğü buradan gelir.
   </details>

2. CMOS bir evirici neden kararlı durumdayken neredeyse hiç güç harcamaz?
   <details><summary>Cevap</summary>
   Her iki kararlı durumda da iki transistörden biri kapalıdır. Bu yüzden beslemeden toprağa doğrudan bir akım yolu yoktur. Güç esas olarak çıkış durum değiştirirken, yük kapasitansı dolup boşalırken harcanır (Bölüm 4.2).
   </details>

3. Bir mantık ailesinde VOH = 2,7 V, VIH = 2,0 V, VIL = 0,8 V ve VOL = 0,5 V'tur. İki seviye için gürültü payları nedir? Hangi seviye gürültüye daha dayanıklıdır?
   <details><summary>Cevap</summary>
   NMH = VOH − VIH = 2,7 − 2,0 = <b>0,7 V</b>. NML = VIL − VOL = 0,8 − 0,5 = <b>0,3 V</b>. Yüksek seviye (1) daha dayanıklıdır; düşük seviyeye 0,3 V'tan fazla gürültü eklenirse alıcı tanımsız bölgeye girer.
   </details>

4. SRAM ve DRAM'in ikisi de uçucudur. DRAM'in ayrıca "yenileme" gerektirmesinin nedeni nedir?
   <details><summary>Cevap</summary>
   DRAM biti bir kapasitördeki yük olarak saklar ve bu yük zamanla sızar. Bu yüzden her hücre periyodik olarak okunup yeniden yazılmalıdır (DDR4'te en geç 64 ms'de bir). SRAM'de bit, kendini besleyen iki evirici halkasıyla tutulur; elektrik olduğu sürece yenileme gerekmez.
   </details>

5. Bir router'da `hostname R1` yazdın ve router'ı kaydetmeden yeniden başlattın. Açıldığında istem neden yine `Router>` olur?
   <details><summary>Cevap</summary>
   Değişiklik yalnızca RAM'deki running-config'e yazıldı. Router açılırken NVRAM'deki startup-config'i yükler; orada `hostname R1` yoktur. Kalıcı olması için önce <code>copy running-config startup-config</code> gerekir.
   </details>

## 12. Uygulama

Packet Tracer'da bir router ekle (ör. 2911) ve CLI sekmesini aç (yapılandırmayı kaydetmeyi LAB-006'da ayrıntılı çalışacaksın):

1. `show version` çıktısında IOS imajının adını ve bellek miktarlarını bul. `show flash:` ile imaj dosyasının flash'ta durduğunu doğrula.
2. `enable` → `configure terminal` → `hostname TEST` yaz, `end` ile çık.
3. `show running-config` ve `show startup-config` çıktılarını karşılaştır. Hostname hangisinde var?
4. `reload` ile yeniden başlat (kaydetme sorusuna `no` de). Açıldığında hostname ne oldu?
5. Adım 2'yi tekrarla, bu kez `copy running-config startup-config` ile kaydet ve yeniden başlat.

Her adımdan önce sonucu tahmin et.

## 13. Ustalık Kontrol Listesi

- [ ] nMOS ve pMOS'un gerilime göre davranışını ve CMOS eviricinin çalışmasını kaynağa bakmadan çizerek anlatabiliyorum.
- [ ] VOH, VOL, VIH ve VIL değerlerinden iki gürültü payını hesaplayabiliyorum.
- [ ] Bir bitin flip-flop (SRAM), kapasitör (DRAM) ve flash hücresinde nasıl saklandığını ve hangisinin elektrik kesilince kaybolduğunu söyleyebiliyorum.
- [ ] Saat sinyalinin neden gerektiğini ve iki cihazın saatlerinin neden ayrı olduğunu açıklayabiliyorum.
- [ ] Cisco'daki ROM, flash, NVRAM ve RAM'in içeriklerini sayabiliyor ve running-config'in neden kaydedilmesi gerektiğini anlatabiliyorum.

## Kaynaklar

- [STD-TI-LOGIC] Texas Instruments, *Logic Guide* (SDYU001): 5 V TTL ve 3,3 V LVTTL mantık seviyeleri (VIH 2,0 V, VIL 0,8 V, VOH 2,4 V, VOL 0,4 V).
- [STD-JEDEC-DDR4] JEDEC JESD79-4 (DDR4): 64 ms yenileme penceresi. Birincil metin okunmadı; değer [SEC-DRAM] ile çapraz kontrol edildi.
- [CISCO-NETACAD] Cisco Networking Academy CCNA materyali: router bellek türleri (RAM, ROM, NVRAM, flash).
- [TXT-HARRIS] Digital Design and Computer Architecture: CMOS kapılar, flip-flop'lar, bellek dizileri (ek okuma).
- [TXT-PETZOLD] Code, 2. baskı: anahtarlardan kapılara ve belleğe sezgisel yol (ek okuma).

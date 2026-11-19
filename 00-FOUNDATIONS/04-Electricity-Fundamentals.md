# 00-04 Elektrik Temelleri (Electricity Fundamentals)

> Önkoşullar: — (00-01 yardımcı olur) | Tahmini süre: ~2 saat | CCNA: dolaylı (v1.1 1.1.h PoE, 1.3, 1.4'ün altyapısı)

## Öğrenme Hedefleri

- Gerilim (voltage), akım (current) ve direnç (resistance) kavramlarını ve aralarındaki ilişkiyi (Ohm yasası) açıklamak.
- Bir devrenin neden kapalı bir döngü gerektirdiğini ve gerilimin neden her zaman iki nokta arasında ölçüldüğünü açıklamak.
- Elektronların yavaş hareket ettiği hâlde sinyalin neden çok hızlı yayıldığını açıklamak.
- PoE'nin neden yaklaşık 48 V gibi görece yüksek bir gerilim kullandığını güç kaybı hesabıyla göstermek.
- Gürültünün (noise) elektriksel kökenini ve diferansiyel sinyalin temel fikrini tanımlamak.

## 1. Sezgisel Giriş

Bir Ethernet kablosunu bilgisayarına taktığında iki cihaz arasında bir **elektrik devresi** kurulur. Gönderici, bir çift telin arasındaki gerilimi çok hızlı bir şekilde değiştirir; alıcı bu değişimleri ölçer ve bitlere çevirir. PoE kullanan bir IP telefonda aynı kablo, veriyle birlikte telefonun çalışması için gereken gücü de taşır.

Bunların nasıl mümkün olduğunu ve kablonun neden en fazla 100 metre olabildiğini anlamak için üç büyüklüğü tanıman yeterli: gerilim, akım ve direnç. Bu dosya derin bir elektronik dersi değildir; yalnızca ağ konularını anlamak için gerekeni verir.

## 2. Neden Var?

Fiziksel katman (01-*) bitleri elektriksel, optik ya da radyo sinyalleriyle taşır. Bakır kablolar, PoE, gürültü, zayıflama, karışma ve kablo uzunluğu sınırı gibi konuların hepsi elektriğin temel davranışlarından doğar. Bu temeller olmadan "kabloyu kısalt" ya da "kabloyu güç hattından uzaklaştır" gibi önerileri yalnızca ezberleyebilirsin; neden işe yaradıklarını açıklayamazsın.

## 3. Mekanizma

### 3.1 Yük, iletken ve yalıtkan

Madde atomlardan, atomlar da artı yüklü bir çekirdek ve çevresindeki eksi yüklü elektronlardan oluşur. Elektrik yükünün birimi **coulomb (C)**'dur; tek bir elektronun yükü yaklaşık 1,6 × 10⁻¹⁹ C'dur.

- **İletken (conductor):** Bakır gibi metallerde atomların en dıştaki elektronlarının bir kısmı serbestçe hareket edebilir. Bu yüzden yük kolayca akar.
- **Yalıtkan (insulator):** Plastik, cam ve hava gibi maddelerde elektronlar atomlarına sıkıca bağlıdır; yük neredeyse hiç akmaz.

Bir Ethernet kablosu bu ikisinin birleşimidir: Bakır teller sinyali iletir, plastik kılıf telleri birbirinden ve dış dünyadan yalıtır.

### 3.2 Gerilim: itme kuvveti

**Gerilim (voltage, V)**, iki nokta arasındaki elektriksel potansiyel farkıdır. Bir yükü bir noktadan diğerine götürmek için birim yük başına ne kadar enerji gerektiğini söyler. Birimi **volt (V)**'tur: 1 V = 1 joule/coulomb.

Sezgisel bir benzetme olarak su borularını düşün: Gerilim, suyu iten **basınç farkı** gibidir. Basınç farkı yoksa su akmaz.

Bu benzetmenin en önemli dersi şudur: **Gerilim her zaman iki nokta arasında ölçülür.** "Bu telde 5 V var" cümlesi, aslında "bu tel ile referans noktası arasında 5 V fark var" demektir. Bu referansa genellikle **toprak (ground)** ya da devrenin ortak noktası denir. Bu fikir, Ethernet'in diferansiyel sinyalini anlamanın anahtarıdır (Bölüm 3.6).

### 3.3 Akım: yük akışı

**Akım (current, I)**, bir noktadan birim zamanda geçen yük miktarıdır. Birimi **amper (A)**'dir: 1 A = saniyede 1 coulomb. Su benzetmesinde akım, borudan saniyede geçen su miktarıdır.

Akımın akabilmesi için **kapalı bir döngü (closed circuit)** gerekir: Yük kaynaktan çıkar, yükü (lamba, alıcı devresi) geçer ve kaynağa geri döner. Döngü bir yerden koparsa akım durur. Bu yüzden her elektriksel sinyalin bir "gidiş" ve bir "dönüş" yolu vardır. Ethernet'te bu, bir çift içindeki iki teldir.

### 3.4 Direnç ve Ohm yasası

**Direnç (resistance, R)**, bir maddenin akıma karşı gösterdiği zorluktur. Birimi **ohm (Ω)**'dur. Su benzetmesinde direnç borunun darlığıdır.

Bu üç büyüklük **Ohm yasasıyla (Ohm's law)** bağlıdır:

> V = I × R

Aynı gerilimde direnç artarsa akım azalır. Aynı akımı geçirmek için direnç arttıkça daha fazla gerilim gerekir.

Bir telin direnci üç şeye bağlıdır:

- **Malzeme:** Bakırın direnci düşüktür.
- **Uzunluk:** Tel uzadıkça direnç **doğru orantılı** olarak artar.
- **Kesit:** Tel inceldikçe direnç artar.

Ağdaki sonucu: Uzun ve ince bir kablo daha fazla direnç gösterir ve sinyalin bir kısmı yolda ısıya dönüşür. Sinyal zayıflar. Bu, Ethernet'in kablo uzunluğu sınırının nedenlerinden biridir (diğer nedenler 01-05 ve 01-06'da).

### 3.5 Güç

**Güç (power, P)**, birim zamanda aktarılan enerjidir. Birimi **watt (W)**'tır.

> P = V × I ve Ohm yasasıyla birleştirince P = I² × R

İkinci biçim çok önemlidir: **Bir telde ısıya dönüşen güç, akımın karesiyle artar.** Akımı ikiye katlarsan kayıp dört katına çıkar.

### 3.6 Gürültü ve diferansiyel sinyal

Değişen bir manyetik alan, yakınındaki bir telde gerilim oluşturur (indüklenme). Bu yüzden elektrik motorları, floresan lambalar ve güç kabloları gibi kaynaklar yakındaki veri kablolarına istenmeyen gerilimler ekler. Bu istenmeyen gerilimlere **gürültü (noise)**, kaynağına da **elektromanyetik girişim (EMI, electromagnetic interference)** denir.

Gürültü, 00-01'deki gürültü payını tüketir. Gürültü karar eşiğini aşarsa alıcı yanlış bit okur.

Ethernet'in bakır kablolarda kullandığı çözüm **diferansiyel sinyaldir (differential signaling)**: Bilgi tek bir telin toprağa göre gerilimiyle değil, **bir çiftteki iki tel arasındaki gerilim farkıyla** taşınır. Gönderici bir telin gerilimini yükseltirken diğerininkini düşürür. Alıcı iki teli birbirinden çıkarır:

```
 Tel A:  sinyal + gürültü
 Tel B: −sinyal + gürültü        (iki tel yan yana olduğu için gürültüyü neredeyse eşit alır)
 ─────────────────────────
 A − B:  2 × sinyal              (gürültü birbirini götürür)
```

İki telin gürültüyü **eşit** alması gerekir. Bükümlü çiftteki büküm (twist) bunu sağlar. Ayrıntılar 01-06'da.

### 3.7 Elektronlar yavaş, sinyal hızlı

Yaygın bir yanılgı, kabloda elektronların ışık hızıyla aktığıdır. Gerçekte bir bakır teldeki elektronların ortalama ilerleme hızı (sürüklenme hızı, drift velocity) çok düşüktür: Tipik akımlarda saniyede milimetreler mertebesinde ya da daha yavaştır.

Hızlı olan, **sinyalin kendisidir**: Gerilimdeki bir değişim kablo boyunca bir elektromanyetik dalga olarak yayılır. Bu dalga, bir boruyu baştan sona dolduran suyu bir uçtan ittiğinde diğer uçta suyun neredeyse aynı anda çıkmasına benzer. Su moleküllerinin kendisi o kadar hızlı gitmez. Ağ kablolarında sinyal ışık hızının yaklaşık üçte ikisiyle yayılır; bu da metre başına yaklaşık 5 nanosaniye eder. 100 metrelik bir kabloda yayılma gecikmesi yaklaşık 0,5 mikrosaniyedir.

### 3.8 DC ve AC

- **Doğru akım (DC, direct current):** Akım hep aynı yönde akar. Pil, adaptör çıkışı ve PoE gücü DC'dir.
- **Alternatif akım (AC, alternating current):** Akımın yönü periyodik olarak değişir. Şebeke elektriği AC'dir; Türkiye'de ve Rusya'da frekansı 50 Hz'dir, yani saniyede 50 tam döngü.

Veri sinyalleri de sürekli değişen gerilimlerdir; ama frekansları çok daha yüksektir (megahertz mertebesi). Sinyallerin frekans açısından incelenmesi 01-02'nin konusudur.

## 4. Teknik Ayrıntı

### 4.1 PoE neden yaklaşık 48 V kullanır?

**PoE (Power over Ethernet)**, IP telefon, kablosuz erişim noktası ve kamera gibi cihazlara veri kablosu üzerinden DC güç verir. IEEE 802.3 standardında tanımlıdır [IEEE-8023]:

| Standart | Ticari adı | Güç kaynağı tarafında en fazla (PSE) | Kaynak tarafındaki gerilim |
|---|---|---|---|
| 802.3af (Type 1) | PoE | 15,4 W | 44–57 V |
| 802.3at (Type 2) | PoE+ | 30 W | 50–57 V |
| 802.3bt (Type 3 / Type 4) | PoE++ | 60 W / 90 W | — (bt ayrıntıları 01-06'da) |

Cihaz tarafına ulaşan güç, kablodaki kayıp nedeniyle daha düşüktür.

Neden 5 V ya da 12 V değil? Bölüm 3.5'teki P = I² × R formülü cevabı verir. Aşağıdaki hesap **[BASİTLEŞTİRME]** içerir: Kablonun toplam döngü direncini 12,5 Ω kabul ediyoruz ve gerilimin kablo boyunca sabit kaldığını varsayıyoruz.

| Gerilim | 15,4 W için gereken akım (I = P / V) | Kablodaki kayıp (I² × R) |
|---|---|---|
| 48 V | 0,32 A | 0,32² × 12,5 ≈ **1,3 W** |
| 12 V | 1,28 A | 1,28² × 12,5 ≈ **20,5 W** |

12 V'ta kablo, cihaza iletmek istediğinden daha fazla gücü ısıya çevirir; bu pratikte imkânsızdır. Gerilimi artırmak aynı gücü daha düşük akımla taşımayı, dolayısıyla kaybı karesel olarak azaltmayı sağlar. Elektrik şebekelerinin uzun mesafede yüksek gerilim kullanmasının nedeni de budur. 48 V civarı, güvenlik açısından düşük gerilim sınıfında kalırken kaybı kabul edilebilir düzeyde tutan bir orta noktadır.

> **[DERİN]** Ethernet portları, kablo ile cihazın devresi arasında küçük **izolasyon transformatörleri (magnetics)** kullanır. Transformatör değişen sinyalleri (veri) geçirir, sabit DC gerilimi geçirmez. Böylece iki cihazın toprakları arasındaki farklar devreye zarar vermez. PoE, DC gücü transformatörlerin orta uçlarından (center tap) bir çiftin iki teline eşit olarak verir. Bu güç, çiftin iki teli arasında bir fark oluşturmadığı için diferansiyel veri sinyalini bozmaz.

### 4.2 [DERİN] Kapasitans, endüktans ve empedans

Bu kavramlar sinyalin neden "bozulduğunu" anlamak için gereklidir; ayrıntılar 01-05'te.

- **Kapasitans (capacitance, C):** İki iletken arasında yük depolama yeteneğidir. Bir çiftin iki teli de küçük bir kapasitör gibi davranır. Gerilimi değiştirmek için önce bu kapasitörün dolması ya da boşalması gerekir. Bu süreyi R × C (zaman sabiti) belirler. Kablo uzadıkça kapasitans artar, gerilim değişimleri yuvarlanır. Sonuç olarak bitler birbirine karışmaya başlar ve hızlı sinyaller zorlaşır.
- **Endüktans (inductance, L):** Akımdaki değişime karşı koyma eğilimidir. Değişen akım bir manyetik alan oluşturur; bu alan da değişime karşı bir gerilim üretir.
- **Empedans (impedance, Z):** Değişen sinyallere karşı toplam "zorluk"tur. Direnci ve kapasitans ile endüktansın frekansa bağlı etkilerini birlikte içerir. Bir iletim hattının **karakteristik empedansı (characteristic impedance)**, sinyalin hat boyunca "gördüğü" empedanstır. Ethernet bükümlü çiftleri 100 Ω, kablo TV koaksiyelleri 75 Ω, eski koaksiyel Ethernet kabloları 50 Ω'dur. Hattın bir noktasında empedans değişirse (kötü bir konnektör, ezilmiş kablo) sinyalin bir kısmı geri yansır. Bu yansıma, kablo test cihazlarının arızanın yerini nasıl bulduğunu da açıklar (01-05).

## 5. Gerçek Dünya Örnekleri

- **Ofiste PoE:** Bir Cisco switch, tavandaki kablosuz erişim noktasına ve masalardaki IP telefonlara aynı anda güç verir. Switch'in toplam PoE bütçesi sınırlıdır. Bütçe aşılırsa bazı portlara güç verilmez ve o cihazlar açılmaz. Bu, sık görülen bir "telefon çalışmıyor" arızasıdır.
- **Fabrika ortamı:** Bir veri kablosu, büyük bir motorun güç kablosuyla aynı kanaldan geçiriliyor. Motor her çalıştığında güçlü bir manyetik alan oluşur, kabloya gürültü indüklenir ve switch portunda CRC hataları artar. Çözümler: kabloları ayırmak, ekranlı kablo kullanmak ya da fibere geçmek. Fiber ışık kullandığı için EMI'den etkilenmez (01-07).
- **Veri merkezi:** Ağ cihazlarının harcadığı her watt ısıya dönüşür ve soğutulması gerekir. Bu yüzden veri merkezlerinde port başına güç tüketimi önemli bir tasarım ölçütüdür.

## 6. Diğer Konularla Bağlantı

| Bu dosyadaki fikir | Nerede derinleşiyor |
|---|---|
| Gürültü payı ve karar eşiği | 00-01, 01-04 |
| Transistör, gerilimle kontrol edilen bir anahtar olarak | 00-05 |
| Sinyallerin frekansı ve bant genişliği | 01-02 |
| Zayıflama, gürültü, karışma, yansıma | 01-05 |
| Diferansiyel sinyal ve büküm; PoE türleri | 01-06 |
| Fiberin EMI'den etkilenmemesi | 01-07 |
| Uç cihazlar için PoE port ayarları | LAB-018 |

## 7. Cisco ve Pratik

PoE destekli Cisco Catalyst switch'lerde port başına güç durumu şu komutla görülür:

```
Switch# show power inline
```

Çıktı; her portun güç verip vermediğini, harcanan watt değerini ve bağlı cihaz sınıfını gösterir. **[CISCO-ÖZEL]** Bu komut gerçek Cisco donanımında vardır. Packet Tracer 9.0'daki desteği LAB-018 yazılırken doğrulanacak (PROGRESS.md, Bölüm D).

## 8. Yaygın Yanılgılar

| Yanılgı | Doğrusu |
|---|---|
| "Elektronlar kabloda ışık hızıyla akar." | Elektronların ortalama hızı çok düşüktür. Işık hızına yakın yayılan, gerilimdeki değişimin oluşturduğu elektromanyetik dalgadır. |
| "Bir telin gerilimi kendi başına ölçülür." | Gerilim her zaman iki nokta arasındaki farktır. Ethernet bu yüzden bilgiyi iki tel arasındaki farkla taşır. |
| "PoE yüksek gerilim kullanır, tehlikelidir." | PoE yaklaşık 44–57 V DC kullanır ve güvenlik açısından düşük gerilim sınıfındadır. Şebeke elektriği (220–230 V AC) ise tehlikelidir. |
| "Kablo uzadıkça yalnızca direnç artar." | Direnç artar, ama asıl sınırlayıcı etkiler yüksek frekanslarda artan zayıflama, kapasitans ve karışmadır (01-05). |
| "Bakır kablo EMI'den hiç etkilenmez; büküm yalnızca düzen içindir." | Büküm, iki telin gürültüyü eşit almasını sağlayarak diferansiyel alıcının gürültüyü iptal etmesine izin verir. Bükümü bozulmuş kablolar gürültüye çok daha açıktır. |

## 9. Arıza Giderme Yaklaşımı

Fiziksel katman arızalarının çoğu bu dosyadaki dört nedenden birine dayanır:

| Belirti | Olası elektriksel neden |
|---|---|
| Bağlantı hiç kurulmuyor | Döngü kopuk: tel kopmuş, konnektör oturmamış (devre kapanmıyor) |
| Bağlantı kuruluyor ama CRC ve input error sayaçları artıyor | Gürültü (EMI) ya da zayıflama, gürültü payını tüketiyor |
| Uzun kablolarda bağlantı daha düşük hızda kuruluyor | Direnç, kapasitans ve zayıflama, yüksek hızlı sinyali taşıyamıyor |
| PoE cihazı açılmıyor ya da yeniden başlıyor | Switch'in PoE bütçesi aşıldı ya da kablodaki kayıp çok yüksek |

Bu tabloyu 01-10'da `show interfaces` çıktılarıyla birleştireceğiz.

## 10. CCNA Bağlantısı

CCNA elektrik hesabı sormaz. Ancak v1.1 1.1.h (PoE), 1.3 (kablo türleri) ve 1.4 (arayüz ve kablo sorunları) konularındaki "hangi kablo, neden?" ve "bu hata neden oluşur?" sorularının arkasındaki mantık bu dosyadadır.

## 11. Kendini Kontrol Et

1. Bir telin direnci 2 Ω ve üzerinden 0,5 A akım geçiyor. Telin iki ucu arasındaki gerilim farkı nedir? Telde ısıya dönüşen güç nedir?
   <details><summary>Cevap</summary>
   V = I × R = 0,5 × 2 = <b>1 V</b>. P = I² × R = 0,25 × 2 = <b>0,5 W</b>.
   </details>

2. Bir kablonun uzunluğunu iki katına çıkarırsan direnci nasıl değişir?
   <details><summary>Cevap</summary>
   Direnç uzunlukla doğru orantılıdır; iki katına çıkar.
   </details>

3. PoE'de aynı gücü yarı gerilimle taşımak istersen kablodaki kayıp nasıl değişir?
   <details><summary>Cevap</summary>
   Aynı güç için akım iki katına çıkar (I = P / V). Kayıp I² × R olduğu için <b>dört katına</b> çıkar.
   </details>

4. Diferansiyel bir alıcı neden gürültüye karşı dayanıklıdır? Bunun çalışması için hangi koşul gerekir?
   <details><summary>Cevap</summary>
   Alıcı iki telin farkını ölçer. Her iki tele eşit miktarda eklenen gürültü çıkarma işleminde birbirini götürür. Koşul, iki telin gürültüyü gerçekten eşit almasıdır; bunu tellerin birbirine sarılması (büküm) sağlar.
   </details>

5. 100 metrelik bir kabloda sinyalin yayılma gecikmesi yaklaşık ne kadardır? Bu gecikmenin kaynağı elektronların yavaşlığı mıdır?
   <details><summary>Cevap</summary>
   Yaklaşık 5 ns/m × 100 m = <b>500 ns</b> (0,5 µs). Kaynağı elektronların hızı değildir. Elektromanyetik dalga kablo malzemesi içinde ışık hızının yaklaşık üçte ikisiyle yayılır.
   </details>

## 12. Uygulama

Bu dosyanın PT pratiği yoktur. Evinde ya da yurdunda gözlem yap: Ethernet kablolarının yakınından geçen güç kablolarını, bükümünün açıldığı konnektör uçlarını ve ezilmiş kabloları ara. Bunların her birinin hangi elektriksel etkiye (gürültü, direnç, empedans değişimi) yol açacağını yaz. 01-05'i okuduktan sonra listeni kontrol et.

## 13. Ustalık Kontrol Listesi

- [ ] Gerilim, akım ve direnci kendi cümlelerimle ve bir benzetmeyle açıklayabiliyorum; benzetmenin sınırını da biliyorum.
- [ ] Ohm yasasıyla ve P = I² × R ile basit hesaplar yapabiliyorum.
- [ ] PoE'nin neden yaklaşık 48 V kullandığını bir sayısal örnekle gösterebiliyorum.
- [ ] Diferansiyel sinyalin gürültüyü nasıl iptal ettiğini çizerek anlatabiliyorum.
- [ ] Sinyal hızı ile elektron hızı arasındaki farkı açıklayabiliyorum.

## Kaynaklar

- [IEEE-8023] IEEE 802.3: PoE Type 1–4 güç seviyeleri ve PSE gerilim aralıkları.
- [TXT-SPURGEON] Ethernet: The Definitive Guide, 2. baskı: kablo ve sinyal ayrıntıları (ek okuma).
- [TXT-HARRIS] Digital Design and Computer Architecture: devre temelleri ([DERİN] ek okuma).

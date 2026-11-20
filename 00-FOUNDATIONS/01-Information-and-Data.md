# 00-01 Bilgi ve Veri (Information and Data)

> Önkoşullar: — | Tahmini süre: ~1,5 saat | CCNA: dolaylı (v1.1 1.3, 1.4'ün altyapısı)

## Öğrenme Hedefleri

- Bilgi (information) ile veri (data) arasındaki farkı bir ağ örneğiyle açıklamak.
- Analog ve dijital temsili karşılaştırmak; dijitalin ağ iletişiminde neden kazandığını gerekçelendirmek.
- Bilgisayarların neden ikili sistem kullandığını gürültü payı (noise margin) kavramıyla açıklamak.
- N olası durumu ayırt etmek için kaç bit gerektiğini hesaplamak.
- "Kabloda 0 ve 1 akar" yanılgısını düzeltmek.

## 1. Sezgisel Giriş

Bir arkadaşınla bir anlaşma yapıyorsun: "Akşam maça geleceksem odamın ışığını yakacağım, gelmeyeceksem yakmayacağım." Arkadaşın pencereden baktığında iki olasılıktan birini öğrenir. Işık burada **veri**dir: fiziksel bir durum. Arkadaşının öğrendiği "geliyor" ya da "gelmiyor" ise **bilgi**dir: belirsizliğin ortadan kalkması.

Dikkat et, iki şey olmadan bu sistem çalışmaz:

1. **Ayırt edilebilir durumlar:** Işık ya açık ya kapalı olmalı. Yarı açık bir lamba kafa karıştırır.
2. **Önceden yapılmış bir anlaşma:** "Işık açık = geliyorum" kuralını ikiniz de bilmelisiniz. Bu kurala sahip olmayan biri için ışık yalnızca ışıktır.

Bilgisayar ağları tam olarak bu iki fikrin üzerine kurulur. Kablodaki gerilimler, fiberdeki ışık darbeleri ve havadaki radyo dalgaları **veriyi** taşır. Bu veriden **bilgi** çıkarabilmek için gönderici ile alıcının aynı kurallar üzerinde anlaşmış olması gerekir. Ağ dünyasında bu kurallara **protokol (protocol)** denir.

## 2. Neden Var?

### 2.1 Bilgi nedir?

Claude Shannon 1948'de iletişimi matematiksel olarak tanımlarken bilgiyi anlamla değil **belirsizliğin azalmasıyla** ölçtü [PAPER-SHANNON]. Bir mesaj, alıcının bilmediği bir şeyi ne kadar netleştiriyorsa o kadar bilgi taşır. "Güneş yarın doğacak" mesajı neredeyse hiç bilgi taşımaz; zaten biliyorsun. Bir yazı-tura atışının sonucu ise tam olarak bir birimlik belirsizliği giderir.

Bu birimin adı **bit (binary digit)**'tir: **eşit olasılıklı iki seçenek arasındaki tek bir karar.**

### 2.2 Veri nedir?

Veri, bilginin **temsilidir**: semboller, sayılar, baytlar, gerilim seviyeleri. Aynı bilgi farklı verilerle temsil edilebilir:

| Bilgi | Temsil 1 | Temsil 2 |
|---|---|---|
| "5 sayısı" | 8 bitlik tamsayı: `00000101` | ASCII karakteri "5": `00110101` (0x35) |
| "Evet" | Işık açık | Tek bir bit: `1` |
| Bir hedef adres | `192.168.1.10` (metin) | 32 bitlik sayı: `11000000 10101000 00000001 00001010` |

Tablonun ilk satırı önemli bir ders içerir: `00000101` ile `00110101` farklı bit dizileridir ama ikisi de "5"i temsil edebilir. Hangisinin kullanıldığını bilmeden bitlere bakmak sana hiçbir şey söylemez. **Bitlerin anlamı bitlerin içinde değil, anlaşmadadır.** Bu yüzden ağda her protokol, hangi bitin hangi anlama geldiğini bayt bayt tanımlar. Ethernet çerçevesinin ilk 6 baytının hedef MAC adresi olması (02-03) ya da IPv4 başlığındaki 9. baytın üst katman protokolünü göstermesi (03-02) bu tür anlaşmalardır.

## 3. Mekanizma: Analog ve dijital temsil

### 3.1 Analog temsil

**Analog (analog)** temsilde değer süreklidir; belirli bir aralıktaki her değeri alabilir. Bir mikrofonun ürettiği gerilim, havadaki ses basıncını bire bir taklit eder. Ses yükseldikçe gerilim de yükselir; 0,312 V, 0,3121 V, 0,31215 V… hepsi farklı bir değeri temsil eder.

Analog temsilin büyük zayıflığı şudur: **Her bozulma doğrudan bilgiye karışır.** Kabloya karışan 0,002 V'luk bir gürültü, alıcı tarafında "gerçek" sesten ayırt edilemez. Bir fotokopinin fotokopisini çektikçe görüntünün bozulması gibi: her kopya bir öncekinin hatasını da taşır ve hata birikir.

### 3.2 Dijital temsil

**Dijital (digital)** temsilde değer **sınırlı sayıda ayrık sembolden** biridir. En basit durumda iki sembol vardır: 0 ve 1. Alıcı, gelen sinyali "tam olarak hangi değer?" diye değil, **"hangi sembole en yakın?"** diye yorumlar.

Bir örnek: Gönderici 0 için 0 V, 1 için 1 V kullansın. Alıcı **karar eşiğini (decision threshold)** 0,5 V'a koysun:

```
 Gerilim
  1.0 V ─────────────  "1" gönderildi
                        ↑ gürültü payı: 0,5 V'a kadar bozulma tolere edilir
  0.5 V ─ ─ ─ ─ ─ ─ ─  karar eşiği
                        ↓ gürültü payı
  0.0 V ─────────────  "0" gönderildi
```

Gelen değer 0,87 V ya da 1,12 V olabilir; alıcı ikisini de "1" olarak okur. Gürültü eşiği aşmadıkça **bilgi kaybolmaz.** Sembol ile eşik arasındaki bu güvenlik mesafesine **gürültü payı (noise margin)** denir.

Dijital temsilin ağ iletişimi için sağladığı dört büyük avantaj bu mekanizmadan doğar:

1. **Yenileme (regeneration):** Bir ara cihaz sinyali okuyup sembolleri kusursuz bir şekilde yeniden üretebilir. Gürültü bir sonraki bağlantıya taşınmaz. Bu, analogdaki "fotokopinin fotokopisi" sorununu çözer. Her switch ve router portu tam olarak bunu yapar.
2. **Hata tespiti (error detection):** Semboller sayılabildiği için üzerlerinde matematik yapılabilir. Göndericinin eklediği bir kontrol değeri (Ethernet'te FCS, 02-04), alıcının bozulmayı fark etmesini sağlar.
3. **Kayıpsız kopyalama ve saklama:** Bir dosyayı bin kez kopyalasan da bitler aynı kalır.
4. **Mantıkla işleme:** Sembollerle mantık işlemleri yapılabilir (00-03). Bir router'ın hedef adresi maskeyle karşılaştırması, bitler üzerinde yapılan bir AND işlemidir.

### 3.3 Neden ikili? Neden 10 seviye değil?

Daha fazla seviye kullanırsan tek bir sembolde daha fazla bilgi taşırsın. Ama aynı gerilim aralığına daha çok seviye sığdırırsan seviyeler birbirine yaklaşır ve gürültü payı küçülür:

| Seviye sayısı | 0–1 V aralığında seviyeler arası mesafe | Sembol başına bit |
|---|---|---|
| 2 | 1 V | 1 |
| 4 | ~0,33 V | 2 |
| 10 | ~0,11 V | ~3,32 |

Bilgisayarın içinde ikili seçilmesinin nedeni **güvenilirlik ve basitliktir**, hız değil:

- Transistör (00-05) en kolay ve en güvenilir şekilde iki durumda çalışır: tam iletimde ya da tam kesimde. Ara değerlerde çalıştırmak hem daha çok güç harcar hem de sıcaklık ve üretim farklılıklarına karşı hassastır.
- İki seviye, belirli bir gerilim aralığında en geniş gürültü payını verir.
- Mantık işlemleri (00-03) ikili değerlerle doğrudan tanımlanır.

> **[TCP/IP-GERÇEK]** İletişim hatları her zaman ikili sinyal kullanmaz. Bant genişliği kısıtlı olduğunda mühendisler gürültü payından vazgeçip sembol başına daha çok bit taşır. 1000BASE-T Ethernet, kabloda beş seviyeli PAM-5 sembolleri kullanır; Wi-Fi tek bir sembolde birçok biti QAM ile taşır. Bilgisayarın içi ikilidir, ama kablodaki sinyal bu ikili veriyi başka bir alfabeyle kodlayabilir. Bu konu 01-03'te açılacak.

### 3.4 Önemli bir ayrım: "dijital sinyal" bir yorumdur

Fiziksel dünyada her sinyal süreklidir. Kablodaki gerilim 0 V'tan 1 V'a anında sıçramaz; bir eğri çizerek yükselir, yolda gürültü alır, bükülür. "Dijital sinyal" dediğimiz şey, **sürekli bir fiziksel büyüklüğün ayrık sembollere göre yorumlanmasıdır.** Alıcının işi tam olarak budur: Sürekli bir dalga biçimini belirli anlarda örnekler ve her örneği bir sembole eşler. Bunun nasıl yapıldığı 01-04'ün konusudur.

### 3.5 Analogdan dijitale ve geri

Gerçek dünyadaki bilginin çoğu analogdur: ses, görüntü, sıcaklık. Bunları ağda taşımak için önce dijitale çevirmek gerekir. Bu dönüşümün iki adımı vardır (ayrıntılar 00-06'da):

1. **Örnekleme (sampling):** Sürekli sinyalden belirli aralıklarla ölçüm almak. Örneğin bir sesi saniyede 48.000 kez ölçmek.
2. **Nicemleme (quantization):** Her ölçümü sonlu sayıda seviyeden en yakınına yuvarlamak. Örneğin 16 bitle 65.536 seviyeden birine.

Bu yuvarlama küçük ama kalıcı bir hata yaratır (nicemleme hatası). Karşılığında elde edilen veri artık gürültüye karşı korunabilir, kopyalanabilir ve ağda taşınabilir.

## 4. Teknik Ayrıntı: Bir bilgi kaç bit eder?

N tane **eşit olasılıklı** durumdan birini belirtmek için gereken bit sayısı log₂(N)'dir. Bit sayısı tam sayı olmak zorunda olduğundan pratikte bu değer yukarı yuvarlanır: ⌈log₂(N)⌉.

| Ayırt edilecek durum | Hesap | Gereken bit |
|---|---|---|
| Yazı-tura | log₂(2) = 1 | 1 |
| Bir zar atışı (6 sonuç) | log₂(6) ≈ 2,585 | 3 |
| İngiliz alfabesindeki 26 harf | log₂(26) ≈ 4,7 | 5 |
| 1000 farklı host'tan biri | log₂(1000) ≈ 9,97 | 10 |
| Tüm IPv4 adresleri | 2³² | 32 |
| Tüm MAC adresleri | 2⁴⁸ | 48 |

Ters yönde de düşünebilirsin: **n bit, 2ⁿ farklı durumu ayırt edebilir.** Her bit eklediğinde ayırt edebileceğin durum sayısı ikiye katlanır. Bu basit kural, subnetting'in temelidir: Bir alt ağın host kısmında 8 bit varsa 2⁸ = 256 farklı adres vardır (03-04).

> **[DERİN]** Durumlar eşit olasılıklı değilse ortalama bilgi miktarı daha düşüktür. Shannon bunu **entropi (entropy)** ile tanımladı: H = −Σ pᵢ · log₂(pᵢ). Örneğin %90 yazı, %10 tura gelen hileli bir para atışı yaklaşık 0,47 bit bilgi taşır, çünkü sonuç büyük ölçüde tahmin edilebilir. Kayıpsız sıkıştırma (06-04) bu fazlalığı kullanır: Bir veri, entropisinin altına sıkıştırılamaz.

## 5. Gerçek Dünya Örnekleri

- **Görüntülü görüşme:** Mikrofon havadaki basınç değişimini analog bir gerilime çevirir. Ses kartı bu gerilimi örnekler ve nicemler; sonuç bir bit dizisidir. Bu bitler sıkıştırılır (06-04), paketlere bölünür ve ağda taşınır. Karşı tarafta bitler yeniden bir gerilime, gerilim de hoparlörde ses dalgasına dönüşür. Uçtan uca yalnızca iki noktada analog dünya vardır: mikrofon ve hoparlör.
- **Çevrim içi oyun:** Bir tuşa basman, oyunun protokolüne göre birkaç baytlık bir mesaja dönüşür ("oyuncu 7, x=120, y=45'e hareket etti"). Bu baytlar sunucuya ulaştığında sunucu aynı protokolü kullanarak onları yeniden anlama çevirir.
- **Ev ağın:** Dizüstü bilgisayarın ile modem arasında aynı bitler en az iki farklı fiziksel biçimde taşınır: havada radyo dalgası olarak (Wi-Fi), modemin içinde ve kablosunda elektrik sinyali olarak. Biçim değişir, bitler değişmez. Ortamlar arasındaki bu bağımsızlık, katmanlı modelin (00-09) en önemli sonucudur.

## 6. Diğer Konularla Bağlantı

| Bu dosyadaki fikir | Nerede derinleşiyor |
|---|---|
| İkili sayılar, bit ve bayt | 00-02 |
| Bitler üzerinde mantık işlemleri | 00-03 |
| Gerilim ve gürültü | 00-04 |
| Transistörün iki durumu | 00-05 |
| Ses, görüntü ve metnin bitlerle temsili | 00-06, 06-02 |
| Bitlerin sinyale dönüşmesi ve çok seviyeli semboller | 01-02, 01-03 |
| Alıcının sembol kararı | 01-04 |
| Gürültü ve sinyal bozulması | 01-05 |
| Hata tespiti | 02-04 |
| Protokol kavramı | 00-08, 00-09 |

## 7. Cisco ve Pratik

Bir Cisco cihazında `show interfaces` komutunun çıktısı, aynı trafiği hem **bit** hem **bayt** cinsinden gösterir. Örnek çıktı (değerler örnektir):

```
  5 minute input rate 2000 bits/sec, 3 packets/sec
  ...
     1234 packets input, 567890 bytes, 0 no buffer
```

İlk satırdaki hız bit/saniye, ikinci satırdaki sayaç bayt cinsindendir. Bu iki birimi karıştırmamak, kapasite ve performans hesaplarında temel bir beceridir (birim dönüşümleri 00-02'de).

## 8. Yaygın Yanılgılar

| Yanılgı | Doğrusu |
|---|---|
| "Kabloda 0'lar ve 1'ler akar." | Kabloda sürekli değişen bir gerilim vardır. Alıcı onu belirli anlarda örnekleyip sembollere çevirir. Üstelik semboller her zaman ikili değildir (1000BASE-T'de beş seviye). |
| "Veri ile bilgi aynı şeydir." | Veri temsildir, bilgi ise o temsilin bir anlaşmaya göre yorumlanmasıyla giderilen belirsizliktir. Aynı bitler farklı protokollerde farklı anlamlara gelir. |
| "Bilgisayarlar ikili kullanır, çünkü ikili daha hızlıdır." | Asıl neden güvenilirlik ve basitliktir: İki durum en geniş gürültü payını verir ve transistör iki durumda en kararlı çalışır. |
| "Analog kötü, dijital iyidir." | Gerçek dünya analogdur ve her dijital sistem sonunda analog bir fiziksel ortamı kullanır. Dijitalin üstünlüğü, gürültünün birikmesini ve yayılmasını engellemesidir. |
| "Bir bit, bir gerilim seviyesine eşittir." | Bit soyut bir bilgi birimidir. Fiziksel olarak bir bit; bir gerilim seviyesiyle, bir geçişle (Manchester kodlaması), birden çok bitin tek bir sembolde birleşmesiyle ya da ışığın varlığıyla temsil edilebilir. |

## 9. Arıza Giderme Yaklaşımı

Bu dosyanın arıza giderme dersi tek bir cümledir: **Gürültü karar eşiğini aşarsa alıcı yanlış sembole karar verir.** Bir bitin yanlış okunması, o bitin taşıdığı çerçevenin bozulması demektir. Alıcı bunu hata tespit koduyla (FCS) fark eder ve çerçeveyi atar.

Bir switch arayüzünde artan `CRC` ve `input errors` sayaçları gördüğünde zincir şöyle işler: fiziksel bir sorun (hasarlı kablo, elektromanyetik parazit, duplex uyumsuzluğu) → gürültü → yanlış sembol kararları → bozuk çerçeveler → FCS hatası → atılan çerçeveler. Bu zinciri 01-05, 01-10 ve 02-04'te adım adım kuracağız.

## 10. CCNA Bağlantısı

CCNA bu konuyu doğrudan sormaz. Ama v1.1 1.3 (kablo türleri) ve 1.4 (arayüz ve kablo sorunları) konularındaki "neden" sorularının cevabı buradaki gürültü payı fikrine dayanır.

## 11. Kendini Kontrol Et

1. Bir ağ protokolünün "bitlere anlam veren anlaşma" olduğunu bir örnekle açıkla.
   <details><summary>Cevap</summary>
   Örneğin Ethernet standardı, çerçevenin ilk 6 baytının hedef MAC adresi olduğunu söyler. Bu anlaşmayı bilmeyen bir alıcı için o 48 bit yalnızca bir bit dizisidir. Anlam, bitlerin içinde değil, iki tarafın uyguladığı ortak kuraldadır.
   </details>

2. Bir repeater (tekrarlayıcı) analog bir sinyali güçlendirdiğinde ne olur? Dijital bir sinyali yenilediğinde ne olur?
   <details><summary>Cevap</summary>
   Analog sinyali güçlendirdiğinde içindeki gürültüyü de güçlendirir; gürültü bir sonraki bağlantıya taşınır ve birikir. Dijital sinyali yenilediğinde önce sembollere karar verir, sonra temiz sembolleri yeniden üretir. Gürültü eşiği aşmadığı sürece hiçbir hata taşınmaz.
   </details>

3. Bir ağda 500 cihaza benzersiz bir numara vermek istiyorsun. En az kaç bit gerekir?
   <details><summary>Cevap</summary>
   2⁸ = 256 < 500 ≤ 512 = 2⁹. En az 9 bit gerekir.
   </details>

4. Neden bir hattaki sembol seviyesi sayısını artırmak hem bir kazanç hem bir risktir?
   <details><summary>Cevap</summary>
   Kazanç: Her sembol daha fazla bit taşır, aynı sembol hızında daha yüksek veri hızı elde edilir. Risk: Seviyeler birbirine yaklaşır, gürültü payı küçülür ve alıcının yanlış karar verme olasılığı artar.
   </details>

5. "Dijital sinyal" ifadesi fiziksel olarak neden bir basitleştirmedir?
   <details><summary>Cevap</summary>
   Fiziksel ortamdaki gerilim, ışık ya da radyo dalgası her zaman süreklidir ve sonlu bir hızla değişir. "Dijital" olan, alıcının bu sürekli büyüklüğü belirli anlarda örnekleyip ayrık sembollere göre yorumlamasıdır.
   </details>

## 12. Uygulama

Bu dosyanın PT pratiği yoktur. Kısa bir düşünce alıştırması yap: Evindeki Wi-Fi'den bir videonun telefonuna ulaşmasını düşün. Bilginin **analog** olduğu her noktayı ve **dijital** olduğu her noktayı sırayla yaz. Aynı bitlerin kaç farklı fiziksel ortamda taşındığını say. Cevabını 08-05'i okuduğunda kontrol edeceksin.

## 13. Ustalık Kontrol Listesi

- [ X ] Bilgi ile veri farkını, kaynağa bakmadan bir ağ örneğiyle anlatabiliyorum.
- [ X ] Gürültü payı kavramını bir çizimle açıklayabiliyorum.
- [ ] Dijitalin ağ iletişimine sağladığı dört avantajı ve her birinin nedenini söyleyebiliyorum.
- [ X ] N durum için gereken bit sayısını ve n bitin ayırt edebileceği durum sayısını hesaplayabiliyorum.
- [ X ] "Kabloda 0 ve 1 akar" ifadesinin neden yanlış olduğunu iki gerekçeyle açıklayabiliyorum.

## Kaynaklar

- [PAPER-SHANNON] C. E. Shannon, "A Mathematical Theory of Communication" (1948): bit ve entropi kavramları.
- [TXT-PETZOLD] Code, 2. baskı: bilgi, kodlar ve ikili sistem üzerine sezgisel anlatım (ek okuma).
- [IEEE-8023] 1000BASE-T'nin PAM-5 kullanması (ayrıntılar ve madde numarası 01-03'te).

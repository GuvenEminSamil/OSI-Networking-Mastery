# 12-02 Modül Modül Tekrar Kartları (Flashcards by Module)

> Bu dosya bir **başlangıç setidir**. Kendi cümlelerinle yazdığın kartlar daha etkilidir (12-01, Bölüm 3). Anki'ye aktarılmaya hazır sürümleri `12-REVISION/anki/` klasöründedir (sekmeyle ayrılmış, dosya başına bir ders).
>
> Kartlar, ilgili teori dosyası yazıldıkça eklenir. Son güncelleme: 2026-11-19 (00-01 – 00-04).

## 00-FOUNDATIONS

### 00-01 Bilgi ve Veri

| Soru | Cevap |
|---|---|
| Bilgi ile veri arasındaki fark nedir? | Veri temsildir (bitler, gerilimler). Bilgi, bu temsilin ortak bir anlaşmaya göre yorumlanmasıyla giderilen belirsizliktir. |
| Bir bit tam olarak neyi ölçer? | Eşit olasılıklı iki seçenek arasındaki tek bir kararı. |
| Gürültü payı nedir ve neden önemlidir? | Bir sembol seviyesi ile karar eşiği arasındaki mesafe. Gürültü bu mesafeyi aşmadıkça alıcı doğru sembole karar verir. |
| Dijital temsil, bir ara cihazın gürültüyü bir sonraki bağlantıya taşımasını nasıl engeller? | Cihaz sembollere karar verir ve temiz sembolleri yeniden üretir (yenileme). Analogda ise gürültü sinyalle birlikte güçlendirilir. |
| Bilgisayarlar neden ikili kullanır? | İki durum en geniş gürültü payını verir ve transistör iki durumda en kararlı çalışır. Neden hız değil, güvenilirliktir. |
| Kabloda her zaman ikili sinyal mi vardır? | Hayır. Örneğin 1000BASE-T beş seviyeli PAM-5 sembolleri kullanır; Wi-Fi QAM ile sembol başına birçok bit taşır. |
| 1000 cihaza benzersiz numara vermek için en az kaç bit gerekir? | 10 bit (2¹⁰ = 1024). |

### 00-02 Sayı Sistemleri ve Birimler

| Soru | Cevap |
|---|---|
| Bir baytın konum ağırlıkları nelerdir (soldan sağa)? | 128, 64, 32, 16, 8, 4, 2, 1 |
| Maske baytlarında kullanılan sekiz değer nelerdir (0 hariç)? | 128, 192, 224, 240, 248, 252, 254, 255 |
| Onaltılık neden ağda yaygındır? | Bir onaltılık basamak tam olarak 4 bite (nibble) karşılık gelir; uzun bit dizileri kısa ve hatasız yazılır. |
| 0x0800 onluk tabanda kaçtır? | 2048 (8 × 256). Ethernet'te IPv4'ün EtherType değeridir. |
| RFC'ler neden "byte" yerine "octet" der? | Geçmişte bayt her zaman 8 bit değildi; oktet tam olarak 8 bit demektir. |
| 1 Gbps kaç MB/s eder (ham)? | 125 MB/s (1000 / 8). |
| 1 TB'lık disk Windows'ta neden ~931 GB görünür? | Üretici 10¹² bayt sayar; sistem 2³⁰'luk birimlerle bölüp "GB" etiketiyle gösterir: 10¹² / 2³⁰ ≈ 931. |
| Ağ bağlantı hızları hangi birim sistemini kullanır? | Ondalık SI birimleri ve bit/saniye (1 Gbps = 10⁹ bit/s). |

### 00-03 İkili Aritmetik ve Boole Mantığı

| Soru | Cevap |
|---|---|
| XOR ile OR'u ayıran tek satır hangisidir? | 1 ve 1: OR 1 verir, XOR 0 verir. XOR "bitler farklı mı?" sorusudur. |
| Bir IP adresinden ağ adresi hangi işlemle bulunur? | Adres AND maske. |
| Yayın adresi hangi işlemle bulunur? | Adres OR joker maske (host bitlerinin tamamını 1 yapmak). |
| 255.255.255.192 maskesinin joker maskesi nedir? | 0.0.0.63 (her bayt için 255 − değer). |
| Hedefin yerel olup olmadığına kim karar verir? | Gönderen host, kendi maskesiyle iki adresi AND'leyerek. Router değil. |
| Parite neden çift sayıda bit hatasını kaçırır? | Yalnızca 1'lerin sayısının tekliğine bakar; iki bit değişince teklik değişmez. |
| Yarım toplayıcı hangi kapılardan oluşur? | Toplam için XOR, elde için AND. |
| TCP sıra numaraları neden modüler aritmetikle karşılaştırılır? | 32 bitlik sabit genişlikte oldukları için zamanla taşar ve 0'a dönerler. |

### 00-04 Elektrik Temelleri

| Soru | Cevap |
|---|---|
| Ohm yasası nedir? | V = I × R |
| Bir telde ısıya dönüşen güç akıma nasıl bağlıdır? | Akımın karesiyle: P = I² × R. Akım iki katına çıkarsa kayıp dört katına çıkar. |
| PoE neden ~48 V kullanır? | Aynı gücü düşük akımla taşıyıp kablodaki I²R kaybını küçük tutmak için; bu gerilim aynı zamanda güvenlik açısından düşük gerilim sınıfındadır. |
| Gerilim neden "bir telde" değil, "iki nokta arasında" ölçülür? | Gerilim tanımı gereği potansiyel farkıdır; her zaman bir referansa göredir. |
| Diferansiyel alıcı gürültüyü nasıl iptal eder? | İki telin farkını alır; iki tele eşit eklenen gürültü çıkarmada yok olur. |
| Diferansiyel sinyalin çalışması için hangi koşul gerekir? | İki telin gürültüyü eşit alması; bunu büküm sağlar. |
| Sinyal neden kabloda çok hızlı yayılır, elektronlar yavaş olduğu hâlde? | Yayılan, gerilim değişiminin oluşturduğu elektromanyetik dalgadır (~5 ns/m), elektronların kendisi değil. |
| 802.3af ve 802.3at'nin güç kaynağı tarafındaki en yüksek güçleri nedir? | af (PoE): 15,4 W. at (PoE+): 30 W. |
| Bükümlü çift Ethernet kablosunun karakteristik empedansı nedir? | 100 Ω. |

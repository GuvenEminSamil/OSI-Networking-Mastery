# FND-DAT Cevap Anahtarı

> Sorular: `../Q-FND-DAT.md`. Önce soruları çöz, sonra bu dosyayı aç. Puanlama kuralları: `10-QUESTION-BANK/README.md`.

---

### FND-DAT-001
**Cevap:** B

**Açıklama:** İkili seçilmesinin nedeni güvenilirlik ve basitliktir. Bir gerilim aralığını iki seviyeye bölmek, seviyeler ile karar eşiği arasındaki mesafeyi, yani gürültü payını en büyük yapar. CMOS transistörler de tam iletim ve tam kesim uçlarında en kararlı ve en az güç harcayarak çalışır.

**Çeldiriciler:**
- A) Hız neden değildir. 00-01 bunu açıkça vurgular: Neden güvenilirliktir.
- C) Yanlış. Kablolar ikiden fazla seviye taşıyabilir; 1000BASE-T beş seviyeli PAM-5 kullanır. İkili, bilgisayarın **içi** için bir tercihtir.
- D) Tersine, ikili aynı sayı için onluktan **daha fazla** basamak kullanır.

**Teori:** → 00-01, Bölüm 3.3; 00-05, Bölüm 3.3

---

### FND-DAT-002
**Cevap:** a) **12 bit**. b) **1.096** cihaz.

**Açıklama:** 2¹¹ = 2.048 < 3.000, ama 2¹² = 4.096 ≥ 3.000. Bu yüzden ⌈log₂ 3000⌉ = 12 bit gerekir. 12 bit 4.096 farklı değer verir; 4.096 − 3.000 = 1.096 boş değer kalır.

**Puan:** Her parça 0,5.

**Teori:** → 00-01, Bölüm 4; 00-02, Bölüm 4.5

---

### FND-DAT-003
**Cevap:** a) `1100 0000 1010 1000`. b) **49.320**. c) **192.168.**…

**Açıklama:** Her onaltılık basamak 4 bittir: C = 1100, 0 = 0000, A = 1010, 8 = 1000. 16 bitlik değer 0xC0 × 256 + 0xA8 = 192 × 256 + 168 = 49.152 + 168 = 49.320. Oktet olarak okunursa 0xC0 = 192, 0xA8 = 168; adres `192.168.` ile başlar.

**Puan:** Her parça 1/3.

**Teori:** → 00-02, Bölüm 4.2 ve 4.4; 00-06, Bölüm 1

---

### FND-DAT-004
**Cevap:** **Haklı değil**; 60 MB/s, 500 Mbps'lık bir bağlantının pratikte ulaşılabilecek en yüksek değerine çok yakındır.

**Açıklama:**
- 500 Mbps = 500 × 10⁶ bit/s → 8'e bölünce **62,5 MB/s** (ondalık megabayt, ham).
- Başlıklar (Ethernet, IP, TCP) kabloda yaklaşık %5 yer kaplar (00-09, Bölüm 4.1): 62,5 × 0,949 ≈ **59,3 MB/s**.
- Program MiB/s gösteriyorsa ham değer bile 62,5 × 10⁶ / 2²⁰ ≈ 59,6 MiB/s'tır.

Yani 60 MB/s, bağlantının neredeyse tamamının kullanıldığını gösterir. Arkadaşının hatası, bit ile baytı (8 kat) ve başlık yükünü hesaba katmamaktır.

**Puan:** Mbps → MB/s dönüşümü (8'e bölme) 0,5; başlık yükünü ya da MB/MiB farkını belirtip doğru sonuca varmak 0,5.

**Teori:** → 00-02, Bölüm 4.8 ve 4.9; 00-09, Bölüm 4.1

---

### FND-DAT-005
**Cevap:** A ve C

**Açıklama:** /26 maskesi 255.255.255.192'dir; son oktette blok büyüklüğü 256 − 192 = 64'tür. 77, 64–127 bloğundadır. Ağ adresi = adres AND maske = 10.20.30.64. Joker maske = 255 − 192 = 63 → 0.0.0.63. Yayın adresi = ağ adresi OR joker maske = 10.20.30.127.

**Çeldiriciler:**
- B) 10.20.30.255, /24 bir ağın yayın adresi olurdu.
- D) 10.20.30.0, /24 bir ağın adresi olurdu; /26'da 77 ikinci bloktadır.
- E) 0.0.0.192, maskenin son okteti ile joker maskenin karıştırılmasıdır.

**Teori:** → 00-03, Bölüm 4.1, 4.2 ve 4.3

---

### FND-DAT-006
**Cevap:** a) **Uzak**. b) **Yerel**. c) **Hayır**.

**Açıklama:** Her host kararı **kendi** adresi ve **kendi** maskesiyle verir.

a) A'nın maskesi /25. A'nın ağı: 192.168.1.130 AND 255.255.255.128 = 192.168.1.128. B'nin adresi aynı maskeyle: 192.168.1.100 AND 255.255.255.128 = 192.168.1.0. Sonuçlar farklı → A, B'yi **uzak** sayar ve paketi varsayılan ağ geçidine göndermeye çalışır.

b) B'nin maskesi /24. İki adres de 255.255.255.0 ile AND'lenince 192.168.1.0 verir → B, A'yı **yerel** sayar ve doğrudan gönderir.

c) A'da ağ geçidi yoksa A, uzak saydığı B'ye paketi gönderecek bir yer bulamaz; ping A'dan başlatıldığında başarısız olur. (B'den A'ya giden istek A'ya ulaşır; ama A'nın cevabı da aynı nedenle gönderilemez.) Bu tür asimetrik sorunlar, maske hatalarının en kafa karıştırıcı belirtilerindendir.

**Puan:** Her parça 1/3. (a) için hesap gösterilmeden verilen cevap 0'dır.

**Teori:** → 00-03, Bölüm 4.1 ve 5 (ev ağı örneği); ayrıntı 03-06

---

### FND-DAT-007
**Cevap:** a) `01100110`. b) `11001010` (ilk sayı geri geldi). c) XOR kendi kendisinin tersidir: (x XOR k) XOR k = x.

**Açıklama:** XOR, bitler farklıysa 1 verir. Aynı anahtarla iki kez XOR'lamak her biti iki kez çevirir ya da hiç çevirmez; sonuç başlangıç değeridir. Bu özellik parite ve CRC hesaplarında (00-03, Bölüm 4.4) ve birçok şifreleme algoritmasında (06-05) kullanılır.

**Puan:** Her parça 1/3.

**Teori:** → 00-03, Bölüm 3.4 ve 4.4

---

### FND-DAT-008
**Cevap:** B

**Açıklama:** Ağ protokolleri çok baytlı alanları big-endian (ağ bayt sırası) gönderir. `00 35` → 0x0035 = 3 × 16 + 5 = **53**. 53 numaralı port DNS'e aittir (07-02).

**Çeldiriciler:**
- A) 13.568 = 0x3500. Baytları ters sırayla (little-endian) okumanın sonucudur.
- C) 35, onaltılık basamakların onluk sanılmasıdır.
- D) 3.500, baytları ters çevirip onaltılık basamakları onluk okumanın sonucudur.

**Teori:** → 00-06, Bölüm 3.2 ve 4

---

### FND-DAT-009
**Cevap:** a) **500**. b) `0xF4010000` (= 4.093.706.240).

**Açıklama:**
a) Big-endian: 0x000001F4 = 1 × 256 + 0xF4 = 256 + 244 = 500.
b) Little-endian okumada ilk bayt en az anlamlı bayt sayılır; baytlar ters çevrilir: `F4 01 00 00` → 0xF4010000 = 244 × 2²⁴ + 1 × 2¹⁶ = 4.093.640.704 + 65.536 = 4.093.706.240.

**Puan:** Her parça 0,5 (b için onaltılık sonuç yeterli).

**Teori:** → 00-06, Bölüm 3.2

---

### FND-DAT-010
**Cevap:** a) **22 görüşme**. b) Başlıkları unutmuş.

**Açıklama:**
a) 2.000 kbps / 87,2 kbps ≈ 22,9 → tam sayıya **aşağı** yuvarlanır: 22. (23. görüşme hattı aşar.)
b) 64 kbps yalnızca ses verisidir. Her 20 ms'lik pakete 40 bayt RTP/UDP/IP başlığı ve 18 bayt Ethernet başlığı ile FCS eklenir. Başlıklar ses verisinin yaklaşık %36'sı kadar yük getirir; bu yüzden 31 görüşme hattı tıkar ve bütün görüşmelerin kalitesi bozulur.

**Puan:** Her parça 0,5.

**Teori:** → 00-06, Bölüm 3.5 ve 5

---

### FND-DAT-011
**Cevap:** İstemci, port numarasını ağ bayt sırasına çevirmeden (`htons()` kullanmadan) pakete yazmıştır.

**Açıklama:** 5000 = 0x1388. Doğru gönderimde kabloya `13 88` gider. Little-endian bir bilgisayarda bellekte `88 13` olarak durur; çevirmeden kopyalanınca kabloya `88 13` gider ve karşı taraf 0x8813 = 8 × 4096 + 8 × 256 + 1 × 16 + 3 = **34.835** okur. Wireshark'ta görülen değer tam olarak budur.

**Puan:** Nedeni (bayt sırası / `htons()`) söylemek 0,5; 0x1388 → 0x8813 hesabıyla göstermek 0,5.

**Teori:** → 00-06, Bölüm 3.2

---

### FND-DAT-012
**Örnek cevap:** Kabloda giden şey yalnızca bitlerdir; bu bitlerin ne anlama geldiğini, iki tarafın önceden anlaştığı protokol belirler. Örneğin Ethernet başlığındaki `08 00` baytları, EtherType alanında okunduğunda "yükte bir IPv4 paketi var" demektir. Aynı iki bayt bir TCP başlığının port alanında olsaydı 2048 numaralı portu, bir metin dosyasında olsaydı iki kontrol karakterini anlatırdı. Alıcı baytları hangi alanda bulduğuna göre yorumlar; yorum kuralı farklı olursa aynı veri bambaşka bir bilgiye dönüşür. Protokollerin var olma nedeni de bu ortak yorum kuralını sağlamaktır.

**Puanlama ölçütü (toplam 1):**

| Ölçüt | Puan |
|---|---|
| Verinin bitler/baytlar olduğunu, kendi başına anlam taşımadığını söylüyor | 0,25 |
| Aynı baytların iki farklı yorumla iki farklı anlama geldiği, 00-06'dakinden farklı ve doğru bir örnek veriyor | 0,5 |
| Yorum kuralını protokolün ya da alanın konumunun belirlediğini açıklıyor | 0,25 |

**Teori:** → 00-01, Bölüm 2; 00-06, Bölüm 1 ve 3.7

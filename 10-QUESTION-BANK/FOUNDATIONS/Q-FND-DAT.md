# FND-DAT: Bilgi, Sayılar, Mantık ve Veri Temsili

> Kapsam: 00-01, 00-02, 00-03, 00-06 | 12 soru | Önerilen süre: 35 dakika | Cevaplar: `answers/A-FND-DAT.md`
>
> Kurallar ve puanlama: `10-QUESTION-BANK/README.md`. Hesap makinesi kullanma.

---

### FND-DAT-001
**Kategori:** MC · **Zorluk:** 1 · **Teori:** 00-01

Bilgisayarların içinde ikili sistemin kullanılmasının asıl nedeni hangisidir?

- A) İkili sayılarla yapılan toplama, onluk sayılarla yapılandan daha hızlıdır.
- B) İki seviye, belirli bir gerilim aralığında en geniş gürültü payını verir ve transistör iki uçta en kararlı çalışır.
- C) Kablolar fiziksel olarak yalnızca iki gerilim seviyesi taşıyabilir.
- D) İkili sistem, aynı sayıyı yazmak için daha az basamak kullanır.

---

### FND-DAT-002
**Kategori:** O · **Zorluk:** 1 · **Teori:** 00-01, 00-02

Bir kampüsteki 3.000 cihazın her birine benzersiz bir kimlik numarası verilecek.

a) En az kaç bit gerekir?
b) Bu bit sayısıyla, 3.000 cihazdan sonra kaç cihaz için daha yer kalır?

---

### FND-DAT-003
**Kategori:** O · **Zorluk:** 2 · **Teori:** 00-02

`0xC0A8` değerini ele al.

a) İkili olarak yaz.
b) 16 bitlik işaretsiz bir sayı olarak onluk değeri nedir?
c) Bu iki bayt bir IPv4 adresinin ilk iki okteti olsaydı adres nasıl başlardı?

---

### FND-DAT-004
**Kategori:** S · **Zorluk:** 2 · **Teori:** 00-02, 00-09

Bir arkadaşın şöyle diyor: "İnternet paketim 500 Mbps, ama indirme programı en fazla 60 MB/s gösteriyor. Servis sağlayıcı bana eksik hız veriyor."

Haklı mı? Hesabını göstererek açıkla.

---

### FND-DAT-005
**Kategori:** MC · **Zorluk:** 2 · **Teori:** 00-03

`10.20.30.77/26` adresiyle ilgili hangi **iki** ifade doğrudur? (İki tane seçin.)

- A) Ağ adresi 10.20.30.64'tür.
- B) Yayın adresi 10.20.30.255'tir.
- C) Joker maske 0.0.0.63'tür.
- D) Ağ adresi 10.20.30.0'dır.
- E) Joker maske 0.0.0.192'dir.

---

### FND-DAT-006
**Kategori:** İ · **Zorluk:** 3 · **Teori:** 00-03

İki host aynı switch'e bağlı ve aynı VLAN'da. Yöneticinin yaptığı yazım hatası yüzünden maskeleri farklı:

| Host | Adres |
|---|---|
| A | 192.168.1.130/25 |
| B | 192.168.1.100/24 |

a) A, B'ye bir paket gönderirken B'yi yerel mi uzak mı sayar? Hesabını göster.
b) B, A'ya bir paket gönderirken A'yı yerel mi uzak mı sayar?
c) A'da varsayılan ağ geçidi tanımlı değilse A'dan B'ye ping başarılı olur mu?

---

### FND-DAT-007
**Kategori:** O · **Zorluk:** 1 · **Teori:** 00-03

a) `11001010 XOR 10101100` işleminin sonucu nedir?
b) (a)'nın sonucunu yeniden `10101100` ile XOR'la. Ne elde ettin?
c) Bu sonuç XOR'un hangi özelliğini gösterir?

---

### FND-DAT-008
**Kategori:** MC · **Zorluk:** 1 · **Teori:** 00-06

Wireshark'ta bir TCP başlığının hedef port alanı kabloda `00 35` baytlarıyla görünüyor. Hedef port ve büyük olasılıkla ulaşılmak istenen servis hangisidir?

- A) 13.568, bilinmeyen bir servis
- B) 53, DNS
- C) 35, bilinmeyen bir servis
- D) 3.500, bilinmeyen bir servis

---

### FND-DAT-009
**Kategori:** O · **Zorluk:** 2 · **Teori:** 00-06

Bir başlıkta 32 bitlik işaretsiz bir alan kabloda şu dört baytla geliyor: `00 00 01 F4`.

a) Alanın değeri nedir?
b) Bir program bu dört baytı little-endian bir sayı olarak okursa hangi değeri görür? (Sonucu onaltılık yazman yeterli; onluk değer bonus.)

---

### FND-DAT-010
**Kategori:** S · **Zorluk:** 2 · **Teori:** 00-06

Bir şirketin iki şubesi 2 Mbps'lık bir hatla bağlı. Hattın tamamı yalnızca G.711 sesli görüşmelere ayrılırsa ve her görüşme Ethernet üzerinde 87,2 kbps kullanırsa (20 ms paketleme):

a) En fazla kaç eş zamanlı görüşme taşınabilir?
b) Bir çalışan "64 kbps'tan hesaplarsak 31 görüşme sığar" diyor. Hatası nedir?

---

### FND-DAT-011
**Kategori:** A · **Zorluk:** 2 · **Teori:** 00-06

Bir öğrenci kendi yazdığı bir UDP sunucusunu 5000 numaralı portta dinlemeye açtı. Aynı öğrencinin yazdığı istemci sunucuya ulaşamıyor. Wireshark'ta istemcinin gönderdiği paketlerin hedef portu **34835** görünüyor.

En olası neden nedir? Görüşünü bir hesapla destekle.

---

### FND-DAT-012
**Kategori:** K · **Zorluk:** 2 · **Teori:** 00-01, 00-06

"Veri anlamını kendisi taşımaz; anlamı, iki tarafın anlaştığı yorum kuralı verir."

Bu cümleyi kendi cümlelerinle açıkla. 00-06'nın girişindeki `C0 A8 01 01` örneğinden **farklı** bir ağ örneği kullan. (4–6 cümle.)

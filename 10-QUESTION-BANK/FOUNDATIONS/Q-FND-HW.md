# FND-HW: Elektrik, Transistörler ve Bilgisayar Mimarisi

> Kapsam: 00-04, 00-05, 00-07 | 9 soru | Önerilen süre: 30 dakika | Cevaplar: `answers/A-FND-HW.md`
>
> Kurallar ve puanlama: `10-QUESTION-BANK/README.md`. Hesap makinesi kullanma.

---

### FND-HW-001
**Kategori:** O · **Zorluk:** 1 · **Teori:** 00-04

Bir IP kamera PoE ile 48 V'ta 0,25 A çekiyor. Kablonun toplam döngü direnci 10 Ω.

a) Kameranın çektiği güç nedir?
b) Kabloda ısıya dönüşen güç nedir?

---

### FND-HW-002
**Kategori:** MC · **Zorluk:** 1 · **Teori:** 00-04

Bir fabrikada, büyük bir motorun güç kablosuyla aynı kanaldan geçen bir Ethernet kablosunun bağlı olduğu switch portunda CRC hataları artıyor. Hangi **iki** önlem sorunu doğrudan hedefler? (İki tane seçin.)

- A) Veri kablosunu güç kablosundan ayrı bir güzergâha almak
- B) Daha uzun bir kablo kullanmak
- C) Bu bağlantıyı fiber optik kabloya taşımak
- D) Portun hızını 100 Mbps'tan 1 Gbps'a çıkarmak
- E) Switch'i yeniden başlatmak

---

### FND-HW-003
**Kategori:** İ · **Zorluk:** 2 · **Teori:** 00-05

Bir mantık ailesinin veri sayfasında şu değerler var: VOH = 3,0 V, VIH = 2,3 V, VIL = 1,0 V, VOL = 0,4 V.

a) Yüksek ve düşük seviye gürültü paylarını hesapla.
b) Hatta en fazla 0,65 V gürültü bekleniyor. Hangi mantık seviyesi risk altındadır? Neden?

---

### FND-HW-004
**Kategori:** MC · **Zorluk:** 1 · **Teori:** 00-05

Bir Cisco router'da `configure terminal` ile yaptığın değişiklikler ilk olarak nereye yazılır ve elektrik kesilirse ne olur?

- A) NVRAM'deki startup-config'e; korunur.
- B) RAM'deki running-config'e; kaybolur.
- C) Flash'taki IOS imajına; korunur.
- D) ROM'daki bootstrap programına; korunur.

---

### FND-HW-005
**Kategori:** S · **Zorluk:** 2 · **Teori:** 00-05

Laboratuvarda bir Catalyst switch'e `hostname SW-LAB` yazdın ve 10, 20 numaralı VLAN'ları oluşturdun. Hiçbir şeyi kaydetmeden switch'in fişini çektin. Switch açıldığında VLAN 10 ve 20 hâlâ duruyor, ama istem `Switch>` olarak geri gelmiş.

Bu iki farklı sonucu açıkla.

---

### FND-HW-006
**Kategori:** MC · **Zorluk:** 2 · **Teori:** 00-07

Bir Linux sunucusunun bağlı olduğu switch portunda hiç CRC hatası yok. Ancak yoğun trafik saatlerinde sunucuda `ethtool -S` çıktısındaki `rx_missed_errors` sayacı hızla artıyor. En olası neden hangisidir?

- A) Kablo arızalı; çerçeveler bozuk geliyor.
- B) RX halka tamponu doluyor; sürücü ve CPU gelen çerçevelere yetişemiyor.
- C) Sunucu ile switch arasında duplex uyuşmazlığı var.
- D) Ağda sunucuyla aynı IP adresini kullanan başka bir cihaz var.

---

### FND-HW-007
**Kategori:** O · **Zorluk:** 2 · **Teori:** 00-07

100 Mbps'lık bir Ethernet bağlantısında yalnızca en küçük (64 baytlık) çerçeveler gönderiliyor.

a) Saniyede yaklaşık kaç çerçeve geçer? (Preamble, SFD ve IFG'yi hesaba kat.)
b) Bir çerçevenin kabloda kapladığı süre nedir?

---

### FND-HW-008
**Kategori:** KK · **Zorluk:** 2 · **Teori:** 00-07

Kesme (interrupt) ile yoklamayı (polling) karşılaştır:

- Düşük trafikte hangisi, neden daha uygundur?
- Yüksek trafikte hangisi, neden daha uygundur?
- Linux'taki NAPI ikisini nasıl birleştirir?

---

### FND-HW-009
**Kategori:** A · **Zorluk:** 2 · **Teori:** 00-07

Bir öğrenci kendi dizüstü bilgisayarında Wireshark ile yakalama yapıyor. Bilgisayarından **çıkan** TCP paketlerinin checksum alanlarını `incorrect` olarak görüyor ve "kablom bozuk, paketlerim bozuk gidiyor" diyor. Gelen paketlerde ise sorun yok.

a) Öğrenci haklı mı? En olası açıklama nedir?
b) Bu açıklamayı doğrulamak için iki yol söyle.

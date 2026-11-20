# FND-OSI: Katmanlı Modeller (OSI ve TCP/IP)

> Kapsam: 00-09 | 10 soru | Önerilen süre: 30 dakika | Cevaplar: `answers/A-FND-OSI.md`
>
> Kurallar ve puanlama: `10-QUESTION-BANK/README.md`. Hesap makinesi kullanma.

---

### FND-OSI-001
**Kategori:** MC · **Zorluk:** 1 · **Teori:** 00-09

Hangi katman–PDU eşleşmesi doğrudur?

- A) Veri Bağlantı katmanı – paket
- B) Ağ katmanı – çerçeve
- C) Taşıma katmanı (UDP) – datagram
- D) Fiziksel katman – segment

---

### FND-OSI-002
**Kategori:** MC · **Zorluk:** 2 · **Teori:** 00-09

Aşağıdakilerden hangi **iki** protokol uygulama katmanı (L7) protokolüdür? (İki tane seçin.)

- A) DNS
- B) ICMP
- C) ARP
- D) DHCP
- E) OSPF

---

### FND-OSI-003
**Kategori:** B · **Zorluk:** 1 · **Teori:** 00-09

OSI modelinde verinin şifrelenmesi ve sıkıştırılması hangi katmanın görevidir? TCP/IP dünyasında bu işler bugün nerede yapılır? Birer örnek ver.

---

### FND-OSI-004
**Kategori:** O · **Zorluk:** 2 · **Teori:** 00-09, 00-06

Bir bilgisayar iki çerçeve alıyor:

a) Birinci çerçevenin EtherType alanı `0x0806`. Bu çerçevenin yükü hangi protokole aittir? Yükte bir IP başlığı var mıdır?
b) İkinci çerçevede EtherType `0x0800`, IPv4 Protocol alanı `17` ve hedef port `53`. Yük, alıcıda sırasıyla hangi katmanlardan ve protokollerden geçerek hangi uygulamaya ulaşır?

---

### FND-OSI-005
**Kategori:** İ · **Zorluk:** 3 · **Teori:** 00-09, 00-08

Bir L2 switch ve bir NGFW aynı çerçeveyi inceliyor.

a) Her biri iletim ya da izin kararı verirken en üst hangi katmanın bilgisini okur?
b) Bu farkın güvenlik açısından bir sonucunu bir örnekle açıkla.

---

### FND-OSI-006
**Kategori:** S · **Zorluk:** 2 · **Teori:** 00-09

```
Router# show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol
GigabitEthernet0/0     192.168.10.1    YES manual up                    up
GigabitEthernet0/1     192.168.20.1    YES manual down                  down
GigabitEthernet0/2     192.168.30.1    YES manual administratively down down
```

a) G0/1 ve G0/2'nin durumu sorunun hangi katmanda olduğunu gösterir?
b) Her biri için ilk yapacağın şey nedir?

---

### FND-OSI-007
**Kategori:** O · **Zorluk:** 2 · **Teori:** 00-09

Bir uygulama UDP ile, her datagramda 1472 bayt veri gönderiyor (seçeneksiz IPv4, Ethernet).

a) Ethernet çerçevesinin boyutu ve kabloda kapladığı toplam bayt süresi (preamble, SFD ve IFG dahil) nedir?
b) Kablodaki verimlilik yaklaşık yüzde kaçtır?
c) 100 Mbps'lık bir bağlantıda uygulamanın elde edebileceği en yüksek veri hızı yaklaşık nedir?

---

### FND-OSI-008
**Kategori:** K · **Zorluk:** 2 · **Teori:** 00-09

Kapsülleme ve açma (encapsulation / decapsulation) süreçlerini kendi cümlelerinle anlat. Cevabında şunlar olsun: her katmanın ne eklediği, veri bağlantı katmanının farkı, alıcının yükü bir üst katmana verirken neye baktığı ve bir router'ın bu süreçteki davranışı. (5–8 cümle.)

---

### FND-OSI-009
**Kategori:** KK · **Zorluk:** 2 · **Teori:** 00-09

OSI ve TCP/IP modellerini karşılaştır: aralarındaki iki farkı söyle ve gerçek protokoller TCP/IP ailesinden olduğu hâlde sektörün neden hâlâ OSI'nin katman numaralarını kullandığını açıkla.

---

### FND-OSI-010
**Kategori:** A · **Zorluk:** 2 · **Teori:** 00-09

Bir kullanıcı "web sitesi açılmıyor" diyor. Sırayla şunları kontrol ettin:

1. Bağlantı ışığı yanıyor.
2. `ipconfig` geçerli bir IP adresi, maske ve varsayılan ağ geçidi gösteriyor.
3. `ping 192.168.1.1` (ağ geçidi) başarılı.
4. `ping 8.8.8.8` başarılı.
5. `ping www.example.com` → "Ping request could not find host www.example.com."

a) Sorun büyük olasılıkla hangi katmanda ve hangi hizmettedir?
b) Sıradaki iki kontrolün ne olur?

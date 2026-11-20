# FND-NET: Ağ Temelleri

> Kapsam: 00-08 | 9 soru | Önerilen süre: 25 dakika | Cevaplar: `answers/A-FND-NET.md`
>
> Kurallar ve puanlama: `10-QUESTION-BANK/README.md`. Hesap makinesi kullanma.

---

### FND-NET-001
**Kategori:** MC · **Zorluk:** 1 · **Teori:** 00-08

Aynı yerel ağdaki cihazlar arasında çerçeveleri, hedef MAC adresine bakarak yalnızca ilgili porta ileten cihaz hangisidir?

- A) Hub
- B) L2 switch
- C) Router
- D) Erişim noktası (AP)

---

### FND-NET-002
**Kategori:** MC · **Zorluk:** 2 · **Teori:** 00-08

Bir NGFW'yi (next-generation firewall) geleneksel bir güvenlik duvarından ayıran özellik hangisidir?

- A) Kaynak ve hedef IP adresine göre filtreleme yapması
- B) TCP ve UDP port numaralarına göre filtreleme yapması
- C) Uygulamaları tanıması ve tümleşik saldırı önleme (IPS) sunması
- D) Bağlantıların durumunu izlemesi (stateful çalışması)

---

### FND-NET-003
**Kategori:** MC · **Zorluk:** 1 · **Teori:** 00-08

Bir üniversite kampüsündeki 200 erişim noktasının kanal, güç ve güvenlik ayarlarını tek bir merkezden yöneten bileşen hangisidir?

- A) L3 switch
- B) WLC (wireless LAN controller)
- C) NGFW
- D) PoE switch

---

### FND-NET-004
**Kategori:** MC · **Zorluk:** 2 · **Teori:** 00-08, 00-04

PoE ile ilgili hangi **iki** ifade doğrudur? (İki tane seçin.)

- A) PoE switch güç kaynağıdır (PSE); IP telefon güç alan cihazdır (PD).
- B) PoE kullanan bir kablo yalnızca güç taşır; veri için ikinci bir kablo gerekir.
- C) Switch'in toplam PoE bütçesi aşılırsa bazı portlardaki cihazlar güç alamaz.
- D) PoE, şebeke gibi alternatif akım (AC) kullanır.
- E) PoE yalnızca fiber optik kablolarda çalışır.

---

### FND-NET-005
**Kategori:** O · **Zorluk:** 1 · **Teori:** 00-08

Bir router, 1500 baytlık bir paketi 4 Mbps'lık bir WAN arayüzünden gönderiyor.

a) Paketin iletim (serileştirme) gecikmesi nedir?
b) Aynı paket 1 Gbps'lık bir LAN arayüzünden gönderilseydi iletim gecikmesi ne olurdu?

---

### FND-NET-006
**Kategori:** İ · **Zorluk:** 3 · **Teori:** 00-08

Ofisten başka bir kıtadaki bir bulut sunucusuna ping süresi her zaman yaklaşık 180 ms. Bir yönetici şunu öneriyor: "İnternet hattımızı 100 Mbps'tan 1 Gbps'a çıkaralım, ping 18 ms'ye düşer."

a) Bu beklenti neden yanlış? Gecikmenin dört bileşeniyle açıkla.
b) Hangi durumda hat yükseltmesi ping'i gerçekten düşürebilir? Bunu nasıl anlarsın?

---

### FND-NET-007
**Kategori:** S · **Zorluk:** 2 · **Teori:** 00-08

```
  PC ──── SW1 ──── G0/0 [R1] G0/1 ──── SW2 ──── Sunucu
  10.1.1.10           10.1.1.1   10.2.2.1           10.2.2.20
  MAC: AAAA           MAC: BBBB  MAC: CCCC          MAC: DDDD
```

PC, sunucuya bir ping (ICMP Echo Request) gönderiyor. NAT yok.

a) İsteğin **SW2 ile sunucu arasındaki** bağlantıdaki kaynak MAC, hedef MAC, kaynak IP ve hedef IP değerlerini yaz.
b) Sunucunun cevabının (Echo Reply) **PC ile SW1 arasındaki** bağlantıdaki aynı dört değerini yaz.

---

### FND-NET-008
**Kategori:** KK · **Zorluk:** 2 · **Teori:** 00-08

Bir şirket, 5.000 çalışanının bilgisayarına 2 GB'lık bir yazılım güncellemesini aynı gün dağıtmak istiyor. Tek bir merkezi sunucudan (istemci-sunucu) dağıtmayı ve çalışan bilgisayarlarının güncellemeyi birbirine aktarmasını (P2P) karşılaştır. Her birinin bir güçlü ve bir zayıf yanını söyle ve bu durum için bir tercih yap.

---

### FND-NET-009
**Kategori:** MC · **Zorluk:** 1 · **Teori:** 00-08

Aşağıdaki kuruluş–belge eşleşmelerinden hangisi **yanlıştır**?

- A) IEEE – 802.11 (Wi-Fi)
- B) IETF – RFC 9293 (TCP)
- C) ITU-T – G.711 (PCM ses kodlaması)
- D) IEEE – RFC 791 (IPv4)

# FND-OSI Cevap Anahtarı

> Sorular: `../Q-FND-OSI.md`. Önce soruları çöz, sonra bu dosyayı aç. Puanlama kuralları: `10-QUESTION-BANK/README.md`.

---

### FND-OSI-001
**Cevap:** C

**Açıklama:** Taşıma katmanında TCP'nin veri birimi segment, UDP'ninki datagramdır (adı da "User Datagram Protocol"dür).

**Çeldiriciler:**
- A) Veri bağlantı katmanının PDU'su **çerçevedir**.
- B) Ağ katmanının PDU'su **pakettir**.
- D) Fiziksel katmanın birimi **bittir**; segment L4'e aittir.

**Teori:** → 00-09, Bölüm 3.4

---

### FND-OSI-002
**Cevap:** A ve D

**Açıklama:** DNS (UDP/TCP 53) ve DHCP (UDP 67/68), UDP üzerinde çalışan uygulama protokolleridir. DHCP bir host'un L3 ayarlarını yapılandırsa da kendisi bir uygulama protokolüdür.

**Çeldiriciler:**
- B) ICMP, IP paketinin içinde taşınır (protokol 1) ve IP'nin ayrılmaz parçası sayılır: L3.
- C) ARP doğrudan Ethernet çerçevesinde taşınır (EtherType 0x0806) ve L3'e hizmet eder; L7 değildir.
- E) OSPF, IP'nin içinde taşınan (protokol 89) bir yönlendirme protokolüdür: L3.

**Teori:** → 00-09, Bölüm 3.6

---

### FND-OSI-003
**Cevap:** OSI'de **sunum katmanının (L6)** görevidir. TCP/IP'de ayrı bir sunum katmanı yoktur; bu işler uygulama katmanının içinde ya da uygulama ile TCP arasındaki kütüphanelerde yapılır.

**Açıklama:** **[OSI-TEORİ]** OSI sunum katmanı verinin gösterimiyle (kodlama, sıkıştırma, şifreleme) ilgilenir. **[TCP/IP-GERÇEK]** Örnekler: şifreleme için TLS (çoğunlukla OpenSSL gibi bir kütüphane); sıkıştırma için HTTP'nin `Content-Encoding: gzip` başlığı ya da video kodekleri (H.264).

**Puan:** Katman 0,5; TCP/IP'deki yer ve en az bir doğru örnek 0,5.

**Teori:** → 00-09, Bölüm 3.2 ve 3.6; ayrıntı 06-01, 06-04, 06-06

---

### FND-OSI-004
**Cevap:**
a) **ARP**. Yükte IP başlığı **yoktur**; ARP mesajı doğrudan Ethernet çerçevesinin yüküdür.
b) Ethernet (EtherType 0x0800) → **IPv4** (Protocol 17) → **UDP** (hedef port 53) → **DNS sunucusu**.

**Açıklama:** Her başlıkta, yükün hangi üst protokole ait olduğunu söyleyen bir alan vardır. Alıcı bu alanlara bakarak yükü doğru yere verir: EtherType L2'den L3'e, Protocol alanı L3'ten L4'e, port numarası L4'ten uygulamaya. 0x0806 ARP'nin, 17 UDP'nin, 53 DNS'in değeridir.

**Puan:** Her parça 0,5. (b)'de zincirin bir halkası eksikse 0,25.

**Teori:** → 00-09, Bölüm 3.5 ve 3.6; 00-06, Bölüm 4

---

### FND-OSI-005
**Cevap:**
a) L2 switch **L2** başlığını (hedef MAC adresi) okur. NGFW, L3 ve L4 başlıklarının yanında **L7**'ye kadar (uygulamanın kendisi) bakar.
b) Switch, iletim kararını yalnızca MAC adresine göre verir; çerçevenin içinde zararlı bir uygulama ya da yasaklı bir site trafiği olsa da bunu göremez ve engelleyemez. NGFW ise trafiğin hangi uygulamaya ait olduğunu tanıyabilir; örneğin port 443 üzerinden giden bir dosya paylaşım uygulamasını, aynı porttaki normal web trafiğine izin verirken engelleyebilir.

**Açıklama:** Bir cihazın "hangi katmanda çalıştığı" sorusu, aslında karar verirken hangi başlığa kadar okuduğu sorusudur. Ne kadar yukarıyı okursa o kadar ince politikalar uygulayabilir; bedeli daha fazla işlem gücüdür.

**Puan:** Her parça 0,5.

**Teori:** → 00-09, Bölüm 3.5; 00-08, Bölüm 3.3

---

### FND-OSI-006
**Cevap:**
a) G0/1 **down/down**: L1 sorunu. G0/2 **administratively down/down**: arayüz yönetici tarafından kapatılmış (`shutdown`).
b) G0/1: Kabloyu, karşı cihazı ve portunu kontrol et (L1). G0/2: Arayüz yapılandırma modunda `no shutdown` komutunu ver.

**Açıklama:** `show ip interface brief` çıktısında Status sütunu fiziksel katmanın, Protocol sütunu veri bağlantı katmanının durumunu yansıtır. "administratively down", sorunun bir arıza değil, bir yapılandırma tercihi olduğunu söyler.

```
Router(config)# interface GigabitEthernet0/2
Router(config-if)# no shutdown
```

**Puan:** Her parça 0,5 (iki arayüz de doğru olmalı).

**Teori:** → 00-09, Bölüm 7 ve 9; ayrıntı 01-10

---

### FND-OSI-007
**Cevap:** a) Çerçeve **1518 bayt**; kablodaki toplam **1538 bayt süresi**. b) **≈ %95,7**. c) **≈ 95,7 Mbps**.

**Açıklama:**
a) 1472 (veri) + 8 (UDP) + 20 (IPv4) = 1500 bayt IP paketi. Ethernet başlığı ve FCS (18) ile çerçeve 1518 bayt olur. Preamble ve SFD (8) ile IFG (12) eklenince 1538 bayt süresi.
b) 1472 / 1538 ≈ 0,957.
c) 0,957 × 100 Mbps ≈ 95,7 Mbps. UDP'nin başlığı TCP'ninkinden 12 bayt küçük olduğu için verimlilik 00-09, Bölüm 4.1'deki TCP örneğinden (%94,9) biraz yüksektir.

**Puan:** Her parça 1/3.

**Teori:** → 00-09, Bölüm 4.1

---

### FND-OSI-008
**Örnek cevap:** Gönderen tarafta veri yukarıdan aşağıya iner ve her katman, üstünden aldığı her şeyi açmadan bir yük olarak kabul edip önüne kendi başlığını ekler: TCP başlığıyla segment, IP başlığıyla paket oluşur. Veri bağlantı katmanı başlığın yanında sona bir trailer (Ethernet'te FCS) da ekler ve çerçeve oluşur; fiziksel katman çerçeveyi bitler ve sinyal olarak gönderir. Alan tarafta süreç tersine işler: Her katman kendi başlığını okur, kontrol eder, çıkarır ve yükü bir üst katmana verir. Yükün hangi üst protokole ait olduğunu başlıktaki bir alandan anlar: EtherType, IP'nin Protocol alanı ve port numarası. Bir router çerçeveyi L3'e kadar açar, IP başlığına göre karar verir, TTL'yi azaltır ve paketi yeni bir L2 başlığıyla yeniden kapsülleyerek gönderir.

**Puanlama ölçütü (toplam 1):**

| Ölçüt | Puan |
|---|---|
| Her katmanın kendi başlığını eklediği, üstten geleni değiştirmeden yük saydığı | 0,25 |
| Veri bağlantı katmanının ayrıca trailer (FCS) eklediği | 0,25 |
| Alıcının yükü EtherType / Protocol / port gibi bir alana bakarak yukarı verdiği | 0,25 |
| Router'ın L3'e kadar açıp yeni bir L2 çerçevesiyle yeniden kapsüllediği | 0,25 |

**Not:** "Kapsülleme veriyi şifreler ya da sıkıştırır" ifadesi yanlıştır ve ilk ölçütün puanını sıfırlar (CE-00, soru 10'daki yanılgı).

**Teori:** → 00-09, Bölüm 3.5

---

### FND-OSI-009
**Örnek cevap:** OSI yedi, TCP/IP (RFC 1122) dört katmanlıdır; TCP/IP, OSI'nin üst üç katmanını uygulama katmanında, alt iki katmanını bağlantı katmanında toplar. İkinci fark tarihtir: OSI'de önce model tasarlanıp sonra protokoller yazıldı; TCP/IP'de protokoller önce yazılıp çalıştırıldı, model sonra tarif edildi. Bugün kullanılan protokoller TCP/IP ailesindendir. Ama OSI'nin yedi katmanlı ayrımı, özellikle L1 ile L2'yi ve L4 ile L7'yi ayırdığı için cihazları ve sorunları daha ince tarif etmeye izin verir. Bu yüzden sektör "L2 switch", "L4 yük dengeleyici" gibi adlarda OSI numaralarını ortak dil olarak kullanır.

**Puanlama ölçütü (toplam 1):**

| Ölçüt | Puan |
|---|---|
| Katman sayısı ve eşlemesi doğru | 0,25 |
| İkinci bir geçerli fark (model önce / protokol önce; kim tarafından ve ne zaman; bugünkü kullanım) | 0,25 |
| Gerçek protokollerin TCP/IP ailesinden olduğunu söylüyor | 0,25 |
| OSI numaralarının neden ortak dil olarak kaldığını bir örnekle açıklıyor | 0,25 |

**Teori:** → 00-09, Bölüm 3.2 ve 3.3

---

### FND-OSI-010
**Cevap:**
a) **L7, DNS.** Ad çözümlemesi başarısız; L1–L3 ve İnternet erişimi çalışıyor.
b) (1) `nslookup www.example.com` ile ad çözümlemesini doğrudan test etmek. (2) `ipconfig /all` ile bilgisayarın hangi DNS sunucusunu kullandığına bakmak ve o sunucuya ping atmak ya da `nslookup www.example.com 8.8.8.8` ile başka bir DNS sunucusunu denemek.

**Açıklama:** Kontroller aşağıdan yukarıya bir eleme yapar: Işık (L1), geçerli IP yapılandırması (L3), ağ geçidine ve İnternet'teki bir adrese ping (L3 yolu) çalışıyor. Başarısız olan tek şey, adın IP adresine çevrilmesidir. "could not find host" mesajı, ping'in hiç gönderilmediğini, çünkü hedef adresin bulunamadığını gösterir. Başka bir DNS sunucusuyla çözümleme çalışıyorsa sorun, bilgisayarın kullandığı DNS sunucusundadır.

**Çeldirici düşünceler:** "8.8.8.8'e ping gidiyor, demek ki L3 sorunu" ya da "DNS ağ katmanındadır" sonuçları yanlıştır; DNS bir uygulama katmanı protokolüdür.

**Puan:** (a) 0,5; (b) iki geçerli kontrol 0,5 (bir kontrol 0,25).

**Teori:** → 00-09, Bölüm 3.6 ve 9; ayrıntı 07-02

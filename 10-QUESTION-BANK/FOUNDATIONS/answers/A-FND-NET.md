# FND-NET Cevap Anahtarı

> Sorular: `../Q-FND-NET.md`. Önce soruları çöz, sonra bu dosyayı aç. Puanlama kuralları: `10-QUESTION-BANK/README.md`.

---

### FND-NET-001
**Cevap:** B

**Açıklama:** L2 switch, çerçevenin hedef MAC adresini MAC adres tablosunda arar ve çerçeveyi yalnızca o adresin bağlı olduğu porta gönderir. (Adres tabloda yoksa çerçeveyi flood eder; ayrıntı 02-06.)

**Çeldiriciler:**
- A) Hub adrese bakmaz; bitleri bütün portlara tekrarlar (L1).
- C) Router ağlar **arasında**, IP adresine göre iletir.
- D) AP, kablosuz istemcileri kablolu ağa köprüler; birçok kablolu port arasında MAC tablosuyla iletim yapan cihaz değildir.

**Teori:** → 00-08, Bölüm 3.3

---

### FND-NET-002
**Cevap:** C

**Açıklama:** NGFW, geleneksel güvenlik duvarının yaptıklarına (IP ve porta göre filtreleme, durumlu izleme) ek olarak trafiğin hangi **uygulamaya** ait olduğunu tanır, URL filtreleme ve tümleşik IPS sunar. Böylece "port 443'e izin ver" yerine "bu uygulamaya izin verme" gibi politikalar yazılabilir.

**Çeldiriciler:**
- A, B) IP ve port filtrelemesi geleneksel güvenlik duvarlarının da (hatta basit ACL'lerin de) yaptığı iştir.
- D) Durumlu çalışma bugün geleneksel güvenlik duvarlarında da standarttır; NGFW'yi ayıran özellik değildir.

**Teori:** → 00-08, Bölüm 3.3; ayrıntı 14-01

---

### FND-NET-003
**Cevap:** B

**Açıklama:** WLC, kontrolcü tabanlı (lightweight) AP'leri merkezden yönetir: kanal ve güç ayarları, SSID'ler ve güvenlik politikaları tek yerden yapılır (02-16).

**Çeldiriciler:**
- A) L3 switch VLAN'lar arasında yönlendirme yapar; AP'leri yönetmez.
- C) NGFW trafiği güvenlik politikasına göre denetler.
- D) PoE switch AP'lere güç verir, ama onları yapılandırmaz.

**Teori:** → 00-08, Bölüm 3.3

---

### FND-NET-004
**Cevap:** A ve C

**Açıklama:** PoE'de gücü veren tarafa PSE (power sourcing equipment), gücü alan cihaza PD (powered device) denir. Switch'in bütün portlarına verebileceği toplam bir güç bütçesi vardır; bütçe aşılırsa bazı portlara güç verilmez ve o cihazlar açılmaz.

**Çeldiriciler:**
- B) PoE'nin amacı tam tersidir: Aynı kablo hem veriyi hem gücü taşır.
- D) PoE doğru akım (DC) kullanır; yaklaşık 44–57 V.
- E) PoE bakır kablo gerektirir; fiber elektrik iletmez.

**Teori:** → 00-08, Bölüm 3.3; 00-04, Bölüm 4.1 ve 5

---

### FND-NET-005
**Cevap:** a) **3 ms**. b) **12 µs**.

**Açıklama:** 1500 bayt = 12.000 bit. a) 12.000 / (4 × 10⁶) = 0,003 s = 3 ms. b) 12.000 / 10⁹ = 12 × 10⁻⁶ s = 12 µs. Yavaş WAN hatları, iletim gecikmesinin önemli olduğu yerlerdir; ses paketlerinin büyük veri paketlerinin arkasında beklememesi için QoS bu yüzden gerekir (03-21).

**Puan:** Her parça 0,5.

**Teori:** → 00-08, Bölüm 3.6 ve 4

---

### FND-NET-006
**Cevap:**
a) 180 ms'nin büyük kısmı büyük olasılıkla **yayılma gecikmesidir** ve bant genişliğinden bağımsızdır.
b) Hat şu anda **doluysa** (kuyruklama gecikmesi büyükse) yükseltme ping'i düşürür.

**Açıklama:**
a) Dört bileşen: iletim, yayılma, kuyruklama, işleme. Başka bir kıtaya giden bir yol binlerce kilometredir; yayılma gecikmesi km başına yaklaşık 5 µs'tir ve ancak mesafe kısalırsa azalır. Bir ping paketi küçüktür (onlarca bayt); 100 Mbps'ta bile iletim gecikmesi mikrosaniyeler düzeyindedir, 10 kat hızlanması toplamda fark edilmez. İşleme gecikmesi de mikrosaniyelerdir. Bu yüzden hattı 10 kat hızlandırmak RTT'yi 10'a bölmez.
b) Hat yoğun saatlerde doluyorsa paketler çıkış tamponunda bekler (kuyruklama); bu gecikme bant genişliği artınca azalır. Anlamak için: ping'i hat boşken (gece) ve yoğunken (gün içinde) karşılaştır. Boştayken de 180 ms ise neden mesafedir; yalnızca yoğunken yükseliyorsa neden kuyruklamadır. Traceroute ile gecikmenin hangi atlamada arttığına da bakılabilir (03-11).

**Puan:** (a) 0,5 (yayılmanın bant genişliğinden bağımsız olduğu ve küçük paketlerin iletim gecikmesinin ihmal edilebildiği); (b) 0,5 (kuyruklama + bir ölçüm yöntemi).

**Teori:** → 00-08, Bölüm 3.6 ve 4

---

### FND-NET-007
**Cevap:**

| | Kaynak MAC | Hedef MAC | Kaynak IP | Hedef IP |
|---|---|---|---|---|
| a) İstek, SW2 – Sunucu | CCCC | DDDD | 10.1.1.10 | 10.2.2.20 |
| b) Cevap, SW1 – PC | BBBB | AAAA | 10.2.2.20 | 10.1.1.10 |

**Açıklama:** MAC adresleri yalnızca bir bağlantıda anlamlıdır; R1 her yönde paketi yeni bir çerçeveyle gönderir. (a)'da çerçeveyi R1'in G0/1 arayüzü (CCCC) sunucuya (DDDD) gönderir. (b)'de cevap R1'in G0/0 arayüzünden (BBBB) PC'ye (AAAA) gider. IP adresleri uçtan uca aynı kalır; cevapta yalnızca kaynak ve hedef yer değiştirir. Switch'ler MAC adreslerini değiştirmez.

**Puan:** Her satır 0,5 (dört değerin hepsi doğru olmalı).

**Teori:** → 00-08, Bölüm 3.7

---

### FND-NET-008
**Örnek cevap:** İstemci-sunucu modelinde güncelleme tek bir yerden kontrol edilir; hangi sürümün kime gittiği kolayca izlenir ve dosyanın doğruluğu tek noktada güvenceye alınır. Ama sunucunun 5.000 × 2 GB = 10 TB veri göndermesi gerekir; sunucunun bağlantısı ve diskleri darboğaz olur. P2P'de her bilgisayar indirdiği parçaları diğerlerine de verir; katılımcı arttıkça toplam kapasite artar ve merkezi sunucunun yükü azalır. Ama hangi bilgisayarın neyi kime gönderdiğini denetlemek, güvenlik ve bütünlük kontrolü daha zordur. Bu durum için karma bir yaklaşım uygundur: Sunucu güncellemenin bütünlüğünü (ör. imzayla) güvenceye alır, aynı şubedeki bilgisayarlar ise parçaları kendi aralarında paylaşır.

**Puanlama ölçütü (toplam 1):**

| Ölçüt | Puan |
|---|---|
| İstemci-sunucunun bir güçlü yanı (merkezi kontrol, izlenebilirlik, güvenlik) | 0,25 |
| İstemci-sunucunun zayıf yanı: sunucu yükü/darboğaz (10 TB hesabı ya da benzeri) | 0,25 |
| P2P'nin güçlü (kapasitenin katılımcıyla artması) ve zayıf (denetim/güvenlik) yanı | 0,25 |
| Gerekçeli bir tercih (karma çözüm de kabul) | 0,25 |

**Teori:** → 00-08, Bölüm 3.4; ayrıntı 07-01

---

### FND-NET-009
**Cevap:** D

**Açıklama:** RFC serisi bugün **IETF** tarafından yürütülür. RFC 791 (1981), IETF kurulmadan önce DARPA'nın İnternet programı kapsamında yayımlandı; bugün bir İnternet Standardıdır (STD 5). IEEE ise L1 ve L2 standartlarını (802.3, 802.11, 802.1Q) yayımlar; RFC yayımlamaz.

**Çeldiriciler:**
- A) Doğru eşleşme: 802.11 bir IEEE standardıdır.
- B) Doğru eşleşme: TCP'nin güncel tanımı RFC 9293'tür.
- C) Doğru eşleşme: G.711, ITU-T tavsiyesidir.

**Teori:** → 00-08, Bölüm 3.5

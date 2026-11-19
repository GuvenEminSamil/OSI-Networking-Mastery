# CE-00 Cevap Anahtarı

> Sorular: `../CE-00.md`. Önce soruları çöz, sonra bu dosyayı aç.

## Puanlama

| Puan (40 üzerinden) | Yorum |
|---|---|
| 34–40 | Genel çerçeve sağlam. Faz 1–4'te dikkatini mekanizmalara ve ayrıntılara ver. |
| 24–33 | Çerçeve var ama boşluklar var. Yanlış yaptığın soruların dosyalarını özellikle işaretle. |
| 0–23 | Sorun değil; müfredat sıfırdan kuruyor. Faz 1'i acele etmeden çalış. |

Her cevapta "Derinleştiği yer", o konunun müfredatta işlendiği dosyadır. Yanlış ya da `?` işaretli sorularda bu dosyayı not et.

## Bölüm A

| # | Cevap | Derinleştiği yer |
|---|---|---|
| 1 | Yedi | 00-09 |
| 2 | En üst: Application (L7, Uygulama). En alt: Physical (L1, Fiziksel) | 00-09 |
| 3 | Transport (L4, Taşıma) | 04-03 |
| 4 | Network (L3, Ağ) | 03-01 |
| 5 | Data Link (L2, Veri Bağlantı); daha doğrusu L2'nin MAC alt katmanı | 02-02 |
| 6 | L3. Ama her router arayüzünün L1 ve L2 işlevi de vardır; router ayrıca yönetim için SSH, SNMP gibi L7 protokollerini çalıştırır | 03-07 |
| 7 | L2. L3 switch'ler ayrıca yönlendirme de yapar | 02-06, 03-10 |
| 8 | Paket (IP packet) | 00-09, 08-01 |
| 9 | L2, Data Link | 02-03 |
| 10 | Encapsulation: Göndericide veri aşağı inerken her katman kendi başlığını ekler (L2 ayrıca sona bir trailer, FCS ekler). Decapsulation: Alıcıda veri yukarı çıkarken her katman kendi başlığını işler, çıkarır ve yükü (payload) bir üst katmana verir. Ara cihazlar da bunu kısmen yapar: router bir çerçeveyi L3'e kadar açar ve yeniden kapsüller | 08-01 |

## Bölüm B

**11.** L1, Fiziksel katman.
- *Neden:* Bağlantı ışığı, iki uçtaki PHY'lerin (fiziksel katman yongaları) birbirinin sinyalini algıladığını gösterir. Işık yoksa üst katmanların hiçbiri çalışamaz; aşağıdan yukarıya kontrol burada en verimli yöntemdir.
- *Kontrol edilecekler:* Kablo iki uçta da yerine oturmuş mu; kablo sağlam mı; doğru kablo türü mü; karşı cihaz ve portu açık mı; switch portu yönetimsel olarak kapatılmış (`shutdown`) ya da err-disabled durumunda mı.
- *Puan:* L1 için 1, gerekçe ve en az iki kontrol için 1.
- *Derinleştiği yer:* 01-10, 11-01

**12.** İnternet çalıştığına göre bilgisayarın kendi L1–L3 yapılandırması büyük olasılıkla sağlam. Sorun hedef tarafta ya da arada:
- Hedef bilgisayarın güvenlik duvarı gelen ICMP Echo'yu engelliyor olabilir. Windows'ta bu, özellikle "Ortak" ağ profilinde sık görülür.
- Hedef kapalı, yanlış IP adresi yazıldı ya da hedefin IP/maske/gateway ayarı hatalı (dönüş yolu bozuk).
- İki bilgisayar aslında farklı VLAN'larda ya da alt ağlarda ve aralarında yönlendirme yok.
- Kablosuz ağda "istemci izolasyonu" (client isolation) açık olabilir: AP, istemcilerin birbiriyle konuşmasına izin vermez.
- *Kontrol:* L1–L3 (hedefin IP yapılandırması, ARP tablosu: `arp -a`), ardından host güvenlik duvarı.
- *Puan:* İki makul neden için 1, katman mantığı için 1.
- *Derinleştiği yer:* 03-06, 11-03, 02-15

**13.** 8.8.8.8'e ping gidip geliyorsa İnternet'e kadar L1–L3 yolu çalışıyor. Olası nedenler:
- **DNS:** Alan adı çözümlenemiyor. En olası neden budur. Test: `nslookup <site>`.
- Sitenin portları (TCP 80/443, HTTP/3 için UDP 443) bir güvenlik duvarında ya da proxy'de engelli. Test (Windows): `Test-NetConnection <site> -Port 443`.
- Site kapalı ya da TLS sertifika hatası var; tarayıcıda yanlış proxy ayarı var.
- *Puan:* DNS için 1, ikinci bir makul neden ve test yöntemi için 1.
- *Derinleştiği yer:* 07-02, 08-10

**14.** Varsayılan ağ geçidinin, yani router'ın (192.168.1.1) MAC adresi. 8.8.8.8 yerel ağda değildir (/24 maskesi varsayılırsa). Bu nedenle çerçeve bir sonraki atlamaya, router'a gönderilir. IP başlığındaki hedef adres ise 8.8.8.8 olarak kalır.
- *Puan:* Doğru MAC için 1, gerekçe için 1.
- *Derinleştiği yer:* 03-06, 08-03

**15.** Çerçeveyi, geldiği port hariç aynı VLAN'daki tüm portlara gönderir (unknown unicast flooding). Bu sırada çerçevenin kaynak MAC adresini, geldiği portla birlikte tabloya yazar. Hedef cevap verdiğinde onun adresini de öğrenir; sonraki çerçeveler yalnızca doğru porta gider.
- *Puan:* Flooding için 1, "geldiği port hariç, aynı VLAN" ayrıntısı veya öğrenme için 1.
- *Derinleştiği yer:* 02-06

**16.** Normal yönlendirmede (NAT yokken):
- **L2 başlığının tamamı yenilenir:** Kaynak MAC = router'ın çıkış arayüzünün MAC'i, hedef MAC = bir sonraki atlamanın MAC'i. FCS yeniden hesaplanır.
- **TTL bir azaltılır.** TTL değiştiği için IPv4 başlık checksum'ı yeniden hesaplanır.
- Kaynak ve hedef **IP adresleri değişmez.**
- *Puan:* MAC değişimi için 1, TTL ve checksum için 1.
- *Derinleştiği yer:* 03-07

**17.** SYN, SYN-ACK, ACK.
- *Puan:* Üçü doğru sırayla: 2. Sıra yanlışsa: 1.
- *Derinleştiği yer:* 04-03

**18.** Discover, Offer, Request, Acknowledge (DORA).
- *Puan:* Dördü doğru sırayla: 2. Biri eksik ya da sıra yanlışsa: 1.
- *Derinleştiği yer:* 07-03

**19.** Üç temel amaç: **gizlilik** (veri şifrelenir), **bütünlük** (yolda değiştirilirse fark edilir) ve **kimlik doğrulama** (sunucu kimliği sertifikayla doğrulanır). Bunları sağlamak için TLS el sıkışmasında anahtar değişimi yapılır.
- *Puan:* Üç amaçtan ikisi için 1, üçü için 2.
- *Derinleştiği yer:* 06-05, 06-06

**20.** L3 yönlendirme. Her VLAN ayrı bir yayın alanıdır, dolayısıyla ayrı bir IP alt ağı ve ayrı bir varsayılan ağ geçidi olmalıdır. Uygulama yöntemleri:
- **Router-on-a-stick:** 802.1Q trunk ve VLAN başına alt arayüz.
- **L3 switch:** VLAN başına SVI ve `ip routing`.
- Her VLAN için ayrı fiziksel router arayüzü (eski ve az ölçeklenebilir yöntem).
- *Puan:* "L3 yönlendirme" için 1, bir uygulama yöntemi için 1.
- *Derinleştiği yer:* 03-10

## Bölüm C

**21.** İki adres farklı işler görür:
- **MAC adresi yalnızca tek bir bağlantı (link) üzerinde anlamlıdır.** Görevi, çerçeveyi o bağlantıdaki bir sonraki cihaza ulaştırmaktır. Router gelen çerçeveyi sonlandırır (decapsulation) ve çıkış bağlantısı için yeni bir çerçeve oluşturur. Bu yüzden her atlamada MAC adresleri değişir.
- **IP adresleri uçtan uca kaynak ve hedefi tanımlar.** Yol üzerindeki her router, yönlendirme kararını hedef IP adresine göre verir. Hedef IP değişseydi paket asıl hedefine ulaşamazdı.
- İstisna: NAT, IP adreslerini (ve PAT'ta portları) bilerek değiştirir.
- *Puan:* MAC'in bağlantıya özgü olması için 1, IP'nin uçtan uca rolü ve yönlendirme kararı için 1.
- *Derinleştiği yer:* 03-07, 08-04

**22.** Oyunlarda bayat veri işe yaramaz. Kaybolan bir konum güncellemesinin yeniden gönderilmesi anlamsızdır; bir sonraki güncelleme zaten yoldadır.
- TCP'de kaybolan tek bir segment, arkasından gelen verilerin de uygulamaya teslimini bekletir (head-of-line blocking). Tıkanıklık kontrolü de hızı düşürebilir. Sonuç, gecikme sıçramalarıdır.
- UDP bu mekanizmaları içermez. Uygulama hangi verinin güvenilir, hangisinin "en güncel olan yeter" mantığıyla gideceğini kendisi seçer.
- *Puan:* Gecikme ve bayat veri gerekçesi için 1, head-of-line blocking ya da yeniden iletim maliyeti için 1.
- *Derinleştiği yer:* 04-06

**23.** Büyük olasılıkla bir **L2 döngüsü** ve buna bağlı **yayın fırtınası (broadcast storm)**. Ethernet çerçevesinde IP'deki TTL gibi bir atlama sayacı olmadığından, döngüye giren bir broadcast çerçeve hiç ölmez ve her switch onu çoğaltır. Bu protokol **STP (Spanning Tree Protocol)**'dür; Cisco'da genellikle Rapid PVST+ kullanılır. STP, yedek bağlantıların bir kısmını mantıksal olarak bloke ederek döngüsüz bir ağaç oluşturur. (Daha az olası bir başka neden, sürekli broadcast gönderen arızalı bir cihazdır; storm control bu durumu sınırlar.)
- *Puan:* Döngü ve fırtına için 1, STP için 1.
- *Derinleştiği yer:* 02-11, 02-12

**24.** `192.168.1.0/24`. Router **en uzun önek eşleşmesi (longest prefix match)** kuralını kullanır. İki rota da hedefi kapsar, ama /24 rotası hedefle 24 bitte, /16 rotası 16 bitte eşleşir. Daha uzun önek daha spesifik bir rotadır ve tercih edilir. Bu karar AD ya da metriğe bakılmadan verilir; AD ve metrik yalnızca **aynı önek** için farklı kaynaklardan gelen rotalar arasında seçim yaparken kullanılır.
- *Puan:* Doğru rota için 1, LPM gerekçesi için 1. AD/metrik ayrımı ek bilgidir.
- *Derinleştiği yer:* 03-08

**25.** Host karar vermek için kendi maskesini kullanır:
- `192.168.1.50 AND 255.255.255.0 = 192.168.1.0` ve `192.168.1.10 AND 255.255.255.0 = 192.168.1.0`. Ağ adresleri aynı, yani hedef **yerel**. Host doğrudan hedefin MAC adresini ARP ile sorar.
- `8.8.8.8 AND 255.255.255.0 = 8.8.8.0`. Bu, 192.168.1.0'dan farklı, yani hedef **uzak**. Host çerçeveyi varsayılan ağ geçidine gönderir ve bu yüzden gateway'in MAC adresini ARP ile sorar. IP başlığındaki hedef yine 8.8.8.8'dir.
- Bu kararı router değil, **gönderen host** verir. Notlarındaki §15.2'nin düzeltmesi tam olarak budur (CURRICULUM.md, Bölüm 11.2).
- *Puan:* AND ile yerel/uzak kararı için 1, iki durumda kimin MAC'inin sorulduğu için 1.
- *Derinleştiği yer:* 00-03, 03-06

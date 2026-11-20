# 12-02 Modül Modül Tekrar Kartları (Flashcards by Module)

> Bu dosya bir **başlangıç setidir**. Kendi cümlelerinle yazdığın kartlar daha etkilidir (12-01, Bölüm 3). Anki'ye aktarılmaya hazır sürümleri `12-REVISION/anki/` klasöründedir (sekmeyle ayrılmış, dosya başına bir ders).
>
> Kartlar, ilgili teori dosyası yazıldıkça eklenir. Son güncelleme: 2026-11-20 (00-01 – 00-09).

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

### 00-05 Transistörler ve Dijital Mantık

| Soru | Cevap |
|---|---|
| nMOS ve pMOS transistörlerin kapısına mantık 1 uygulanınca ne olur? | nMOS iletir, pMOS iletmez. İkisi her zaman birbirinin tersini yapar (CMOS'taki "tamamlayıcı"). |
| CMOS bir evirici beklerken neden neredeyse güç harcamaz? | Kararlı durumda transistörlerden biri her zaman kapalıdır; besleme ile toprak arasında doğrudan akım yolu yoktur. Güç esas olarak durum değişirken harcanır. |
| Gürültü payları hangi formüllerle hesaplanır? | NMH = VOH − VIH; NML = VIL − VOL. |
| Klasik TTL seviyelerinde (VOH 2,4 / VIH 2,0 / VIL 0,8 / VOL 0,4 V) gürültü payları nedir? | İki seviye için de 0,4 V. |
| Bir bit SRAM'de ve DRAM'de nasıl saklanır? | SRAM: iki eviricinin halkası (6 transistör). DRAM: bir transistör ve bir kapasitördeki yük. |
| DRAM neden yenileme (refresh) ister? | Kapasitördeki yük zamanla sızar; DDR4'te her hücre en geç 64 ms'de bir okunup yeniden yazılır. |
| Saat sinyali (clock) neden gerekir? | Kapı gecikmeleri yüzünden sonuçlar farklı anlarda hazır olur; saat kenarı, flip-flop'ların sonucu hazır olduğunda ve aynı anda yakalamasını sağlar. |
| Cisco'da running-config ve startup-config nerede durur? | running-config RAM'de (uçucu), startup-config NVRAM'de (kalıcı). Kalıcı yapmak için: copy running-config startup-config. |
| Cisco'da IOS imajı ve açılış programları nerededir? | IOS imajı flash'ta; POST, bootstrap ve ROMMON ROM'da. |

### 00-06 Veri Temsili

| Soru | Cevap |
|---|---|
| 12 bitlik 802.1Q VLAN alanıyla kaç VLAN kullanılabilir? | 4094 (1–4094); 0 ve 4095 ayrılmıştır. |
| Ağ bayt sırası (network byte order) nedir? | Big-endian: Çok baytlı bir değerin en anlamlı baytı önce gönderilir (RFC 791, Ek B). |
| 0x12345678 little-endian bir bellekte hangi bayt sırasıyla durur? | 78 56 34 12. |
| htons() işlevi ne yapar? | 16 bitlik bir değeri (ör. port) host bayt sırasından ağ bayt sırasına çevirir; ntohs() tersini yapar. |
| Nyquist koşulu nedir? | Örnekleme frekansı, sinyaldeki en yüksek frekansın iki katından büyük olmalıdır; yoksa aliasing oluşur. |
| G.711'in 64 kbps'ı nasıl hesaplanır? | 8.000 örnek/s × 8 bit/örnek = 64.000 bit/s. |
| 20 ms paketlemeli bir G.711 görüşmesi Ethernet üzerinde kaç kbps kullanır? | 87,2 kbps: (160 bayt ses + 40 bayt RTP/UDP/IP + 18 bayt Ethernet) × 8 × 50 paket/s. |
| Sıkıştırılmamış 1080p, 30 kare/s video yaklaşık kaç bit/s'tir? | ~1,49 Gbps (1920 × 1080 × 3 bayt × 30 × 8). |
| Bir dosyanın türü neyle belirlenir? | Uzantıyla değil; dosyanın imzasıyla (ör. PNG: 89 50 4E 47 0D 0A 1A 0A) ya da ağda protokolün bildirdiği türle (Content-Type). |

### 00-07 Ağ için Bilgisayar Mimarisi

| Soru | Cevap |
|---|---|
| DMA nedir ve neden gerekir? | NIC'in çerçeveyi CPU'ya sormadan doğrudan RAM'e yazması; CPU'nun her baytı tek tek kopyalamasını önler. |
| RX halka tamponu dolunca ne olur? | NIC yeni gelen çerçeveleri düşürür. Kayıp kabloda değil bilgisayarın içindedir; CRC sayacı artmaz. |
| Kesme birleştirme (interrupt coalescing) nedir? | NIC'in birden fazla çerçeve için tek bir kesme üretmesi; CPU yükünü azaltır, küçük bir gecikme ekler. |
| Linux'ta NAPI nasıl çalışır? | İlk çerçevede kesme gelir; sürücü kesmeleri kapatıp halkayı bir bütçeyle yoklayarak boşaltır; halka boşalınca kesmeleri yeniden açar. |
| Soket nedir? | Bir uygulamanın ağ iletişimi için açtığı uç nokta. Gelen segmentler port numaralarına göre doğru sokete, yani doğru uygulamaya verilir. |
| Kendi bilgisayarında yakaladığın giden paketlerde Wireshark neden "checksum incorrect" der? | Checksum offload: Checksum'ı NIC, Wireshark'ın yakalama noktasından sonra hesaplar. Kablodaki paket doğrudur. |
| 10 Gbps'ta en küçük çerçevelerle saniyede kaç çerçeve gelir? | ~14,88 milyon; her ~67 ns'de bir ((64 + 20) × 8 = 672 bit). |
| Cisco show interfaces çıktısında overrun, ignored ve no buffer neyi gösterir? | Kapasite sorununu: tamponlar yetmiyor. Kablo ve gürültü sorunları ise CRC, frame, runts ve giants ile görünür. |

### 00-08 Ağ Temelleri

| Soru | Cevap |
|---|---|
| Switch ile router arasındaki temel fark nedir? | Switch bir ağın içinde MAC adresine göre iletir ve yayınları geçirir. Router ağlar arasında IP adresine göre iletir ve yayınları durdurur. |
| NGFW'yi geleneksel bir güvenlik duvarından ayıran nedir? | Uygulama tanıma, URL filtreleme ve tümleşik IPS. IP/port filtreleme ve durumlu izleme ikisinde de vardır. |
| IPS ile IDS arasındaki fark nedir? | IPS saldırıyı trafik akarken (inline) engeller; IDS yalnızca uyarı üretir. |
| WLC'nin görevi nedir? | Birçok AP'yi merkezden yönetmek: kanal, güç, SSID ve güvenlik ayarları. |
| PoE'de PSE ve PD nedir? | PSE: gücü veren taraf (ör. switch). PD: gücü alan cihaz (AP, IP telefon, kamera). |
| Gecikmenin dört bileşeni nelerdir? | İletim (serileştirme), yayılma, kuyruklama ve işleme. |
| 1500 baytlık paketin 1 Gbps'taki iletim gecikmesi nedir? | 12.000 bit / 10⁹ bps = 12 µs (formül: boyut / bant genişliği). |
| Bant genişliğini artırmak yayılma gecikmesini değiştirir mi? | Hayır. Yayılma mesafeye ve ortama bağlıdır (bakır ve fiberde ≈ 5 µs/km). |
| Bir paket router'dan geçerken hangi alanlar değişir? | Kaynak ve hedef MAC (her bağlantıda yeni çerçeve) ve TTL. IP adresleri NAT yoksa değişmez. |
| 802.11, TCP (RFC 9293) ve G.711'i hangi kuruluşlar yayımlar? | IEEE, IETF ve ITU-T. |

### 00-09 Katmanlı Modeller: OSI ve TCP/IP

| Soru | Cevap |
|---|---|
| OSI katmanlarını aşağıdan yukarıya sırala. | Fiziksel, Veri Bağlantı, Ağ, Taşıma, Oturum, Sunum, Uygulama. Hatırlatma: "Fiziksel Veri Ağda Taşınır; Oturum Sunumla Uygulanır." |
| RFC 1122'nin dört katmanı nelerdir? | Application, Transport, Internet, Link. |
| L1–L4 katmanlarının PDU adları nelerdir? | L4: segment (TCP) / datagram (UDP); L3: paket; L2: çerçeve; L1: bit. |
| Alıcı, yükü bir üst katmana verirken hangi alanlara bakar? | EtherType (L2 → L3), IPv4 Protocol alanı (L3 → L4), port numarası (L4 → uygulama). |
| Router bir çerçeveyi hangi katmana kadar açar ve neyi değiştirir? | L3'e kadar. Yeni bir L2 başlığı yazar, TTL'yi bir azaltır, IPv4 checksum'ını yeniden hesaplar. |
| ARP'nin katmanı neden tartışmalıdır? | L3'e hizmet eder (IP → MAC), ama IP başlığı olmadan doğrudan Ethernet çerçevesinde taşınır (EtherType 0x0806). |
| DNS hangi katmandadır? | L7 (uygulama); UDP/TCP 53 üzerinde çalışır. |
| Katmanlamanın iki faydası ve bir bedeli nedir? | Faydalar: modülerlik ve bağımsız gelişim, birlikte çalışabilirlik, katman katman arıza giderme. Bedel: başlık yükü, işlev tekrarı. |
| 1460 baytlık TCP yükleriyle Ethernet'in kablodaki verimliliği nedir? | 1460 / 1538 ≈ %94,9 → 1 Gbps'ta ~949 Mbps. |
| show ip interface brief: "administratively down / down" ne demektir? | Arayüz shutdown komutuyla kapatılmıştır; açmak için arayüz modunda no shutdown. |

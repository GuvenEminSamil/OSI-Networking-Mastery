# OSI Networking Mastery — OSI Modeli ve Ağ Mühendisliği Müfredatı

> **Durum:** Müfredat onaylandı (v0.2, 2026-11-19). Hedef: CCNA 200-301 v1.1, en geç 2 Şubat 2027.
> Ders içerikleri, pratikler ve soru bankası faz faz yazılıyor; güncel durum PROGRESS.md'de.
>
> **Bugün ne yapmalıyım?** → [START-HERE.md](START-HERE.md)

## Amaç

Bu kütüphanenin amacı, bir bitin fiziksel temsilinden İnternet üzerindeki iki uygulamanın haberleşmesine kadar, bir ağın içinde **gerçekte ne olduğunu** öğretmektir. Yedi katmanı ezberlemek hedef değildir. Hedef; mekanizmaları açıklayabilmek, ağları yapılandırabilmek, arıza giderebilmek ve teknolojilerin neden öyle davrandığını anlamaktır. Sertifika referansı Cisco CCNA 200-301'dir (bkz. CURRICULUM.md, Bölüm 9).

**Temel ilke:** Bir şeyin yalnızca NE yaptığını değil, NASIL ve NEDEN çalıştığını da açıkla.

## Ana dosyalar

| Dosya | İçerik |
|---|---|
| [CURRICULUM.md](CURRICULUM.md) | **Ne öğrenilecek:** tüm modüller ve dosyalar, önkoşullar, 100 Packet Tracer pratiği (69 yönerge, 31 tam lab), gerçek host ve kod labları, soru bankası tasarımı, CCNA eşlemesi. Dosya listesinin **tek doğruluk kaynağı** budur. |
| [STUDY-ROADMAP.md](STUDY-ROADMAP.md) | **Hangi sırayla ve ne zaman:** 15 faz (0–14) ve tarihli takvim; her fazın dosyaları, pratikleri ve sınavları; ustalık kapıları; günlük şablon; karar noktaları. |
| [PROGRESS.md](PROGRESS.md) | **Nerede kaldık:** içerik üretim durumu, öğrenci ustalık takibi, açık kararlar, bilinen sorunlar. |
| [SOURCES.md](SOURCES.md) | **Neye dayanıyor:** kaynak hiyerarşisi, atıf biçimi, doğrulama yöntemi, kaynak kaydı. |
| `GLOSSARY.md` | Terimler sözlüğü (Türkçe ↔ English). İlk teori dosyasıyla birlikte oluşturulacak. |

## Çalışma döngüsü

1. STUDY-ROADMAP.md'de sıradaki fazı ve dosyayı bul.
2. Teori dosyasını oku ve dosya içindeki "Kendini Kontrol Et" sorularını cevapla.
3. Konuyu kendi cümlelerinle anlat (teach-back): yazılı ya da sesli, kaynağa bakmadan.
4. İlgili Packet Tracer pratiğini (yönerge ya da tam lab) veya host labını **çözüme bakmadan** yap.
5. Soru bankasındaki ilgili soruları çöz ve ayrı cevap anahtarıyla kontrol et.
6. Tekrar kartlarını aralıklı tekrar takvimine ekle (bkz. STUDY-ROADMAP.md, Bölüm 5).
7. PROGRESS.md'deki ustalık seviyeni güncelle. Okumak tek başına ustalık sayılmaz.

## Dizin yapısı

Dizin numaraları konuyu gruplar; **çalışma sırasını STUDY-ROADMAP.md belirler.** Örneğin `11-TROUBLESHOOTING` içindeki metodoloji dosyası Faz 2'de okunur, sona bırakılmaz.

```
OSI-Networking-Mastery/
├── START-HERE.md                   Günlük çalışma rehberi: "bugün ne yapmalıyım?"
├── README.md, CURRICULUM.md, STUDY-ROADMAP.md, PROGRESS.md, SOURCES.md, GLOSSARY.md
├── MY-NOTES/                       Senin notların: günlük, CE-00 cevapların, teach-back, sorular
├── 00-FOUNDATIONS/                 Bilgi, ikili sistem, Boole mantığı, elektrik, transistör, veri temsili,
│                                   bilgisayar mimarisi, ağ temelleri, OSI ve TCP/IP modelleri
├── 01-PHYSICAL-LAYER/              Sinyaller, hat kodlaması, bit senkronizasyonu, bakır, fiber, RF, Ethernet PHY
├── 02-DATA-LINK-LAYER/             Ethernet çerçevesi, MAC, CRC, switch, VLAN, trunk, ARP, STP, EtherChannel, Wi-Fi MAC
├── 03-NETWORK-LAYER/               IPv4/IPv6, subnetting, iletim, yönlendirme, OSPF, ICMP, MTU, FHRP, NAT, QoS
├── 04-TRANSPORT-LAYER/             Portlar, soketler, UDP, TCP (güvenilirlik, akış ve tıkanıklık kontrolü)
├── 05-SESSION-LAYER/               OSI teorisi ve bu işlevlerin modern protokollerdeki karşılıkları
├── 06-PRESENTATION-LAYER/          Karakter kodlama, serileştirme, sıkıştırma, kriptografi, TLS
├── 07-APPLICATION-LAYER/           DNS, DHCP, HTTP(S), e-posta, SSH, dosya aktarımı, NTP, SNMP, syslog, REST
├── 08-CROSS-LAYER-COMMUNICATION/   Katmanların birlikte çalıştığı uçtan uca senaryolar
├── 09-PACKET-TRACER-LABS/          100 pratik: DRILLS/ (69 yönerge, answers/) ve BEGINNER/, INTERMEDIATE/,
│                                   ADVANCED/, EXPERT/ (31 tam lab, her birinde solutions/)
├── 10-QUESTION-BANK/               Konu klasörleri + COMPREHENSIVE-EXAMS/ (her birinde answers/)
├── 11-TROUBLESHOOTING/             Metodoloji, Cisco ve host araçları, belirti → neden kataloğu, vaka çalışmaları
├── 12-REVISION/                    Aralıklı tekrar rehberi, tekrar kartları, özet kartlar (cheat sheets)
├── 13-CCNA-EXAM-PREPARATION/       Kapsama matrisi, sınav stratejisi, boşluk analizi, hazırlık kontrol listesi
├── 14-SECURITY-FUNDAMENTALS/       [YENİ] Güvenlik kavramları, AAA, ACL, L2 saldırı/savunma, IPsec, kablosuz güvenlik
├── 15-NETWORK-OPERATIONS-AUTOMATION-AI/  [YENİ] Mimariler, sanallaştırma, yönetim yaklaşımları, SDN, Ansible, AI
└── 16-REAL-HOST-LABS/              [YENİ] HOST/ (Wireshark, Windows/macOS/Linux, Docker, Ansible) ve
                                    CODE/ ("Kodla-Anla" Python alıştırmaları), her birinde solutions/
```

`[YENİ]` ile işaretli dizinler önerilen yapıya eklendi. Gerekçeleri CURRICULUM.md, Bölüm 10'da.

## İçerik kuralları

### Dil

- Anlatım Türkçedir. Önemli bir terim ilk kez geçtiğinde Türkçe karşılığı ve İngilizcesi birlikte yazılır: **Çerçeve (Frame)**, **Bant Genişliği (Bandwidth)**.
- Türkçede yerleşmiş karşılığı olmayan ya da sektörde İngilizcesiyle kullanılan terimler İngilizce bırakılır: *trunk*, *native VLAN*, *router ID*.
- Komutlar, çıktılar, protokol alan adları ve dosya adları İngilizce kalır.

### Etiketler

Etiketler metin olarak yazılır, böylece `grep` ile aranabilir.

| Etiket | Anlamı |
|---|---|
| `[TEMEL]` | Konuyu anlamak için zorunlu bilgi |
| `[DERİN]` | İsteğe bağlı derin bilgi. Atlanabilir, sonraki konular buna dayanmaz |
| `[BASİTLEŞTİRME]` | Öğretim amaçlı basitleştirme. Neyin basitleştirildiği hemen yanında yazılır |
| `[OSI-TEORİ]` | ISO OSI modelinin tanımı. Gerçek protokoller bundan farklı olabilir |
| `[TCP/IP-GERÇEK]` | İnternet protokol yığınının gerçek davranışı (RFC'ler) |
| `[STANDART]` | IEEE, IETF, ISO veya ITU standardına dayanan genel kural |
| `[CISCO-ÖZEL]` | Cisco'ya özgü davranış, varsayılan değer veya komut |
| `[PT-SINIRI]` | Packet Tracer'ın gerçek ağdan farklı davrandığı ya da desteklemediği nokta |
| `[v2.0-FARK]` | Yalnızca CCNA v2.0'da olan konu. v1.1 sınavından önce atlanabilir (Faz 14) |
| `[CCNA v1.1 x.y]` / `[CCNA v2.0 x.y]` | İlgili resmi sınav konusu |

### Teori dosyası şablonu

Her bölüm her konuya uymaz; ilgisiz bölüm zorla eklenmez.

```
# MM-NN Türkçe Başlık (English Title)
> Önkoşullar: MM-NN, ... | Tahmini süre: ... | CCNA: v2.0 x.y · v1.1 x.y

## Öğrenme Hedefleri
## 1. Sezgisel Giriş            sade dille ve somut bir örnekle
## 2. Neden Var?                çözdüğü problem, tarihçe
## 3. Mekanizma                 nasıl çalışır; neden-sonuç zinciri
## 4. Teknik Ayrıntı            başlık formatları, alanlar, standartlar
## 5. Gerçek Dünya Örnekleri    ev ağı, oyun, video akışı, veri merkezi, kurum ağı
## 6. Diğer Konularla Bağlantı  komşu katmanlar ve ilgili teknolojiler
## 7. Cisco ve Pratik           komutlar, çıktı okuma
## 8. Yaygın Yanılgılar
## 9. Arıza Giderme Yaklaşımı
## 10. CCNA Bağlantısı
## 11. Kendini Kontrol Et       cevaplar katlanmış <details> bloklarında
## 12. Uygulama                 ilgili LAB-, H- ve K- labları
## 13. Ustalık Kontrol Listesi  ölçülebilir maddeler
## Kaynaklar                    SOURCES.md kimlikleriyle, bölüm numarasına kadar
```

Bir dosya başka bir dosyada açıklanmış bir kavrama dayanıyorsa, açıklama tekrarlanmaz. Kimliğiyle bağlantı verilir: "(bkz. 02-06, Bölüm 3)". Tanımlar GLOSSARY.md'de tutulur.

### Pratik türleri

Packet Tracer pratiklerinin çoğu **yönerge**dir; tasarımı sen yaparsın. **Tam lab** yalnızca verilmesi gereken bir şey olduğunda kullanılır (hatalı yapılandırma, kesin gereksinim listesi, hatalı diyagram). Hangi pratiğin hangi türde olduğu CURRICULUM.md, Bölüm 4.5'teki "Tür" sütunundadır.

### Yönerge şablonu

Bir fazın bütün yönergeleri tek dosyadadır (`DRILLS/DRILLS-FNN.md`); cevaplar ayrı dosyadadır (`DRILLS/answers/DRILLS-FNN-ANSWERS.md`).

```
### LAB-013 · MAC adres tablosu: öğrenme, yaşlanma, flooding
**Yönerge:** Bir switch'e dört PC bağla. Tablo boşken PC1'den PC3'e ping at ve
MAC tablosunun nasıl dolduğunu adım adım izle; ardından aging süresini değiştir.
**Başarı ölçütü:** Her adımdan önce tablonun içeriğini doğru tahmin etmek.
**İpucu:** (katlanmış) kullanılacak komutların adları
**Teori:** 02-06 · **CCNA:** v1.1 1.13
```

Cevap dosyası her yönerge için örnek bir çözüm, çözümün neden çalıştığını ve varsa `[PT-SINIRI]` notunu içerir. Senin çözümün farklı olabilir; ölçüt, başarı koşulunun sağlanmasıdır.

### Tam lab şablonu

Görev dosyası ile çözüm dosyası **ayrıdır**; görev dosyası çözüm içermez.

Görev dosyası: (1) numara ve başlık, (2) zorluk, (3) öğrenme hedefleri, (4) ilgili OSI katmanları, (5) gerekli PT cihazları, (6) topoloji tarifi ve diyagramı, (7) cihaz bağlantıları, (8) IP adresleme tablosu, (9) yapılandırma gereksinimleri, (10) adım adım görevler, (11) beklenen sonuçlar, (12) doğrulama komutları, (13) arıza giderme görevleri, (14) kademeli ipuçları (katlanmış).

Çözüm dosyası: (15) tam çözüm, (16) çözümün neden çalıştığı, (17) ilgili CCNA kavramları, ayrıca bilinen `[PT-SINIRI]` notları.

### Sorular

Pratik testlerde cevaplar soruların yanında **yer almaz**; her soru dosyasının ayrı bir `answers/` dosyası vardır. Cevap dosyası şunları içerir: doğru cevap, ayrıntılı açıklama, yanlış seçeneklerin neden yanlış olduğu ve teori dosyasına bağlantı. Teori dosyalarındaki kısa "Kendini Kontrol Et" soruları pratik test sayılmaz; cevapları katlanmış blokta durur.

### Diyagramlar

- Akış, sıra ve topoloji için Mermaid (`flowchart`, `sequenceDiagram`) kullanılır.
- Başlık formatları (Ethernet, IPv4, TCP) için RFC tarzı ASCII bit diyagramı kullanılır. Alan sınırlarını Mermaid'den daha doğru gösterir.
- Süs amaçlı diyagram eklenmez. Her diyagramın altında "ne görüyoruz" notu bulunur.

### Kimlik (ID) kuralları

| Tür | Kimlik | Konum |
|---|---|---|
| Teori | `MM-NN` (ör. `03-04`) | `03-NETWORK-LAYER/04-Subnetting-Binary-Method.md` |
| PT yönergesi (Y) | `LAB-001` … `LAB-100` | `09-PACKET-TRACER-LABS/DRILLS/DRILLS-F02.md` → `DRILLS/answers/DRILLS-F02-ANSWERS.md` (faz numarasıyla) |
| PT tam labı (T) | `LAB-011` gibi | `09-PACKET-TRACER-LABS/<SEVİYE>/LAB-011-<slug>.md` → `<SEVİYE>/solutions/LAB-011-<slug>-SOLUTION.md` |
| Host labı | `H01` … `H19` | `16-REAL-HOST-LABS/HOST/H01-<slug>.md` (+ `solutions/`) |
| Kod labı | `K01` … `K08` | `16-REAL-HOST-LABS/CODE/K01-<slug>.md` (+ `solutions/`) |
| Soru | `<ALAN>-<KONU>-NNN` (ör. `NET-SUB-014`) | `10-QUESTION-BANK/NETWORK/Q-NET-SUB.md` → `answers/A-NET-SUB.md` |
| Tanı testi ve kapsamlı sınav | `CE-00` (tanı), `CE-01` … `CE-06` | `10-QUESTION-BANK/COMPREHENSIVE-EXAMS/CE-01.md` → `answers/CE-01-ANSWERS.md` |

Alan kodları: `FND` temeller, `PHY` fiziksel, `DL` veri bağlantı, `NET` ağ, `TRN` taşıma, `SES` oturum, `PRS` sunum, `APP` uygulama, `SEC` güvenlik, `OPS` operasyon/otomasyon/AI.

## Sınırlar ve dürüstlük notları

- **Claude bu ortamda Packet Tracer çalıştıramaz.** Komutlar Cisco belgelerine ve bilinen PT davranışına göre yazılır ve PT durum etiketiyle işaretlenir (bkz. SOURCES.md, Bölüm 3). Senin PT'de denediğin sonuçlar PROGRESS.md'deki "Bilinen Sorunlar" bölümüne girer ve dosya düzeltilir.
- **`.pkt` dosyası üretilmez** (kapalı, ikili bir format). Topolojiyi tariften sen kurarsın; bu, öğrenmenin bir parçasıdır. Arıza avı (break-fix) lablarında hatalı yapılandırmalar metin olarak verilir ve CLI'ya yapıştırılır.
- Fiziksel sinyaller, gerçek işletim sistemi istemcileri, Ansible ve SCP/SFTP gibi konular PT'de simüle edilemez ya da sınırlıdır. Bunlar için `16-REAL-HOST-LABS` alternatifleri ve kavramsal alıştırmalar vardır.
- Bu müfredatı tamamlamak **tek başına CCNA sınavını geçmeyi garanti etmez.**

## Yeni oturumda çalışmaya devam etme protokolü

Her yeni oturum boş bir çalışma alanıyla başlar. Bu yüzden proje GitHub'daki bir depoda tutulur; her oturum depodan okur ve değişiklikleri depoya yazar. Devam ederken:

1. **MY-NOTES/LOG.md** ve **MY-NOTES/QUESTIONS.md**'yi oku: öğrencinin son durumu ve soruları. Soruları cevapla, PROGRESS.md'yi günlüğe göre güncelle.
2. **PROGRESS.md**'yi oku: mevcut faz, sıradaki dosya, açık kararlar, bilinen sorunlar.
3. **CURRICULUM.md**'de ilgili satırı bul: kapsam, önkoşullar, CCNA kodu.
4. Önkoşul dosyalarının yalnızca ilgili bölümlerine ve **GLOSSARY.md**'ye bak. Tanım yeniden yazılmaz, bağlantı verilir.
5. Dosyayı yaz, yeni kaynakları **SOURCES.md**'ye, yeni terimleri **GLOSSARY.md**'ye ekle, ardından **PROGRESS.md**'yi güncelle.
6. Tamamlanmış dosyalar yalnızca düzeltme gerektiğinde yeniden yazılır. Düzeltme PROGRESS.md'deki değişiklik günlüğüne işlenir.

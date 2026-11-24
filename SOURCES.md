# Kaynaklar ve Araştırma Metodolojisi (Sources)

> Bu dosya iki şeyi tanımlar: (1) içeriklerin nasıl araştırılıp doğrulanacağı ve (2) kullanılan kaynakların kimlikli kaydı. İçerik dosyaları kaynaklara buradaki kimliklerle atıf yapar.
>
> Durum: Taslak v0.1 (2026-11-19).

## 1. Araştırma metodolojisi

### 1.1 Kaynak hiyerarşisi

| Düzey | Kaynak türü | Kullanım |
|---|---|---|
| 1 | Cisco resmi belgeleri ve CCNA sınav konuları | Sınav kapsamı, Cisco komutları, Cisco'ya özgü davranış ve varsayılanlar |
| 2 | IEEE standartları ve diğer teknik standartlar (TIA, ISO/IEC, ITU-T) | L1/L2 davranışı, çerçeve formatları, kablolama |
| 3 | IETF RFC'leri ve IANA kayıtları | IP ve üstü protokollerin davranışı, adres blokları, port numaraları |
| 4 | Diğer üreticilerin resmi belgeleri (işletim sistemleri, Wireshark, Ansible, OpenSSL) | Host labları ve araç kullanımı |
| 5 | Saygın ders kitapları | Kavramsal açıklama ve ek okuma |
| 6 | Güvenilir eğitim kaynakları | Yalnızca çapraz kontrol ve pedagojik örnek |

### 1.2 Doğrulama iş akışı

1. **Her önemli teknik iddia** en az bir Düzey 1–3 kaynağa dayanır. Atıf mümkün olduğunda bölüm numarasına kadar verilir.
2. **Sayısal değerler** (alan boyutları, zamanlayıcılar, varsayılan değerler, port numaraları) birincil kaynaktan alınır. Cisco'ya özgü varsayılanlar Cisco belgesinden alınır ve `[CISCO-ÖZEL]` ile işaretlenir.
3. **Komutlar** Cisco komut referansıyla kontrol edilir ve PT durum etiketi alır (Bölüm 3). IOS ile IOS XE arasında sözdizimi farkı varsa belirtilir.
4. **İkincil kaynaklar** (Düzey 5–6) tek başına dayanak olmaz; yalnızca çapraz kontrol veya açıklama için kullanılır.
5. **Çelişki** durumunda birincil kaynak esas alınır ve fark, ilgili dosyada "Kaynaklar arasında fark" notuyla belirtilir.
6. **Basitleştirmeler** `[BASİTLEŞTİRME]` ile işaretlenir ve gerçek davranış kısa bir notla verilir.
7. **Doğrulanamayan bilgi yazılmaz.** Gerekliyse "doğrulanamadı" diye işaretlenir ve PROGRESS.md'deki "Doğrulama bekleyenler" bölümüne eklenir.
8. **Katman yerleşimi:** Bir protokolün işlevleri birden fazla katmana yayılıyorsa (ARP, TLS, DHCP, OSPF), tek bir katmana aitmiş gibi sunulmaz. OSI teorisi `[OSI-TEORİ]`, gerçek uygulama `[TCP/IP-GERÇEK]` ile ayrılır.

### 1.3 Bilinen sınırlar

- **Packet Tracer:** Claude bu ortamda PT çalıştıramaz. PT desteği bilinen davranışa ve belgelere göre etiketlenir; kesin doğrulama senin PT'de yapacağın denemeyle olur (🧪 etiketi).
- **IEEE standartları:** Tam metinler ücretli olabilir. IEEE GET Program üzerinden ücretsiz erişim mümkün olabilir; koşulları kontrol edilecek. Doğrulanamayan bir madde (clause) numarası verilmez.
- **Ders kitapları:** Bu oturumda kitapların metnine erişim yok. Kitaplar ek okuma önerisidir ve bir iddianın tek dayanağı olarak kullanılmaz.
- **Dinamik web sayfaları:** Bazı Cisco sayfaları JavaScript ile yüklendiği için doğrudan okunamadı. Bu durumda aynı içeriğin resmi PDF'i kullanıldı ya da konu "Açık" olarak işaretlendi.

## 2. Atıf biçimi (içerik dosyalarında)

| Kaynak | Biçim | Örnek |
|---|---|---|
| RFC | `[RFC numara §bölüm]` | `[RFC 9293 §3.5]` |
| IEEE | `[IEEE numara, Cl. madde]` | `[IEEE 802.3, Cl. 25]` (madde numarası doğrulandıysa) |
| Cisco belgesi | `[CISCO: kimlik, bölüm]` | `[CISCO: CISCO-V2, 3.3]` |
| Ders kitabı | `[kimlik, bölüm]` | `[TXT-STEVENS, Bölüm 13]` |
| CCNA sınav konusu | `[CCNA sürüm kod]` | `[CCNA v2.0 3.3]` |

Her içerik dosyası "Kaynaklar" başlığıyla biter ve kullandığı kimlikleri listeler. Yeni bir kaynak önce buraya eklenir, sonra kullanılır.

## 3. Durum etiketleri

### 3.1 Packet Tracer desteği

| Etiket | Anlamı |
|---|---|
| ✅ | PT'de desteklendiği biliniyor; lab yazılırken komut düzeyinde yine kontrol edilir |
| ⚠️ | Destek kısmi ya da belirsiz; lab yazılmadan önce doğrulanacak, gerekirse alternatife geçilecek |
| ❌ | PT'de yok; alternatif (`H`, `K` veya kavramsal alıştırma) kullanılır |
| 🧪 | Senin tarafından PT'de test edildi (sürüm numarasıyla birlikte PROGRESS.md'ye yazılır) |

### 3.2 Kaynak erişim durumu

| Durum | Anlamı |
|---|---|
| Okundu | Kaynak bu projede doğrudan okundu (erişim tarihiyle) |
| Planlandı | İlgili dosya yazılırken okunacak |
| Açık | Erişilemedi ya da içerik henüz doğrulanmadı |

## 4. Kaynak kaydı

### 4.1 Planlama aşamasında kullanılan kaynaklar (erişim: 2026-11-19)

| Kimlik | Kaynak | Düzey | Durum | Kullanım |
|---|---|---|---|---|
| USR-OSI-NOTES | Kullanıcının kendi notları: *OSI Modeli (Open Systems Interconnection) — Bilgisayar Ağlarının 7 Katmanlı Yapısı, Kapsamlı Çalışma Notları* (`OSI.docx`, 20 bölüm) | — (kullanıcı materyali; teknik dayanak değildir) | Okundu | Başlangıç düzeyi, CE-00 tanı testi, yanılgı listesi, bölüm eşlemesi (CURRICULUM.md, Bölüm 11) |
| CISCO-V2 | Cisco, *Implementing and Administering Cisco Solutions (200-301 CCNA) v2.0 — Exam Topics* (PDF). https://learningcontent.cisco.com/documents/marketing/exam-topics/200-301_CCNA_v2.0_Exam_Topics_PDF.pdf | 1 | Okundu | v2.0'ın alanları, ağırlıkları ve 29 konusu |
| CISCO-V2-PAGE | Cisco Learning Network, CCNA v2.0 Exam Topics. https://learningnetwork.cisco.com/s/ccna-v2-exam-topics | 1 | Okundu (arama özeti) | v2.0'ın ilk sınav tarihi: 3 Şubat 2027. Sayfa gövdesi JavaScript ile yüklendiği için okunamadı; içerik CISCO-V2'den alındı |
| CISCO-V11 | Cisco, *CCNA Exam v1.1 (200-301)* (PDF). https://learningcontent.cisco.com/documents/marketing/exam-topics/200-301-CCNA-v1.1.pdf | 1 | Okundu | **Birincil hedef.** v1.1'in 6 alanı, ağırlıkları, 53 konusu ve alt maddeleri |
| CISCO-V11-PAGE | Cisco Learning Network, CCNA Exam Topics (v1.1). https://learningnetwork.cisco.com/s/ccna-exam-topics | 1 | Okundu (arama özeti) | v1.1'in son sınav günü: 2 Şubat 2027 |
| CISCO-POLICY | Cisco, *Exam, Testing, and Certification Policies*. https://www.cisco.com/site/us/en/learn/training-certifications/exams/policies.html | 1 | Okundu (arama özeti) | Yaptırım uygulanan ülkelerde ikamet edenlerin sınava girme kısıtlaması (Rusya dahil) |
| SEC-PV-RU | The Open Group, *FAQ — Exam Based Certifications*. https://www.opengroup.org/certifications/faqs | 6 | Okundu (arama özeti) | Pearson VUE'nun 7 Mart 2022'den beri Rusya'da test merkezi ve OnVUE dahil tüm sınav hizmetlerini askıya alması |
| SEC-V11-LIST | computingforgeeks, *CCNA 200-301 Exam Topics: The Complete v1.1 List Explained*. https://computingforgeeks.com/ccna-exam-topics/ | 6 | Okundu | v1.1'in 53 konusu ve alan ağırlıkları (yazarın özetleri, Cisco'nun birebir metni değil) |
| SEC-V2-DATES | NetworkLessons, *CCNA 200-301*. https://networklessons.com/cisco/ccna-200-301 · Cisnet, *CCNA v2.0 vs v1.1*. https://www.cisnet.ca/blog/ccna-v2-0-vs-v1-1 | 6 | Okundu | Duyuru tarihi (20 Mayıs 2026), v1.1'in son sınav günü (2 Şubat 2027), v2.0'ın başlangıcı (3 Şubat 2027); eklenen ve çıkarılan konular |
| SEC-V2-LIST | CertRamp Learning, *CCNA 200-301 Exam Guide*. https://certramplearning.com/guides/ccna-200-301/ | 6 | Okundu | v2.0 konu listesinin çapraz kontrolü |
| SEC-OCG-V11 | Cisco Press, *CCNA 200-301 Official Cert Guide, Volume 2, 2nd Edition* (Odom, Hucaby, Gooley), 22 Temmuz 2024. https://www.ciscopress.com/title/0138215049 | 5 | Okundu (yayıncı sayfası) | v1.1 için resmi çalışma kitabının varlığı ve kapsamı |
| SEC-PT-VER | Packet Tracer sürüm bilgisi: https://packettracernetwork.com/ · https://www.computernetworkingnotes.com/ccna-study-guide/download-packet-tracer-for-windows-and-linux.html | 6 | Okundu | PT 9.0.0'ın yayımlandığı ve 8.2.2'nin önceki sürüm olduğu. Bir kaynak, CCNA hazırlığı için 8.2.2'yi hâlâ kararlı sürüm olarak öneriyor. Resmi sürüm notlarıyla (NetAcad) doğrulanacak |

### 4.2 Cisco birincil kaynakları (planlandı)

| Kimlik | Kaynak | Kullanım |
|---|---|---|
| CISCO-CFG | Catalyst 2960, 3650 ve 9000 serisi; ISR 1900, 2900 ve 4000 serisi yapılandırma kılavuzları ve komut referansları (IOS 15 ve IOS XE). URL'ler ilgili dosya yazılırken eklenecek | Komutlar, varsayılan değerler, doğrulama çıktıları |
| CISCO-PT | Cisco Packet Tracer resmi belgeleri ve sürüm notları (NetAcad) | Cihaz modelleri, desteklenen özellikler |
| CISCO-NETACAD | Cisco Networking Academy (NetAcad) CCNA kurs materyalleri. https://www.netacad.com | PT kurulumu, Simulation Mode |
| CISCO-WLC | Cisco WLC yapılandırma kılavuzları | 02-16, LAB-071 |
| CISCO-DESIGN | Cisco kampüs tasarım rehberleri | 15-01 |

### 4.3 IETF RFC'leri (planlandı)

Tüm RFC'ler `https://www.rfc-editor.org/rfc/rfcNNNN` adresindedir. Bir RFC yerini yenisine bıraktıysa güncel olan kullanılır (ör. TCP için RFC 793 değil, RFC 9293).

| Alan | RFC'ler | İlgili dosyalar |
|---|---|---|
| Mimari ve katmanlar | 1122 (host gereksinimleri: iletişim katmanları), 1123 (uygulama ve destek), 3439 (mimari ilkeler; katmanlaşmanın sınırları) | 00-09, 05-02 |
| ARP ve L2 ilişkisi | 826 (ARP), 5227 (IPv4 adres çakışması tespiti, gratuitous ARP), 1661 (PPP) | 02-01, 02-10 |
| IPv4 | 791 (IPv4), 792 (ICMP), 1071 (İnternet checksum'ının hesaplanması), 1191 (PMTUD), 1812 (IPv4 router gereksinimleri), 1918 (özel adresler), 3021 (/31), 3927 (IPv4 link-local), 4632 (CIDR), 5737 (dokümantasyon adresleri), 6598 (paylaşılan adres alanı), 6890 (özel amaçlı adres kayıtları) | 03-02 – 03-12 |
| QoS ve ECN | 2474 (DSCP), 3168 (ECN) | 03-02, 03-21, 04-05 |
| Yönlendirme ve FHRP | 2328 (OSPFv2), 5340 (OSPFv3), 2453 (RIPv2), 4271 (BGP-4), 2281 (HSRP, bilgilendirme amaçlı), 5798 (VRRPv3) | 03-13 – 03-19 |
| NAT | 2663 (NAT terminolojisi), 3022 (geleneksel NAT) | 03-20 |
| IPv6 | 8200 (IPv6), 4291 (adresleme mimarisi), 5952 (metin gösterimi), 4193 (ULA), 3849 (dokümantasyon öneki), 4443 (ICMPv6), 4861 (NDP), 4862 (SLAAC), 8981 (geçici adresler), 8415 (DHCPv6), 8201 (IPv6 PMTUD), 6105 (RA Guard) | 03-16 – 03-18, 14-04 |
| Taşıma | 768 (UDP), 9293 (TCP), 5681 (tıkanıklık kontrolü), 6298 (RTO), 7323 (yüksek performans uzantıları, window scaling), 2018 (SACK), 9000 (QUIC), 9260 (SCTP), 6335 (port numarası prosedürleri) | 04-* |
| Sunum ve güvenlik | 8446 (TLS 1.3), 3629 (UTF-8), 8259 (JSON), 4648 (Base64), 1951 (DEFLATE), 1952 (gzip), 5280 (X.509 PKI), 4301 (IPsec mimarisi), 4303 (ESP), 7296 (IKEv2), 2784 (GRE) | 06-*, 14-05 |
| DNS | 1034, 1035 (DNS), 3596 (AAAA), 7858 (DNS over TLS), 8484 (DNS over HTTPS) | 07-02 |
| DHCP | 2131 (DHCP), 2132 (DHCP seçenekleri), 1542 (BOOTP relay açıklamaları) | 07-03 |
| Web | 9110 (HTTP semantiği), 9112 (HTTP/1.1), 9113 (HTTP/2), 9114 (HTTP/3), 3986 (URI), 6265 (çerezler), 6797 (HSTS) | 07-04, 07-11 |
| E-posta | 5321 (SMTP), 6409 (mesaj gönderimi, port 587), 8314 (e-postada örtük TLS, port 465), 1939 (POP3), 9051 (IMAP4rev2) | 07-05 |
| Uzaktan erişim ve dosya | 854 (Telnet), 4251–4254 (SSH), 959 (FTP), 1350 (TFTP) | 07-06, 07-07 |
| Yönetim | 5905 (NTPv4), 3411–3418 (SNMPv3 çerçevesi), 5424 (syslog), 2865 (RADIUS), 8907 (TACACS+) | 07-08, 07-09, 14-02 |

**Not:** SFTP ve SCP için yayımlanmış bir RFC yoktur. SFTP, IETF taslağı (draft-ietf-secsh-filexfer) ve OpenSSH belgeleriyle anlatılacak.

### 4.4 IEEE ve diğer standartlar (planlandı)

| Kimlik | Standart | İlgili dosyalar |
|---|---|---|
| IEEE-8023 | IEEE 802.3 Ethernet (PHY'ler, autonegotiation, MAC, PoE dahil) | 01-03, 01-06, 01-09, 02-03, 02-05 |
| IEEE-8021Q | IEEE 802.1Q (VLAN köprüleme; güncel sürümleri 802.1D köprüleme ve RSTP/MSTP içeriğini de kapsar) | 02-06, 02-08, 02-09, 02-11, 02-12 |
| IEEE-8021D | IEEE 802.1D-2004 (tarihsel STP ve RSTP; 802.1w bu sürüme dahil edildi) | 02-11, 02-12 |
| IEEE-8021AX | IEEE 802.1AX (Link Aggregation ve LACP; eskiden 802.3ad) | 02-13 |
| IEEE-8021AB | IEEE 802.1AB (LLDP) | 02-14 |
| IEEE-8021X | IEEE 802.1X (port tabanlı erişim kontrolü) | 14-06 |
| IEEE-8022 | IEEE 802.2 (LLC) | 02-01 |
| IEEE-80211 | IEEE 802.11 ve ilgili değişiklikleri (n, ac, ax) | 01-08, 02-15 |
| TIA-568 | ANSI/TIA-568 serisi (yapısal kablolama, T568A/B; güncel sürüm kontrol edilecek) | 01-06 |
| ISO-7498 | ISO/IEC 7498-1:1994 = ITU-T X.200 (OSI temel başvuru modeli) | 00-09 |
| ISO-8327 | ISO 8327 / ITU-T X.225 (OSI oturum protokolü) | 05-01 |
| ISO-8823 | ISO 8823 / ITU-T X.226 (OSI sunum protokolü) | 06-01 |
| ITU-ASN1 | ITU-T X.680 (ASN.1), X.690 (BER/DER), X.509 (sertifikalar) | 06-01, 06-03, 06-05 |
| ISO-10589 | ISO/IEC 10589 (IS-IS) | 03-13 |
| STD-IEC80000 | IEC 80000-13 (bilgi bilimi ve teknolojisinde büyüklükler ve birimler; ikili önekler kibi, mebi, gibi) | 00-02 |

### 4.5 Kayıtlar ve referans verileri (planlandı)

| Kimlik | Kaynak | Kullanım |
|---|---|---|
| IANA-PORTS | IANA Service Name and Transport Protocol Port Number Registry | Port numaraları |
| IANA-PROTO | IANA Protocol Numbers | IPv4 Protocol / IPv6 Next Header değerleri |
| IANA-SPECIAL | IANA IPv4 ve IPv6 Special-Purpose Address Registry | Özel amaçlı adres blokları |
| IEEE-RA | IEEE Registration Authority (OUI ve EtherType kayıtları) | 02-02, 02-03 |
| UNICODE | The Unicode Standard (unicode.org) | 06-02 |

### 4.6 Ders kitapları (ek okuma)

| Kimlik | Kitap | En uygun olduğu yer |
|---|---|---|
| TXT-PETZOLD | Charles Petzold, *Code: The Hidden Language of Computer Hardware and Software*, 2. baskı, Microsoft Press | 00-01 – 00-05 |
| TXT-HARRIS | David M. Harris ve Sarah L. Harris, *Digital Design and Computer Architecture*, Morgan Kaufmann | 00-03 – 00-07 [DERİN] |
| TXT-KUROSE | James F. Kurose ve Keith W. Ross, *Computer Networking: A Top-Down Approach*, 8. baskı, Pearson | Tüm katmanlar |
| TXT-TANENBAUM | Andrew S. Tanenbaum, Nick Feamster ve David J. Wetherall, *Computer Networks*, 6. baskı, Pearson | L1–L2 ve genel |
| TXT-STEVENS | Kevin R. Fall ve W. Richard Stevens, *TCP/IP Illustrated, Volume 1: The Protocols*, 2. baskı, Addison-Wesley | 03-*, 04-*, 07-* |
| TXT-SPURGEON | Charles E. Spurgeon ve Joann Zimmerman, *Ethernet: The Definitive Guide*, 2. baskı, O'Reilly | 01-06, 01-09, 02-03 |
| TXT-PERLMAN | Radia Perlman, *Interconnections*, 2. baskı, Addison-Wesley | 02-11, 03-13 [DERİN] |
| TXT-ODOM | Wendell Odom ve diğerleri, *CCNA 200-301 Official Cert Guide*, Cilt 1 ve 2, 2. baskı, Cisco Press (v1.1 için). v2.0 için yeni baskı çıkarsa güncellenecek | CCNA hazırlığı |

### 4.7 Eğitim kaynakları ve araç belgeleri (planlandı)

| Kimlik | Kaynak | Kullanım |
|---|---|---|
| EDU-JITL | Jeremy's IT Lab, ücretsiz CCNA kursu | Yalnızca çapraz kontrol (Düzey 6) |
| TOOL-WIRESHARK | Wireshark User's Guide ve örnek yakalamalar. https://www.wireshark.org/docs/ | H02, H07–H12 |
| TOOL-ANSIBLE | Ansible belgeleri (cisco.ios koleksiyonu dahil). https://docs.ansible.com | 15-05, H18 |
| TOOL-LINUX | iproute2 ve Linux man sayfaları (`ip`, `ss`, `ip netns`). https://man7.org/linux/man-pages/ | H01, H07, H16 |
| TOOL-OPENSSL | OpenSSL belgeleri (`s_client`) | H09 |
| TOOL-OPENSSH | OpenSSH belgeleri (ssh, scp, sftp) | H13 |

### 4.8 Temel makaleler ve öğrenme bilimi

| Kimlik | Kaynak | Kullanım |
|---|---|---|
| PAPER-SHANNON | C. E. Shannon, "A Mathematical Theory of Communication", *Bell System Technical Journal*, 27 (1948) | 00-01: bit, bilgi ve entropi |
| LRN-ROEDIGER | H. L. Roediger ve J. D. Karpicke, "Test-Enhanced Learning", *Psychological Science*, 17(3), 2006 | 12-01: geri çağırma pratiği |
| LRN-CEPEDA | N. J. Cepeda ve diğerleri, "Distributed Practice in Verbal Recall Tasks", *Psychological Bulletin*, 132(3), 2006 | 12-01: aralıklı çalışma |
| LRN-DUNLOSKY | J. Dunlosky ve diğerleri, "Improving Students' Learning With Effective Learning Techniques", *Psychological Science in the Public Interest*, 14(1), 2013 | 12-01: öğrenme tekniklerinin karşılaştırılması |

### 4.9 P1'in ikinci yarısında kullanılan kaynaklar (00-05 – 00-09, FND soruları; erişim: 2026-11-20)

Bu bölümdeki kimlikler ilk kez burada tanımlandı ya da daha önce "planlandı" durumundaydı ve bu oturumda okundu. "Okundu (arama özeti)", kaynağın yalnızca arama sonucundaki ilgili bölümünün okunduğunu gösterir.

| Kimlik | Kaynak | Düzey | Durum | Kullanım |
|---|---|---|---|---|
| CISCO-V11 | (Bölüm 4.1) | 1 | Okundu (arama özeti, yeniden) | 00-08: v1.1 1.1.a–h alt maddeleri |
| CISCO-NETACAD | Cisco Networking Academy CCNA materyali (Tartu Üniversitesi aynası, modül 6.3.1.3) ve NSRC atölye notları (çapraz kontrol) | 1 | Okundu (arama özeti) | 00-05: router bellek türleri (RAM, ROM, NVRAM, flash) |
| CISCO-PCM | Cisco, *Waveform Coding Techniques* (belge 8123). https://www.cisco.com/c/en/us/support/docs/voice/h323/8123-waveform-coding.html | 1 | Okundu (arama özeti) | 00-06: örnekleme öncesi süzme, PCM, 64 kbps |
| CISCO-VOIP-BW | Cisco, *Voice Over IP – Per Call Bandwidth Consumption* (belge 7934). https://www.cisco.com/c/en/us/support/docs/voice/voice-quality/7934-bwidth-consume.html | 1 | Okundu (arama özeti) | 00-06: G.711, 20 ms, 50 pps, Ethernet üzerinde 87,2 kbps; 40 bayt IP/UDP/RTP ve 18 bayt Ethernet başlığı varsayımı |
| CISCO-IFCOUNT | Cisco belgeleri ve Cisco Community: `show interfaces` sayaçları (ör. *Troubleshoot Ignored Errors*, belge 18003; Cisco çalışanlarının overrun açıklaması) | 1 / 6 | Okundu (arama özeti) | 00-07: overrun, ignored, no buffer |
| STD-TI-LOGIC | Texas Instruments, *Logic Guide* (SDYU001, 2017). https://www.ti.com/lit/sdyu001 | 4 | Okundu (arama özeti) | 00-05: 5 V TTL ve 3,3 V LVTTL seviyeleri (VIH 2,0; VIL 0,8; VOH 2,4; VOL 0,4 V) |
| STD-JEDEC-DDR4 | JEDEC JESD79-4, DDR4 SDRAM | 2 | Açık (birincil metin ücretli; okunmadı) | 00-05: 64 ms yenileme penceresi. Değer SEC-DRAM ile çapraz kontrol edildi |
| SEC-DRAM | *HiRA: Hidden Row Activation for Reducing Refresh Latency of Off-the-Shelf DRAM Chips* (arXiv:2209.10198); arXiv:2303.07445; Maine Üniversitesi ECE 571 ders notları | 5–6 | Okundu (arama özeti) | 00-05: DDR4 tREFW = 64 ms, tREFI = 7,8 µs; yüksek sıcaklıkta daha sık yenileme |
| PAPER-COHEN | D. Cohen, "On Holy Wars and a Plea for Peace", IEN 137, 1 Nisan 1980. https://www.ietf.org/rfc/ien/ien137.txt | 3 | Okundu (arama özeti) | 00-06: big-endian ve little-endian terimlerinin kökeni |
| RFC 791 | (Bölüm 4.3) RFC 791, Ek B: *Data Transmission Order* | 3 | Okundu (arama özeti) | 00-06: oktetlerin iletim sırası; 00-09: "internet datagram" terimi |
| ITU-G711 | ITU-T G.711, *Pulse code modulation (PCM) of voice frequencies*. https://www.itu.int/rec/T-REC-G.711 | 2 | Okundu (arama özeti; Blue Book alıntısı) | 00-06: 8.000 örnek/s, örnek başına 8 bit |
| STD-PNG | W3C, *Portable Network Graphics (PNG) Specification* (3. baskı), §5.2 PNG signature. https://www.w3.org/TR/png/ | 2 | Okundu (arama özeti) | 00-06: PNG imzası 137 80 78 71 13 10 26 10 |
| LNX-NAPI | Linux kernel documentation, *NAPI*. https://docs.kernel.org/networking/napi.html | 4 | Okundu (arama özeti) | 00-07: kesme + yoklama, bütçe, kesme maskeleme, cihazdaki IRQ birleştirme |
| TOOL-WINNET | Microsoft, NetAdapter PowerShell modülü belgeleri (`Get-NetAdapter`, `Get-NetAdapterStatistics`, `Get-NetAdapterAdvancedProperty`). https://learn.microsoft.com/powershell/module/netadapter/ | 4 | Planlandı (komut adları bilinen davranışa göre; H01'de doğrulanacak) | 00-07: Windows'ta NIC istatistikleri ve sürücü ayarları |
| RFC 1122 | (Bölüm 4.3) §1.1.3 *Internet Protocol Suite*, §1.3.1 *Organization* | 3 | Okundu | 00-09: dört katman; ICMP'nin IP ile ilişkisi; "strict layering is an imperfect model" |
| RFC 3439 | (Bölüm 4.3) §3 *Layering Considered Harmful* | 3 | Okundu (arama özeti: içindekiler ve bölüm girişi) | 00-09: katmanlamanın sakıncaları |
| ITU-X200 | ITU-T X.200 (07/1994), *OSI Basic Reference Model: The basic model*; ISO/IEC 7498-1:1994 ile aynı metin. https://www.itu.int/rec/T-REC-X.200-199407-I | 2 | Okundu (kayıt sayfası; metin ücretsiz, bu oturumda açılmadı) | 00-09: OSI modelinin geçerli metni ve tarihi; önceki sürüm X.200 (11/88) |


## References added for Physical Layer lessons

| ID | Source | Used in |
|---|---|---|
| CISCO-CCNA-EXAM-TOPICS-V11 | [Cisco 200-301 CCNA v1.1 Exam Topics](https://learningnetwork.cisco.com/s/ccna-exam-topics) | 01-06: objective 1.3 (single-mode fiber, multimode fiber, copper; Ethernet shared media and point-to-point connections) |
| CISCO-POE-INDUSTRIAL | [Cisco — PoE for Industrial Automation](https://www.cisco.com/c/en/us/products/collateral/networking/industrial-switches/poe-ind-data-control-single-cable-so.html) | 01-06: 802.3af/at/bt PSE and PD power levels |
| CISCO-POE-IOSXE | [Cisco IOS XE PoE Configuration Guide](https://www.cisco.com/c/en/us/td/docs/switches/lan/c9000/infra/poe/poe-configuration-guide/g-poe/c-poe.html) | 01-06: PoE classification and power capabilities |
| ANSI-TIA-568-E-REFERENCE | [ANSI/TIA-568-E cabling reference table](https://imlive.s3.amazonaws.com/Federal%20Government/ID62048956821926688123123361973875756393/Attachment%201i%20TIA-568%20Telecomm%20Cabling%20Standard.pdf) | 01-06: balanced twisted-pair application distances and categories |

| CISCO-GIG-SFP-DATA-SHEET | [Cisco — Gigabit Ethernet SFP Transceiver Data Sheet](https://www.cisco.com/c/en/us/products/collateral/interfaces-modules/gigabit-ethernet-gbic-sfp-modules/datasheet-c78-366584.html) | 01-07: example 1000BASE-SX and 1000BASE-LX/LH wavelengths, fiber types, and transceiver reach |
| CISCO-CPWE-FIBER-GUIDE | [Cisco — Physical Infrastructure Design Guide (Fiber Optics)](https://www.cisco.com/c/en/us/td/docs/solutions/Verticals/CPwE/5-1/Phy_Arch/CPwE-Physical-Infrastructure_Feb2023.pdf) | 01-07: core size, SMF/MMF overview, OM/OS fiber categories |

| CISCO-WIRELESS-RF-GUIDE | [Cisco Wireless RF Reference Guide](https://www.cisco.com/c/en/us/td/docs/wireless/controller/9800/technical-reference/wireless-rf-reference-guide.html) | 01-08: frequency bands, channel overlap, RSSI/dBm, attenuation, multipath, MIMO |
| CISCO-WIRELESS-DESIGN-LARGE | [Cisco Design Guide — Wireless for Large Public Networks](https://www.cisco.com/c/en/us/support/docs/wireless/catalyst-9800-series-wireless-controllers/222000-design-guide-cx-wireless-for-large-pub.html) | 01-08: channel width, 2.4/5/6 GHz planning, regional channel considerations |
| CISCO-ETHERNET-AUTONEG | [Cisco Configure and Verify Ethernet Auto-Negotiation](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/10561-3.html) | 01-09: auto-negotiation, speed/duplex, duplex mismatch |
| CISCO-LAN-TROUBLESHOOT | [Cisco Troubleshoot LAN Switching Environments](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/12006-chapter22.html) | 01-10: collisions, late collisions, errors and Ethernet troubleshooting |

| IEEE-802-LLC-REFERENCE | [IEEE 802 overview and standards references](https://www.ieee802.org/) | 02-01: LLC/MAC sublayer context and IEEE 802 architecture |

| RFC-9724-MAC-RANDOMIZATION | [RFC 9724 — State of Affairs for Randomized and Changing MAC Addresses](https://www.rfc-editor.org/rfc/rfc9724.html) | 02-02: 48-bit MAC address format, OUI, I/G and U/L bits, local/randomized addresses |
| IEEE-EUI-OUI-GUIDELINES | [IEEE — Guidelines for EUI, OUI, and CID](https://standards-support.ieee.org/hc/en-us/articles/4888705676564-Guidelines-for-Use-of-Extended-Unique-Identifier-EUI-Organizationally-Unique-Identifier-OUI-and-Company-ID-CID) | 02-02: OUI and special MAC address bits |
| RFC-7042-IEEE-802-IDENTIFIERS | [RFC 7042 — IANA Considerations and IEEE 802 Parameters](https://www.rfc-editor.org/rfc/rfc7042.html) | 02-02: EUI-48 address structure, group and local bits |

| CISCO-ETHERNET-FRAME-TR | [Cisco — Ethernet and IEEE 802.3 Frame Formats](https://www.cisco.com/en/US/docs/internetworking/troubleshooting/guide/tr1904.pdf) | 02-03: frame fields, preamble, SFD, Type/Length, FCS, minimum frame size and padding |
| CISCO-NETFLOW-L2-FRAME | [Cisco — NetFlow Layer 2 and Ethernet Frame Formats](https://www.cisco.com/c/en/us/td/docs/ios-xml/ios/iproute_pi/configuration/15-s/nf-15-s-book.pdf) | 02-03: Ethernet II and IEEE 802.3 frame fields |
| CISCO-PRESS-ETHERNET-FRAME | [Cisco Press — Ethernet Frames](https://www.ciscopress.com/articles/article.asp?p=3089352&seqNum=4) | 02-03: standard frame size and VLAN-tagged Ethernet |

| CISCO-ETHERNET-ERROR-DETECTION | [Cisco — Ethernet and IEEE 802.3 Frame Formats](https://www.cisco.com/en/US/docs/internetworking/troubleshooting/guide/tr1904.pdf) | 02-04: Ethernet FCS and frame integrity checks |
| CISCO-LAN-TROUBLESHOOT-ERRORS | [Cisco — Troubleshoot LAN Switching Environments](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/12006-chapter22.html) | 02-04: CRC/FCS errors and interface troubleshooting |

| CISCO-ETHERNET-CSMA-CD | [Cisco Press — Ethernet Frames and Shared Ethernet](https://www.ciscopress.com/articles/article.asp?p=3089352&seqNum=4) | 02-05: half-duplex shared Ethernet and CSMA/CD |
| CISCO-LAN-TROUBLESHOOT-CSMA | [Cisco — Troubleshoot LAN Switching Environments](https://www.cisco.com/c/en/us/support/docs/lan-switching/ethernet/12006-chapter22.html) | 02-05: collisions, late collisions, duplex mismatch and troubleshooting |

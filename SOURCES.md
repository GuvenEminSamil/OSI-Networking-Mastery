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
| IPv4 | 791 (IPv4), 792 (ICMP), 1191 (PMTUD), 1812 (IPv4 router gereksinimleri), 1918 (özel adresler), 3021 (/31), 3927 (IPv4 link-local), 4632 (CIDR), 5737 (dokümantasyon adresleri), 6598 (paylaşılan adres alanı), 6890 (özel amaçlı adres kayıtları) | 03-02 – 03-12 |
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

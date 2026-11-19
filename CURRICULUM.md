# Müfredat (Curriculum)

> Bu dosya projedeki **tüm planlanan dosyaların tek doğruluk kaynağıdır.** STUDY-ROADMAP.md bu dosyalara kimlikleriyle (`MM-NN`, `LAB-NNN`, `Hnn`, `Knn`) atıf yapar. Dosya adı değişirse önce burası güncellenir.
>
> Durum: v0.2, onaylandı ve CCNA v1.1 hedefine göre güncellendi (2026-11-19).

## 1. Tasarım kararları

1. **Aşağıdan yukarıya, spiral tekrarlarla.** İstediğin gibi bitten uygulamaya ilerliyoruz. Kapsamlı senaryolar (08-*) ise ilgili katmanlar öğrenildiği anda devreye giriyor. Böylece katmanlar birbirinden kopuk konular olarak kalmıyor.
2. **Birincil sınav hedefi CCNA 200-301 v1.1.** v1.1'in son sınav günü 2 Şubat 2027 (bkz. SOURCES.md: CISCO-V11). Konu listesi Cisco'nun resmi v1.1 PDF'iyle doğrulandı; müfredat 53 konunun tamamını kapsıyor (Bölüm 9.1). v2.0'a özgü konular `[v2.0-FARK]` ile işaretlendi ve sınav sonrasına, Faz 14'e ertelendi. Sınav 2 Şubat'tan önce yapılamazsa aynı müfredat Faz 14'teki v2.0 farklarıyla v2.0'a geçirilir (Bölüm 9.2).
3. **Her bilgi tek yerde.** Kavram bir kez, en uygun dosyada açıklanır. Diğer dosyalar kimlikle bağlantı verir.
4. **Bağımlılığa göre yerleşim.** Bazı konular, dayandıkları konular öğrenilene kadar ertelendi. ARP, IPv4 adreslemeden sonra gelir. NAT, portlardan sonra gelir. DHCP snooping ve DAI ise DHCP, ARP ve NDP'den sonra gelir.
5. **Packet Tracer'ın sınırları açıkça belirtilir.** PT'de yapılamayan konular için gerçek host labları (`H`) ve kod alıştırmaları (`K`) var.
6. **Mevcut OSI notların başlangıç düzeyi kabul edilir.** "OSI Modeli — Kapsamlı Çalışma Notları" (SOURCES.md: USR-OSI-NOTES) genel bakış düzeyindedir. Müfredat bu notları yeniden yazmaz, altlarındaki mekanizmaları açar. Notlardaki düzeltilmesi gereken noktalar ilgili dosyalarda ele alınır (bkz. Bölüm 11).
7. **İki tür pratik: yönerge ve tam lab.** Senin isteğinle labların çoğu kısa yönergeye dönüştürüldü: topolojiyi ve yapılandırmayı sen tasarlarsın. Tam lab (adresleme tablosu, hatalı yapılandırmalar, ayrıntılı çözüm) yalnızca arıza avı, entegrasyon ve sınav tarzı görevlerde kullanılır (Bölüm 4.4).
8. **Sınav öncesi çekirdek, sınav sonrası derinleşme.** `[DERİN]` bölümler, "Kodla-Anla" alıştırmaları (K01–K08), sınavla doğrudan ilgisi olmayan host labları ve v2.0 farkları Faz 14'e bırakıldı. Teori dosyalarının tamamı çekirdektir.

## 2. Modül düzeyinde önkoşullar

| Modül | Önkoşul | Neden |
|---|---|---|
| 00 Temeller | — | Başlangıç noktası |
| 01 Fiziksel | 00 | Elektrik, transistör ve ikili temsil olmadan sinyal anlaşılmaz |
| 02 Veri Bağlantı | 01, 00-03 | Çerçeve bitlerin üzerine kurulur; CRC, XOR'a dayanır |
| 03 Ağ | 02, 00-03 | Maske işlemleri AND'e, iletim ARP ve switch'e dayanır |
| 04 Taşıma | 03, 00-07 | Portlar süreçleri adresler; soket, işletim sistemi kavramıdır |
| 05 Oturum | 04 | Oturum işlevleri bugün TCP ve TLS içinde yaşar |
| 06 Sunum | 00-06, 04, 05 | Kodlama veri temsiline, TLS ise TCP'ye dayanır |
| 07 Uygulama | 04, 06 | Protokoller TCP/UDP üzerinde çalışır; HTTPS, TLS'e dayanır |
| 08 Katmanlar Arası | ilgili katmanlar | Her senaryonun önkoşulu kendi satırında |
| 14 Güvenlik | 02, 03, 04, 07 | ACL portlara; L2 savunmaları DHCP, ARP ve NDP'ye dayanır |
| 15 Operasyon/Otomasyon/AI | 03, 07 | Kontrol ve veri düzlemi, REST, SNMP ve syslog bilgisi gerekir |
| 11 Arıza Giderme | parça parça | Metodoloji Faz 2'de, katalog ve vakalar sonda |

## 3. Teori modülleri

Sütunlar: **ID**, **Dosya**, **Kapsam**, **Önkoşul** (dosya kimliği), **CCNA** (`v2` = v2.0, `v1.1` = v1.1 konu kodu).

### 3.1 `00-FOUNDATIONS/`

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 00-01 | `01-Information-and-Data.md` | Bilgi ve veri ayrımı; analog ve dijital bilgi; neden ikili: gürültü payı (noise margin) ve güvenilir ayırt etme; bitin bir "karar" olması | — | — |
| 00-02 | `02-Number-Systems-and-Units.md` | Onluk, ikili ve onaltılık sistemler; elle ve hızlı dönüşüm; 2'nin kuvvetleri; bit, nibble, bayt, oktet; SI ve IEC önekleri (kB/KiB); Mbps ile MB/s farkı | 00-01 | v2 1.3, 1.4 (altyapı) |
| 00-03 | `03-Binary-Arithmetic-and-Boolean-Logic.md` | İkili toplama, taşma, ikiye tümleyen; AND, OR, NOT, XOR; bit düzeyi işlemler ve maskeleme; mantık kapıları. Köprüler: AND → alt ağ maskesi, XOR → parite ve CRC | 00-02 | v2 1.3 (altyapı) |
| 00-04 | `04-Electricity-Fundamentals.md` | Gerilim (Voltage), akım (Current), direnç (Resistance), Ohm yasası, güç, devre, toprak ve referans; DC ve AC. [DERİN] empedans ve kapasitans sezgisi | — | — |
| 00-05 | `05-Transistors-and-Digital-Logic.md` | Yarı iletken ve anahtar olarak MOSFET; CMOS kapılar; mantık seviyeleri ve eşikler; bitin bellekte saklanması (flip-flop, DRAM sezgisi); saat sinyali (clock) | 00-03, 00-04 | — |
| 00-06 | `06-Data-Representation.md` | Tamsayılar; endianness ve ağ bayt sırası (network byte order); metne giriş (ayrıntısı 06-02'de); görüntü (piksel, RGB), ses (örnekleme, Nyquist, PCM), video (kare, codec); her dosyanın bir bayt dizisi olması | 00-02 | — |
| 00-07 | `07-Computer-Architecture-for-Networking.md` | CPU, RAM, veri yolu; NIC, DMA, kesmeler (interrupt), halka tamponlar; sürücü; işletim sistemi ağ yığını; soket kavramına ilk bakış | 00-05, 00-06 | — |
| 00-08 | `08-Networking-Fundamentals.md` | Ağ nedir; LAN, WAN, WLAN; cihazların rolleri (host, NIC, hub, switch, router, AP, WLC, firewall/IPS, sunucu, PoE); istemci-sunucu ve P2P; protokol ve standart; IEEE, IETF, ISO, ITU; bant genişliği, gecikme, verim; MAC ve IP adresine ilk bakış | 00-07 | v1.1 1.1 |
| 00-09 | `09-Layered-Models-OSI-and-TCPIP.md` | Katmanlı mimarinin nedeni; OSI'nin tarihi (ISO/IEC 7498-1); TCP/IP modeli (RFC 1122); PDU adları; kapsüllemeye genel bakış; protokollerin katmanlara neden tam oturmadığı; model ile uygulama farkı | 00-08 | — |

### 3.2 `01-PHYSICAL-LAYER/`

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 01-01 | `01-Physical-Layer-Purpose.md` | Sorumluluklar ve sınırlar (bu katmanda çerçeve kavramı yoktur); bitten sinyale hattın genel görünümü; PHY ile MAC arayüzü | 00-09 | — |
| 01-02 | `02-Signals-and-Bandwidth.md` | Sinyal; frekans, genlik, faz, periyot; analog ve dijital sinyal; Fourier sezgisi; bant genişliği (Hz) ile veri hızı (bps) farkı; Nyquist ve Shannon ([TEMEL] özet, [DERİN] türetme) | 00-04, 01-01 | — |
| 01-03 | `03-Line-Coding-and-Modulation.md` | Hat kodlaması (line coding): NRZ, Manchester (10BASE-T), 4B/5B + MLT-3 (100BASE-TX), PAM-5 (1000BASE-T), PAM-16 (10GBASE-T), PAM4; 8b/10b ve 64b/66b blok kodlama; bit hızı ile sembol hızı (baud) farkı; ASK, FSK, PSK, QAM; OFDM | 01-02, 00-05 | — |
| 01-04 | `04-Bit-Synchronization-and-Reception.md` | **Alıcı bitleri nasıl yeniden kurar:** örnekleme, karar eşiği, saat kurtarma (PLL), preamble ve SFD ile hizalanma, eşitleme (equalization), kod çözme; bit hata oranı (BER) | 01-03 | — |
| 01-05 | `05-Signal-Impairments.md` | Zayıflama (attenuation); desibel ve dBm; gürültü ve SNR; EMI ve RFI; karışma (crosstalk: NEXT/FEXT); yansıma ve empedans uyumsuzluğu; dispersiyon; jitter | 01-02 | v2 1.1 |
| 01-06 | `06-Copper-Cabling.md` | Bükümlü çiftin fiziği ve diferansiyel sinyal; UTP, STP, F/UTP; Cat5e–Cat8; koaksiyel; RJ-45 (8P8C); T568A/B pin dizilimleri; düz, çapraz ve rollover kablo; Auto-MDIX; 100 m sınırının nedeni; PoE (802.3af/at/bt) | 01-05, 00-04 | v2 1.1, 2.2 · v1.1 1.3 |
| 01-07 | `07-Fiber-Optics.md` | Işığın kırılması ve tam iç yansıma; çekirdek ve kaplama; SMF ve MMF; 850/1310/1550 nm; modal ve kromatik dispersiyon; LC ve SC; SFP, SFP+, QSFP; verici (lazer, VCSEL) ve alıcı (fotodiyot) | 01-05 | v2 1.1 · v1.1 1.3 |
| 01-08 | `08-Wireless-RF-Fundamentals.md` | Elektromanyetik dalga; 2.4/5/6 GHz bantları; kanallar, kanal genişliği, örtüşmeyen kanallar; RSSI, dBm, SNR; girişim nedenleri; çok yolluluk (multipath); MIMO | 01-02, 01-05 | v2 1.5 · v1.1 1.11 |
| 01-09 | `09-Ethernet-Physical-Standards.md` | IEEE 802.3 adlandırması (10BASE-T … 100GBASE); otomatik anlaşma (autonegotiation); hız ve duplex; half ve full duplex | 01-03, 01-06, 01-07 | v2 1.1 |
| 01-10 | `10-Topologies-Devices-and-Interface-Issues.md` | Fiziksel ve mantıksal topoloji; repeater, hub, medya dönüştürücü, transceiver; arayüz hataları (CRC, runt, giant, collisions, late collisions, input errors) ve teşhis yaklaşımı | 01-09 | v2 1.1 · v1.1 1.4 |

### 3.3 `02-DATA-LINK-LAYER/`

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 02-01 | `01-Data-Link-Layer-Purpose.md` | Sorumluluklar; LLC (802.2) ve MAC alt katmanları; çerçeveleme (framing); ortam erişimi; LAN ve WAN veri bağlantısı (HDLC ve PPP'ye kısa bakış) | 00-09, 01-01 | — |
| 02-02 | `02-MAC-Addresses-and-NICs.md` | 48 bitlik yapı, OUI, I/G ve U/L bitleri; unicast, multicast, broadcast; MAC rastgeleleştirme; NIC'in çerçeve filtrelemesi, promiscuous mod, donanım offload'ları | 00-02, 02-01 | v1.1 1.13 |
| 02-03 | `03-Ethernet-Frame-Structure.md` | Preamble ve SFD; çerçeve alanları; EtherType ile Length ayrımı; minimum 64 bayt kuralının nedeni; MTU ve jumbo çerçeve; çerçeveler arası boşluk (IFG) | 02-02 | v1.1 1.13 |
| 02-04 | `04-Error-Detection-FCS-and-CRC.md` | Parite ve checksum; CRC matematiği (polinom bölmesi ve XOR); FCS; hata tespiti ile hata düzeltme farkı; hatalı çerçeveye ne olduğu | 00-03, 02-03 | v2 1.1 |
| 02-05 | `05-Media-Access-CSMA-CD-and-Duplex.md` | Paylaşımlı ortam ve çarpışma; CSMA/CD; üstel geri çekilme; slot time; full duplex'in CSMA/CD'yi neden gereksiz kıldığı | 01-09, 02-03 | v2 1.1 · v1.1 1.4 |
| 02-06 | `06-Switch-Operation.md` | **Çerçeve switch'e girdiğinde tam olarak ne olur:** FCS kontrolü, kaynak MAC'i öğrenme, hedefi arama, forward/filter/flood kararı; aging; CAM ve TCAM; ASIC; store-and-forward, cut-through, fragment-free; tamponlar | 02-03, 02-04, 02-05 | v1.1 1.13 |
| 02-07 | `07-Collision-and-Broadcast-Domains.md` | Çarpışma ve yayın alanları; hub, switch ve router'ın bu alanlara etkisi | 02-06 | v1.1 1.13 |
| 02-08 | `08-VLANs.md` | VLAN'ın nedeni; VLAN ID aralıkları; access port; default VLAN; data ve voice VLAN; VLAN veritabanı | 02-07 | v2 2.2 · v1.1 2.1 |
| 02-09 | `09-Trunking-8021Q-and-DTP.md` | 802.1Q etiketi (TPID, PCP, DEI, VID); native VLAN; izinli VLAN listesi; DTP modları ve güvenlik riski; [DERİN] VTP | 02-08 | v2 2.1 · v1.1 2.2 |
| 02-10 | `10-ARP.md` | ARP paket formatı; istek (broadcast) ve yanıt (unicast); önbellek; gratuitous ARP; proxy ARP; ARP'nin hangi katmana ait olduğu tartışması | 02-03, 03-03 | v2 2.4 |
| 02-11 | `11-Spanning-Tree-STP.md` | Döngüler, yayın fırtınası, MAC flapping; bridge ID ve root seçimi; yol maliyeti; port rolleri ve durumları; BPDU; zamanlayıcılar | 02-06, 02-09 | v2 2.5 |
| 02-12 | `12-Rapid-PVST-and-STP-Protection.md` | RSTP (802.1w) farkları ve proposal/agreement; Rapid PVST+; root primary/secondary; PortFast; BPDU guard ve BPDU filter; root guard; loop guard | 02-11 | v2 2.5 · v1.1 2.5 |
| 02-13 | `13-EtherChannel-LACP.md` | Bağlantı birleştirmenin nedeni; LACP, PAgP ve statik mod; uyumluluk koşulları; yük dağıtım hash'i; L2 ve L3 port-channel | 02-11 | v2 2.1, 2.2 · v1.1 2.4 |
| 02-14 | `14-CDP-and-LLDP.md` | Keşif protokolleri; TLV yapısı; ağ dokümantasyonunu doğrulama | 02-03 | v2 2.3 · v1.1 2.3 |
| 02-15 | `15-Wireless-LAN-MAC-802-11.md` | 802.11 çerçeve türleri (yönetim, kontrol, veri); CSMA/CA, RTS/CTS; SSID ve BSSID; BSS ve ESS; ilişkilendirme (association); dolaşım (roaming); 3 ve 4 adres alanları | 01-08, 02-05 | v2 1.5 · v1.1 1.11 |
| 02-16 | `16-Wireless-Architectures-and-WLC.md` | Otonom, kontrolcü tabanlı ve bulut yönetimli mimariler; CAPWAP; AP modları; AP ve WLC'nin switch'e bağlanması (access, trunk, LAG) | 02-15, 02-09, 03-03 | v2 2.2 · v1.1 2.6, 2.7, 2.9 |

### 3.4 `03-NETWORK-LAYER/`

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 03-01 | `01-Network-Layer-Purpose.md` | MAC adresi varken mantıksal adresin neden gerektiği (hiyerarşi, ölçeklenebilirlik); bağlantısız, en iyi çaba (best-effort) teslimat; kontrol, veri ve yönetim düzlemleri | 00-09, 02-01 | v1.1 6.2 |
| 03-02 | `02-IPv4-Header.md` | Tüm alanlar ve her birinin varlık nedeni; DSCP/ECN; TTL; protokol numarası; bayraklar ve fragment offset; başlık checksum'ı | 03-01, 00-02 | — |
| 03-03 | `03-IPv4-Addressing.md` | Noktalı ondalık gösterim; ağ ve host kısmı; maske; sınıflı adreslemenin tarihi ve CIDR; özel adresler (RFC 1918); özel amaçlı adresler (loopback, APIPA, multicast, 100.64/10) | 03-02, 00-03 | v2 1.3 · v1.1 1.6, 1.7 |
| 03-04 | `04-Subnetting-Binary-Method.md` | Önce ikili yöntem, sonra hızlı yöntem (magic number); ağ adresi, yayın adresi ve host aralığı; FLSM | 03-03 | v2 1.3 · v1.1 1.6 |
| 03-05 | `05-VLSM-and-Summarization.md` | VLSM tasarımı; /31 (RFC 3021) ve /32; rota özetleme (summarization) | 03-04 | v2 1.3 |
| 03-06 | `06-Host-Forwarding-and-Default-Gateway.md` | Host'un yerel/uzak kararı (AND işlemi); varsayılan ağ geçidi için ARP; host yönlendirme tablosu; Windows, macOS ve Linux'ta doğrulama | 03-04, 02-10 | v2 1.3, 1.6 · v1.1 1.10 |
| 03-07 | `07-Router-Packet-Forwarding.md` | **Router bir IP paketi aldığında tam olarak ne olur:** hedef MAC ve FCS kontrolü, decapsulation, başlık denetimi, TTL azaltma, checksum'ın yeniden hesaplanması, tablo araması, ARP/adjacency, yeni çerçeve; process switching, fast switching ve CEF (FIB + adjacency tablosu) | 03-06, 02-06 | v2 3.1 |
| 03-08 | `08-Routing-Table-LPM-AD-Metric.md` | Rota kaynakları ve kodları; connected ve local rotalar; en uzun önek eşleşmesi (LPM); yönetimsel uzaklık (AD); metrik; varsayılan rota; `show ip route` çıktısını okuma | 03-07 | v2 3.1 · v1.1 3.1, 3.2 |
| 03-09 | `09-Static-Routing.md` | Ağ, host, varsayılan ve floating rotalar; next-hop ve çıkış arayüzü; özyinelemeli arama (recursive lookup); IPv4 sözdizimi (IPv6 sözdizimi 03-18'de) | 03-08 | v2 3.2 · v1.1 3.3 |
| 03-10 | `10-Inter-VLAN-Routing.md` | Router-on-a-stick; SVI; routed port; `ip routing` | 03-09, 02-09 | v2 2.1 · v1.1 2.1 |
| 03-11 | `11-ICMP-Ping-and-Traceroute.md` | ICMP mesaj türleri; ping mekaniği; extended ping; traceroute (TTL ile; Windows'ta ICMP, Unix ve Cisco'da UDP); ICMPv6 farkları | 03-02, 03-07 | v2 2.4 |
| 03-12 | `12-MTU-and-Fragmentation.md` | MTU; IPv4 parçalanma alanları ve birleştirme; DF biti; Path MTU Discovery ve "kara delik" sorunları; IPv6'da router'ların parçalama yapmaması; TCP MSS ile ilişkisi | 03-02, 02-03 | — |
| 03-13 | `13-Dynamic-Routing-Concepts.md` | Mesafe vektörü (distance vector) ve bağlantı durumu (link state); yakınsama; IGP ve EGP; döngü önleme; AD'nin rolü; yönlendirilen protokol (IP) ile yönlendirme protokolü ayrımı; örnekler: RIP, EIGRP, IS-IS, BGP; yönlendirme protokollerinin neyin üzerinde çalıştığı (OSPF: IP protokol 89, RIP: UDP 520, BGP: TCP 179) | 03-08 | v2 3.1 |
| 03-14 | `14-OSPF-Concepts.md` | Komşuluk durumları; hello ve dead; LSA ve LSDB; SPF (Dijkstra); maliyet; ağ türleri; DR/BDR; router ID | 03-13 | v2 3.3 · v1.1 3.4 |
| 03-15 | `15-OSPFv2-Configuration.md` | Tek alan yapılandırma ve doğrulama; passive-interface; reference bandwidth; default-information originate; tipik komşuluk sorunları | 03-14 | v2 3.3 · v1.1 3.4 |
| 03-16 | `16-IPv6-Fundamentals.md` | IPv6'nın nedeni; başlık; gösterim ve sıkıştırma kuralları (RFC 5952); adres türleri (GUA, ULA, link-local, multicast, anycast, loopback, unspecified); EUI-64; önek boyutlandırma | 03-02, 00-02 | v2 1.4 · v1.1 1.8, 1.9 |
| 03-17 | `17-IPv6-NDP-SLAAC-DHCPv6.md` | NDP (RS, RA, NS, NA, Redirect); DAD; SLAAC; stateless ve stateful DHCPv6; gizlilik adresleri | 03-16, 02-10 | v2 1.4 |
| 03-18 | `18-IPv6-Routing-and-OSPFv3.md` | `ipv6 unicast-routing`; IPv6 statik rotalar (link-local next-hop dahil); `[v2.0-FARK]` tek alan OSPFv3 | 03-17, 03-09, 03-15 | v2 3.2, 3.3 · v1.1 3.3 |
| 03-19 | `19-First-Hop-Redundancy-HSRP-VRRP.md` | Ağ geçidinin neden tek arıza noktası olduğu; sanal IP ve sanal MAC; aktif/standby (HSRP); `[v2.0-FARK]` master/backup (VRRP); öncelik, preempt; durum çıktısını yorumlama | 03-07, 02-10 | v2 3.4 · v1.1 3.5 |
| 03-20 | `20-NAT-and-PAT.md` | Inside/outside ve local/global terimleri; statik NAT, dinamik NAT, PAT; çeviri tablosu; IOS XE'de yapılandırma; NAT'ın uçtan uca ilkeye etkisi | 03-08, 04-01 | v2 4.3 · v1.1 4.1 |
| 03-21 | `21-QoS-Fundamentals.md` | Atlama başına davranış (per-hop behavior); sınıflandırma; işaretleme (DSCP, CoS); kuyruklama; tıkanıklık; policing ve shaping | 03-02, 02-09 | v1.1 4.7 |

### 3.5 `04-TRANSPORT-LAYER/`

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 04-01 | `01-Transport-Layer-Purpose-Ports-Sockets.md` | Host'tan sürece (process) teslimat; portlar ve port aralıkları; soketler ve 5'li (5-tuple); çoklama ve ayrıştırma (multiplexing/demultiplexing); portlara bakan ara cihazlar (L4 firewall, L4 yük dengeleyici) | 00-07, 03-01 | v1.1 1.5 |
| 04-02 | `02-UDP.md` | Başlık; sözde başlıklı (pseudo-header) checksum; "az şey yapmanın" neden bir özellik olduğu; DNS, VoIP, oyun, QUIC | 04-01 | v1.1 1.5 |
| 04-03 | `03-TCP-Header-and-Connection-Lifecycle.md` | Başlık ve bayraklar; üçlü el sıkışma (three-way handshake); ISN'in neden rastgele olduğu; durum makinesi; FIN, RST, TIME-WAIT | 04-01 | v1.1 1.5 |
| 04-04 | `04-TCP-Reliability.md` | Sıra numaraları; kümülatif ACK; RTT ölçümü ve RTO; hızlı yeniden iletim (fast retransmit); SACK; sıralama | 04-03 | v1.1 1.5 |
| 04-05 | `05-TCP-Flow-and-Congestion-Control.md` | Alıcı penceresi, window scaling, kayan pencere; bant genişliği-gecikme çarpımı (BDP); slow start, congestion avoidance, AIMD, fast recovery; ECN; [DERİN] CUBIC ve BBR | 04-04 | — |
| 04-06 | `06-TCP-vs-UDP-and-Modern-Transport.md` | TCP ve UDP karşılaştırması; MSS, segmentasyon ve TSO; QUIC; [DERİN] SCTP (çoklu akış, çoklu bağlantı noktası); oyun, canlı yayın ve dosya indirme örnekleri | 04-02, 04-05, 03-12 | v1.1 1.5 |
| 04-07 | `07-Application-to-Application-Communication.md` | **İki uygulama ağ üzerinden haberleşirken ne olur:** soket API'si (socket, bind, listen, accept, connect, send, recv); çekirdek tamponları; uygulamadan kabloya ve kablodan uygulamaya yolculuk | 04-03, 00-07 | — |

### 3.6 `05-SESSION-LAYER/`

Bu modül bilerek küçük tutuldu. TCP/IP'de ayrı bir oturum katmanı yoktur; bu işlevler başka protokollerin içine dağılmıştır.

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 05-01 | `01-OSI-Session-Layer-Theory.md` | [OSI-TEORİ] ISO 8327 / ITU-T X.225: oturum kurma, sürdürme, sonlandırma; diyalog kontrolü (token); senkronizasyon noktaları ve checkpoint'ler | 00-09 | — |
| 05-02 | `02-Session-Functions-in-Modern-Protocols.md` | [TCP/IP-GERÇEK] Bu işlevlerin bugünkü yerleri: TCP bağlantıları, TLS oturumları ve resumption, HTTP çerezleri ve oturum kimlikleri, devam ettirilebilir indirmeler (HTTP Range), WebSocket, SSH kanalları, RPC ve SMB | 05-01, 04-03 | — |

### 3.7 `06-PRESENTATION-LAYER/`

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 06-01 | `01-Presentation-Layer-Purpose.md` | Soyut sözdizimi ve aktarım sözdizimi (abstract/transfer syntax); ASN.1'e kısa bakış; OSI teorisi ile TCP/IP gerçeği | 00-06, 00-09 | — |
| 06-02 | `02-Character-Encoding-ASCII-Unicode-UTF8.md` | ASCII; kod sayfaları (Windows-1254, ISO-8859-9); Unicode kod noktaları; UTF-8'in bayt düzeyindeki mekanizması; UTF-16; BOM; Türkçe karakterlerle bozuk metin (mojibake) örnekleri; HTTP `charset` | 06-01, 00-06 | — |
| 06-03 | `03-Serialization-and-Data-Formats.md` | JSON, XML, YAML, Protocol Buffers; ASN.1/BER (SNMP); MIME türleri; Base64 | 06-02 | v1.1 6.7 |
| 06-04 | `04-Compression.md` | Kayıpsız (Huffman, LZ77, DEFLATE, gzip, Brotli) ve kayıplı (JPEG, H.264) sıkıştırma; HTTP `Content-Encoding` | 06-01 | — |
| 06-05 | `05-Cryptography-Fundamentals.md` | Gizlilik, bütünlük, kimlik doğrulama; simetrik (AES) ve asimetrik (RSA, ECC) şifreleme; anahtar değişimi (DH, ECDHE); hash (SHA-2) ve HMAC; dijital imza; sertifikalar ve PKI | 00-03 | v2 4.5 · v1.1 5.4 |
| 06-06 | `06-TLS-and-the-OSI-Model.md` | TLS 1.3 el sıkışması; kayıt katmanı (record layer); SNI ve ALPN; TLS'in neden tek bir OSI katmanına oturmadığı | 06-05, 04-03, 05-02 | — |

### 3.8 `07-APPLICATION-LAYER/`

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 07-01 | `01-Application-Layer-Concepts.md` | Uygulama ile uygulama protokolü farkı; istemci-sunucu ve P2P; istek-yanıt; durumlu ve durumsuz protokoller; iyi bilinen portlar; proxy, reverse proxy ve L7 yük dengeleyici | 04-01 | — |
| 07-02 | `02-DNS.md` | Hiyerarşi (kök, TLD, yetkili sunucu); özyinelemeli ve yinelemeli sorgu; kayıt türleri (A, AAAA, CNAME, MX, NS, PTR, SOA, TXT); önbellek ve TTL; UDP/TCP 53; DoT ve DoH; Cisco'da DNS istemci ayarları | 07-01, 04-02 | v2 4.4 · v1.1 4.3 |
| 07-03 | `03-DHCPv4.md` | DORA; neden broadcast kullanıldığı; seçenekler (gateway, DNS); kiralama; relay agent (`ip helper-address`); Cisco DHCP sunucusu ve arayüzde DHCP istemcisi | 07-01, 04-02, 03-06 | v2 1.7 · v1.1 4.3, 4.6 |
| 07-04 | `04-HTTP-and-HTTPS.md` | HTTP/1.1 mesajları; metotlar, durum kodları, başlıklar; kalıcı bağlantılar; HTTP/2 ve HTTP/3; çerezler; HTTPS = HTTP + TLS | 07-01, 04-03, 06-06 | — |
| 07-05 | `05-Email-SMTP-POP3-IMAP.md` | Gönderim ve alım protokolleri; MX kaydıyla teslimat; portlar ve STARTTLS | 07-02, 07-04 | — |
| 07-06 | `06-Remote-Access-Telnet-SSH.md` | Telnet'in neden güvensiz olduğu; SSH mimarisi (taşıma, kimlik doğrulama ve bağlantı katmanları); Cisco'da SSH yapılandırması; konsol ve HTTP/HTTPS ile yönetim erişimi | 04-03, 06-05 | v2 4.1, 4.2 · v1.1 2.8, 4.8 |
| 07-07 | `07-File-Transfer-FTP-TFTP-SCP-SFTP.md` | FTP kontrol ve veri kanalları; aktif ve pasif mod (NAT sorunları); TFTP (UDP 69); `[v2.0-FARK]` SCP ve SFTP (SSH üzerinden); IOS imajı ve yapılandırma dosyası yönetimi | 07-06, 04-02 | v2 4.2 · v1.1 4.9 |
| 07-08 | `08-NTP.md` | Zamanın neden önemli olduğu (loglar, sertifikalar); stratum; NTP istemci ve sunucu modu | 04-02 | v1.1 4.2 |
| 07-09 | `09-SNMP-and-Syslog.md` | SNMP yöneticisi, ajan, MIB ve OID; get/set/trap/inform; v2c ve v3; syslog mesaj yapısı, tesisler (facility) ve şiddet seviyeleri (severity) | 04-02, 06-03 | v2 5.4, 5.6 · v1.1 4.4, 4.5 |
| 07-10 | `10-REST-APIs.md` | REST ilkeleri; CRUD ile HTTP metotlarının eşlenmesi; kimlik doğrulama türleri; JSON veri yapıları; ağ cihazı API'leri | 07-04, 06-03 | v1.1 6.5, 6.7 |
| 07-11 | `11-Browser-to-Website-Application-View.md` | **Tarayıcıya adres yazıldığında uygulama perspektifinden ne olur:** URL ayrıştırma, önbellek, HSTS, DNS, TCP, TLS, HTTP, sayfanın oluşturulması. Paket düzeyindeki ayrıntılar 08-09'da | 07-02, 07-04 | — |

### 3.9 `08-CROSS-LAYER-COMMUNICATION/`

Her senaryo aynı iskeleti izler: göndericide ne olur, her katmanda işleme, kapsülleme, ara cihazlarda ne olur (router'da çerçevenin akıbeti dahil), hangi başlıkların eklendiği/çıkarıldığı/değiştirildiği, adresleme, alıcıda decapsulation. Senaryolar basitten karmaşığa doğru sıralandı; tam web sitesi senaryosu (08-09) en sonda, öncekilerin toplamı olarak geliyor.

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 08-01 | `01-Encapsulation-Master-Model.md` | Kapsüllemenin tam modeli; başlık boyutları; her atlamada neyin değiştiği (MAC, TTL, checksum, FCS) ve neyin değişmediği (NAT hariç IP adresleri) | 03-07 | — |
| 08-02 | `02-Same-LAN-File-Transfer.md` | Aynı LAN'da dosya gönderme: ARP, switch iletimi, TCP, uygulama | 04-07, 02-06 | — |
| 08-03 | `03-Different-Subnet-Communication.md` | Başka alt ağdaki bir bilgisayarla haberleşme (ping): gateway kararı, ARP, router'da yeniden çerçeveleme | 03-07 | — |
| 08-04 | `04-Multiple-Router-Path.md` | Birden fazla router üzerinden veri: her atlamadaki başlık değişimleri, TTL, yönlendirme kararları | 03-09 | — |
| 08-05 | `05-WiFi-Communication.md` | Wi-Fi üzerinden haberleşme: ilişkilendirme, 802.11'den 802.3'e dönüşüm, AP'nin köprü rolü, DHCP | 02-15, 07-03 | — |
| 08-06 | `06-DNS-Resolution-End-to-End.md` | Bir alan adının çözümlenmesi: stub resolver, özyinelemeli çözümleyici, kök/TLD/yetkili sunucular, önbellek | 07-02 | — |
| 08-07 | `07-TCP-Connection-End-to-End.md` | Bir TCP bağlantısının kurulması, veri aktarımı ve kapanması; her segmentin kablodaki görünümü | 04-05 | — |
| 08-08 | `08-HTTPS-to-Remote-Server.md` | Uzak bir HTTPS sunucusuna erişim: ev router'ında PAT, İnternet yolu, TLS, HTTP | 06-06, 03-20 | — |
| 08-09 | `09-Opening-a-Website-Full-Journey.md` | **Ana senaryo:** Wi-Fi'deki dizüstü bilgisayardan veri merkezindeki web sunucusuna; tüm katmanlar ve tüm ara cihazlar | 08-02 … 08-08 | — |
| 08-10 | `10-When-Connections-Fail.md` | Bağlantı koptuğunda ne olur: kablo, VLAN, gateway, DNS, TCP RST, firewall'un sessizce düşürmesi, MTU kara deliği; her durumun belirtisi | 08-09, 11-01 | v2 2.4 |

### 3.10 `11-TROUBLESHOOTING/`

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 11-01 | `01-Troubleshooting-Methodology.md` | Top-down, bottom-up, böl ve fethet, yolu izle, karşılaştır/değiştir; hipotez-test döngüsü; dokümantasyon | 00-09 | v2 2.4 |
| 11-02 | `02-Cisco-Show-and-Debug-Toolkit.md` | Show komutları, `show logging`, ping, extended ping, traceroute; debug kullanırken dikkat edilecekler; paket yakalama çıktısı | 03-11 | v2 2.4 |
| 11-03 | `03-Host-Side-Troubleshooting-Windows-macOS-Linux.md` | IP yapılandırmasının, erişilebilirliğin ve kablosuz ayarlarının üç işletim sisteminde doğrulanması | 03-06 | v2 1.6 · v1.1 1.10 |
| 11-04 | `04-Layer-by-Layer-Fault-Catalog.md` | Belirti → olası neden → doğrulama komutu tablosu (L1–L7) | Faz 1–11 | v2 2.4 |
| 11-05 | `05-Case-Studies.md` | Gerçekçi arıza biletleri ve çözüm süreçleri | 11-04 | v2 2.4 |

### 3.11 `12-REVISION/`

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 12-01 | `01-Spaced-Repetition-Guide.md` | Aralıklı tekrar ve karışık tekrar (interleaving) nasıl uygulanır; iyi tekrar kartı yazma kuralları | — | — |
| 12-02 | `02-Flashcards-by-Module.md` | Modül modül tekrar kartları. Her teori dosyası tamamlandıkça büyür; ileride Anki'ye aktarılabilir | sürekli | — |
| 12-03 | `03-Cheat-Sheets.md` | Alt ağ tabloları, port numaraları, başlık alanları, sık kullanılan komutlar | sürekli | — |

### 3.12 `13-CCNA-EXAM-PREPARATION/`

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 13-01 | `01-Exam-Blueprint-Mapping.md` | Son kapsama matrisi (v2.0 ve v1.1) | tümü | tümü |
| 13-02 | `02-Exam-Strategy-and-Question-Types.md` | Sınav stratejisi, zaman yönetimi, soru kalıpları | tümü | — |
| 13-03 | `03-Gap-Analysis-and-Next-Modules.md` | Derinlemesine işlenen, giriş düzeyinde kalan ve kapsam dışı konular; önerilen sonraki modüller | tümü | — |
| 13-04 | `04-Final-Readiness-Checklist.md` | Sınava hazırlık kontrol listesi | tümü | — |

### 3.13 `14-SECURITY-FUNDAMENTALS/` [YENİ]

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 14-01 | `01-Security-Concepts.md` | Tehdit, zafiyet, istismar (exploit), azaltma; güvenlik programı (farkındalık, eğitim, fiziksel erişim); parola politikaları, MFA, sertifikalar, biyometri | 00-08 | v1.1 5.1, 5.2, 5.4 |
| 14-02 | `02-Device-Access-Control-and-AAA.md` | Yerel parolalar ve kullanıcılar; AAA; RADIUS ve TACACS+ karşılaştırması; yedek yöntem (fallback) | 07-06 | v2 4.1 · v1.1 5.3, 5.8 |
| 14-03 | `03-Access-Control-Lists.md` | Standart, genişletilmiş, numaralı ve isimli ACL; joker maske (wildcard mask); yukarıdan aşağı işleme ve örtük ret (implicit deny); yerleşim kuralları | 03-08, 04-01 | v2 4.6 · v1.1 5.6 |
| 14-04 | `04-Layer2-Attacks-and-Defenses.md` | Saldırılar: MAC flooding, VLAN hopping, sahte DHCP ve DHCP tüketme, ARP sahteciliği, sahte RA, yayın fırtınası. Savunmalar: port security, DHCP snooping, DAI; `[v2.0-FARK]` storm control, RA guard | 02-12, 02-10, 07-03, 03-17 | v2 4.7 · v1.1 5.7 |
| 14-05 | `05-VPNs-and-IPsec.md` | Siteler arası ve uzaktan erişim VPN; IKE, ESP, AH; tünel ve taşıma modu; GRE | 06-05, 03-09 | v2 4.5 · v1.1 5.5 |
| 14-06 | `06-Wireless-Security.md` | WPA, WPA2, WPA3; PSK ve Enterprise (802.1X/EAP); SAE | 02-15, 06-05 | v2 1.5 · v1.1 5.9, 5.10 |

### 3.14 `15-NETWORK-OPERATIONS-AUTOMATION-AI/` [YENİ]

| ID | Dosya | Kapsam | Önkoşul | CCNA |
|---|---|---|---|---|
| 15-01 | `01-Network-Architectures.md` | İki ve üç katmanlı kampüs; spine-leaf; WAN; SOHO; şirket içi ve bulut | 03-19, 02-12 | v1.1 1.2 |
| 15-02 | `02-Virtualization-VMs-Containers-VRFs.md` | Tip 1 ve tip 2 hypervisor; sanal switch; konteyner ağları (veth, bridge, NAT); VRF. [DERİN] Kubernetes ağına köprü | 02-08, 03-07 | v2 1.2 · v1.1 1.12 |
| 15-03 | `03-Network-Management-Approaches.md` | Cihaz tabanlı, bulut tabanlı, kontrolcü tabanlı ve otomasyon tabanlı yönetim; altyapının kod olarak yönetimi (IaC) | 07-09 | v2 5.3 · v1.1 6.1 |
| 15-04 | `04-Controller-Based-and-SDN.md` | Kontrol ve veri düzlemi ayrımı; underlay, overlay, fabric; northbound ve southbound API | 03-07, 07-10 | v1.1 6.2, 6.3 |
| 15-05 | `05-Configuration-Management-Ansible-Terraform.md` | Ansible ve Terraform'un yetenekleri ve farkları (agentless, push, deklaratif/prosedürel); `[v2.0-FARK]` Ansible ile komut çalıştırma | 15-03, 06-03 | v2 5.5 · v1.1 6.6 |
| 15-06 | `06-AI-in-Network-Operations.md` | Tahmine dayalı ve üretken AI, makine öğrenmesi; `[v2.0-FARK]` agentic AI'ın rolü ve sınırları; istem (prompt) seçimi: veri sınıflandırması, çıktı formatı, persona, talimatlar | 15-03 | v2 5.1, 5.2 · v1.1 6.4 |

**Toplam: 116 teori dosyası.**

## 4. Packet Tracer lab kataloğu (100 lab)

### 4.1 Hedef ortam ve cihaz temel seti

- **Hedef sürüm:** Packet Tracer 9.0. Sürüm 8.2.2 ile farklar lab yazılırken not edilecek. Kullandığın sürüm onaylanacak (bkz. PROGRESS.md, Açık Kararlar).
- **Cihazlar** (model seçimi lab yazılırken PT sürümüne göre doğrulanacak): PC-PT, Laptop-PT, Server-PT; 2960-24TT (L2 switch); 3560-24PS veya 3650-24PS (L3 switch, PoE); ISR 1941/2911 (IOS 15); ISR 4321 (IOS XE, NAT/PAT labları için); WLC-3504 ve hafif AP; Home Router; IP Phone 7960; Hub-PT; Sniffer.
- **Simulation Mode** her bloğun bir parçasıdır: PDU'yu adım adım izleme, OSI Model sekmesi, Inbound/Outbound PDU Details, olay filtreleri.

### 4.2 PT durum etiketleri

| Etiket | Anlamı |
|---|---|
| ✅ | PT'de desteklendiği biliniyor (lab yazılırken komut düzeyinde yine doğrulanacak) |
| ⚠️ | Destek kısmi ya da belirsiz; lab yazılmadan önce doğrulanacak, gerekirse alternatife geçilecek |
| ❌ | PT'de yok; alternatif (`H`, `K` ya da kavramsal alıştırma) kullanılacak |

### 4.3 Dağılım

Önerdiğin dağılım korundu, iki ayarlama yapıldı: IPv6 için ayrı bir blok açıldı (IPv6 adresleme ve statik yönlendirme v1.1'in 1.8, 1.9 ve 3.3 konularında), güvenlik ise entegrasyon bloğundan önce kendi bloğuna alındı. Lab sırası çalışma sırasıyla aynıdır.

| Seviye | Lablar | Bloklar |
|---|---|---|
| BEGINNER | LAB-001 – LAB-025 | PT ve Fiziksel Katman · Ethernet, switching, VLAN · IPv4'e giriş |
| INTERMEDIATE | LAB-026 – LAB-061 | STP ve EtherChannel · Statik yönlendirme ve ICMP · OSPF, FHRP, IPv6 · TCP/UDP · Uygulama servisleri |
| ADVANCED | LAB-062 – LAB-082 | NAT ve güvenlik · Otomasyon · Çok katmanlı entegre ağlar |
| EXPERT | LAB-083 – LAB-100 | Kurumsal arıza giderme · Kapsamlı CCNA tarzı senaryolar |

### 4.4 Pratik türleri

| Tür | Ne verilir | Çözüm | Dosya |
|---|---|---|---|
| **Y — Yönerge** | 1–3 cümlelik görev ("İki LAN'ı bir router ile bağla ve…"), başarı ölçütü, katlanmış ipucu komutları, ilgili teori. Topolojiyi, adresleri ve yapılandırmayı sen tasarlarsın | Faz başına tek bir cevap dosyasında: kısa çözüm, neden çalıştığı, `[PT-SINIRI]` notları | `09-PACKET-TRACER-LABS/DRILLS/DRILLS-FNN.md` → `DRILLS/answers/DRILLS-FNN-ANSWERS.md` |
| **T — Tam lab** | README.md'deki 17 maddelik şablon: topoloji, adresleme tablosu, görevler; arıza avında hatalı yapılandırmalar metin olarak | Ayrı çözüm dosyası | `09-PACKET-TRACER-LABS/<SEVİYE>/LAB-NNN-<slug>.md` → `<SEVİYE>/solutions/LAB-NNN-<slug>-SOLUTION.md` |

Tam lab yalnızca, verilmesi gereken bir şey olduğunda kullanılır: hatalı yapılandırma (arıza avı), kesin gereksinim listesi (entegrasyon ve sınav tarzı görevler) ya da hatalı bir diyagram. Bu yüzden **31 tam lab, 69 yönerge** var. `⏸` işaretli lablar Faz 14'e ertelendi.

### 4.5 Katalog

#### BEGINNER

| ID | Tür | Başlık | OSI | Ana kavramlar | CCNA (v1.1 · v2.0) | PT |
|---|---|---|---|---|---|---|
| LAB-001 | Y | PT'ye giriş: ilk ağ, Realtime ve Simulation modları | L1–L3 | Cihaz ekleme, kablolama, ping, olay listesi | v1.1 1.1 · v2 2.4 | ✅ |
| LAB-002 | Y | Simulation Mode'da PDU incelemesi | L1–L7 | OSI Model sekmesi, Inbound/Outbound PDU Details, filtreler | dolaylı · v2 2.4 | ✅ |
| LAB-003 | Y | Kablo türleri ve bağlantı durumları | L1 | Düz, çapraz, konsol, fiber, seri kablo; link göstergeleri; Auto-MDIX | v1.1 1.3 · v2 1.1 | ✅ (Auto-MDIX davranışı ⚠️) |
| LAB-004 | Y | Hub ve switch: çarpışma alanları | L1–L2 | Paylaşımlı ortam, çarpışma gözlemi, mikrosegmentasyon | v1.1 1.3 · v2 1.1 | ✅ |
| LAB-005 | Y | Konsol erişimi ve IOS komut modları | Yönetim | Konsol; user EXEC, privileged EXEC, global config; yardım ve kısaltmalar | v1.1 2.8 | ✅ |
| LAB-006 | Y | Temel cihaz yapılandırması ve yapılandırma dosyaları | Yönetim | hostname, banner, enable secret, yerel kullanıcı, running ve startup config | v1.1 5.3 · v2 4.1 | ✅ |
| LAB-007 | Y | Arayüz durumları ve sayaçları | L1–L2 | up/down, administratively down, err-disabled; `show interfaces` sayaçları | v1.1 1.4 · v2 1.1, 2.4 | ✅ |
| LAB-008 | Y | Hız, duplex ve otomatik anlaşma | L1 | Autonegotiation; duplex uyumsuzluğunun belirtileri (late collision, CRC) | v1.1 1.4 · v2 1.1 | ⚠️ (+ çıktı yorumlama) |
| LAB-009 | Y | Seri WAN bağlantısı: DCE/DTE ve clock rate | L1–L2 | Seri arayüz, clock rate, HDLC kapsüllemesi | — | ✅ |
| LAB-010 | Y | Ev tipi kablosuz ağ | L1–L2 | SSID, WPA2-PSK, bant ve kanal seçimi, istemci ilişkilendirmesi | v1.1 1.11, 5.10 · v2 1.5 | ✅ (ALT: H04) |
| LAB-011 | T | Fiziksel katman arıza avı (break-fix) | L1 | Yanlış kablo, kapalı arayüz, err-disabled, yanlış port | v1.1 1.4 · v2 1.1 | ✅ |
| LAB-012 | Y | Ethernet çerçevesini incelemek | L2 | Alanlar, EtherType, FCS, MAC adres türleri | v1.1 1.13 | ✅ |
| LAB-013 | Y | MAC adres tablosu: öğrenme, yaşlanma, flooding | L2 | Öğrenme, aging, bilinmeyen unicast, broadcast | v1.1 1.13 | ✅ |
| LAB-014 | Y | Switch yönetimi: yönetim SVI'ı ve Telnet | L2–L3, L7 | VLAN 1 SVI, `ip default-gateway`, VTY hatları, Telnet | v1.1 2.8 · v2 2.1 | ✅ |
| LAB-015 | Y | VLAN'lar ve access portlar | L2 | VLAN oluşturma, access port, yayın alanlarının ayrılması | v1.1 2.1 · v2 2.2 | ✅ |
| LAB-016 | Y | 802.1Q trunk ile çok switch'li VLAN'lar | L2 | Trunk yapılandırması, etiketin PDU'da gözlemlenmesi | v1.1 2.2 · v2 2.1 | ✅ |
| LAB-017 | Y | Native VLAN, izinli VLAN'lar ve DTP | L2 | Native VLAN uyumsuzluğu, allowed list, DTP modları, nonegotiate | v1.1 2.2 · v2 2.1 | ✅ |
| LAB-018 | Y | Voice VLAN, IP telefon ve edge port profilleri | L1–L2 | Voice VLAN, PoE, uç cihaz türüne göre port ayarı | v1.1 1.1, 2.1 · v2 2.2 | ✅ (PoE ⚠️) |
| LAB-019 | Y | CDP ve LLDP ile dokümantasyon doğrulama | L2 | Komşu keşfi, bulguların diyagramla karşılaştırılması | v1.1 2.3 · v2 2.3 | ✅ |
| LAB-020 | T | VLAN ve trunk arıza avı (break-fix) | L2 | Yanlış VLAN; trunk, native ve allowed list hataları | v1.1 2.2 · v2 2.1, 2.4 | ✅ |
| LAB-021 | Y | ARP iş başında | L2–L3 | ARP önbelleği, istek ve yanıt, gateway'in ARP'ı | dolaylı · v2 2.4 | ✅ |
| LAB-022 | Y | Host IPv4 yapılandırması ve default gateway | L3 | Yerel/uzak kararı; gateway'in eksik ya da yanlış olması | v1.1 1.6 · v2 1.3 | ✅ |
| LAB-023 | Y | Router ile iki LAN: MAC başlığının yeniden yazılması | L2–L3 | Router arayüzleri; her atlamada MAC ve IP değerlerinin izlenmesi | v1.1 3.1, 3.2 · v2 2.4, 3.1 | ✅ |
| LAB-024 | Y | FLSM alt ağ tasarımı ve uygulaması | L3 | Eşit boyutlu alt ağlar, adres planı | v1.1 1.6 · v2 1.3 | ✅ |
| LAB-025 | Y | VLSM adres planı: çok şubeli kurum | L3 | VLSM, /30 ve /31 bağlantılar, dokümantasyon | v1.1 1.6 · v2 1.3 | ✅ (/31 ⚠️) |

#### INTERMEDIATE

| ID | Tür | Başlık | OSI | Ana kavramlar | CCNA (v1.1 · v2.0) | PT |
|---|---|---|---|---|---|---|
| LAB-026 | Y | STP: döngü, yayın fırtınası ve kök köprü seçimi | L2 | Bridge ID, root seçimi, port rolleri | v1.1 2.5 · v2 2.5 | ✅ |
| LAB-027 | Y | Rapid PVST+: VLAN başına kök ve port durumları | L2 | root primary/secondary, maliyet, roller ve durumlar | v1.1 2.5 · v2 2.5 | ✅ |
| LAB-028 | Y | PortFast, BPDU Guard, Root Guard, Loop Guard | L2 | Koruma özellikleri, err-disabled | v1.1 2.5 · v2 2.5 | ✅ (Loop Guard ⚠️) |
| LAB-029 | Y | EtherChannel: LACP, PAgP ve statik | L2 | Mod uyumu, port-channel doğrulama | v1.1 2.4 · v2 2.1, 2.2 | ✅ |
| LAB-030 | T | STP ve EtherChannel arıza avı (break-fix) | L2 | Uyumsuz parametreler, yanlış kök köprü | v1.1 2.5 · v2 2.4, 2.5 | ✅ |
| LAB-031 | Y | Statik yönlendirme: üç router | L3 | Ağ rotaları, next-hop ve çıkış arayüzü | v1.1 3.3 · v2 3.2 | ✅ |
| LAB-032 | Y | Varsayılan rota ve floating static yedek | L3 | Default route, AD ile yedekleme | v1.1 3.3 · v2 3.2 | ✅ |
| LAB-033 | Y | Host rotaları, özet rotalar ve en uzun önek eşleşmesi | L3 | /32 rotalar, özetleme, LPM | v1.1 3.2, 3.3 · v2 3.1, 3.2 | ✅ |
| LAB-034 | Y | Router-on-a-stick ile VLAN'lar arası yönlendirme | L2–L3 | Alt arayüzler, `encapsulation dot1Q` | v1.1 2.1 · v2 2.1 | ✅ |
| LAB-035 | Y | L3 switch: SVI, routed port ve L3 EtherChannel | L2–L3 | `ip routing`, `no switchport`, L3 port-channel | v1.1 2.1, 2.4 · v2 2.1 | ✅ |
| LAB-036 | Y | ICMP: ping, extended ping, traceroute ve TTL | L3 | Echo, Time Exceeded, Destination Unreachable | dolaylı · v2 2.4 | ✅ |
| LAB-037 | Y | MTU ve parçalanma | L3 | MTU, DF biti, parçalanma alanları | — | ⚠️ (ALT: H05) |
| LAB-038 | Y | Yönlendirme tablosu yorumlama | L3 | Rota kodları, AD, metrik, connected ve local rotalar | v1.1 3.1, 3.2 · v2 3.1 | ✅ |
| LAB-039 | T | Statik yönlendirme arıza avı (break-fix) | L3 | Eksik ya da yanlış rota, dönüş yolu, yanlış maske | v1.1 3.3 · v2 3.2 | ✅ |
| LAB-040 | Y | OSPFv2: point-to-point komşuluk ve router ID | L3 | Komşuluk kurulması, router ID seçimi | v1.1 3.4 · v2 3.3 | ✅ |
| LAB-041 | Y | OSPFv2: broadcast ağlarda DR/BDR seçimi | L3 | Öncelik, DR/BDR, komşuluk durumları | v1.1 3.4 · v2 3.3 | ✅ |
| LAB-042 | Y | OSPF maliyeti, passive-interface, default-information originate | L3 | Maliyet hesabı, reference bandwidth, varsayılan rotanın yayılması | v1.1 3.4 · v2 3.3 | ✅ |
| LAB-043 | T | OSPF komşuluk arıza avı (break-fix) | L3 | Hello/dead, alan, alt ağ, router ID çakışması, MTU | v1.1 3.4 · v2 3.3, 2.4 | ✅ (MTU ⚠️) |
| LAB-044 | Y | HSRP ve FHRP durum yorumlama | L3 | Sanal IP ve MAC, öncelik, preempt | v1.1 3.5 · v2 3.4 | ✅ (VRRP ⚠️ → çıktı yorumlama) |
| LAB-045 | Y | IPv6 adresleme: GUA, link-local, EUI-64 | L3 | `ipv6 unicast-routing`, adres türleri | v1.1 1.8, 1.9 · v2 1.4 | ✅ |
| LAB-046 | Y | NDP, SLAAC ve DHCPv6 | L3 | RS/RA/NS/NA, DAD, stateless ve stateful DHCPv6 | v1.1 1.8 · v2 1.4 | ✅ (stateful DHCPv6 ⚠️) |
| LAB-047 | Y | IPv6 statik yönlendirme | L3 | Varsayılan, ağ, host ve floating rotalar | v1.1 3.3 · v2 3.2 | ✅ |
| LAB-048 | Y ⏸ | OSPFv3 tek alan | L3 | OSPFv3 komşuluk, router ID | — · v2 3.3 | ✅ |
| LAB-049 | T | Dual-stack ağ ve IPv6 arıza avı | L3 | Dual-stack doğrulama, tipik IPv6 hataları | v1.1 1.8, 3.3 · v2 1.4, 3.2 | ✅ |
| LAB-050 | Y | TCP el sıkışması ve bağlantı sonlandırma | L4 | SYN, SYN-ACK, ACK; SEQ/ACK değerleri; FIN | v1.1 1.5 | ✅ |
| LAB-051 | Y | TCP ve UDP: DNS ve HTTP trafiği | L4, L7 | Portlar, soketler, çoklama | v1.1 1.5 | ✅ |
| LAB-052 | Y | DHCPv4 sunucusu ve DORA | L2–L3, L7 | Havuz, excluded-address, DORA gözlemi | v1.1 4.3 · v2 1.7 | ✅ |
| LAB-053 | Y | DHCP relay ve router'da DHCP istemcisi | L3, L7 | `ip helper-address`, `ip address dhcp` | v1.1 4.6 · v2 1.7 | ✅ |
| LAB-054 | T | DHCPv4 arıza avı (break-fix) | L2–L3, L7 | Eksik relay, yanlış havuz ya da gateway, tükenmiş havuz | v1.1 4.6 · v2 1.7 | ✅ |
| LAB-055 | Y | DNS sunucusu ve isim çözümleme arızaları | L7 | Kayıt türleri, istemcinin DNS ayarı | v1.1 4.3 · v2 4.4 | ✅ (MX/PTR ⚠️ → H11) |
| LAB-056 | Y | HTTP ve HTTPS: web isteğini katman katman izlemek | L4–L7 | TCP 80 ve 443; TLS'in PT'deki görünümü | — | ✅ |
| LAB-057 | Y | Dosya aktarımı: TFTP ve FTP ile yedekleme | L7 | `copy running-config tftp:`, IOS imajı | v1.1 4.9 · v2 4.2 | ✅ (SCP/SFTP ⚠️ → H13) |
| LAB-058 | Y | E-posta: SMTP ve POP3 | L7 | İstemci ve sunucu ayarları, portlar | — | ✅ |
| LAB-059 | Y | SSH ile güvenli uzaktan yönetim | L7 | RSA anahtarı, `ip domain-name`, `transport input ssh` | v1.1 2.8, 4.8 · v2 4.1 | ✅ |
| LAB-060 | Y | NTP ve syslog | L7 | NTP istemci ve sunucu, `logging host`, şiddet seviyeleri | v1.1 4.2, 4.5 · v2 5.6 | ✅ |
| LAB-061 | Y | SNMP: community ve MIB sorguları | L7 | Get/Set, community, MIB tarayıcı | v1.1 4.4 · v2 5.4 | ⚠️ (ALT: H14) |

#### ADVANCED

| ID | Tür | Başlık | OSI | Ana kavramlar | CCNA (v1.1 · v2.0) | PT |
|---|---|---|---|---|---|---|
| LAB-062 | Y | Statik NAT ile sunucu yayınlama (IOS XE) | L3–L4 | inside/outside, inside local/global | v1.1 4.1 · v2 4.3 | ✅ |
| LAB-063 | Y | Dinamik NAT havuzu ve PAT | L3–L4 | Havuz, overload, çeviri tablosu | v1.1 1.7, 4.1 · v2 4.3 | ✅ |
| LAB-064 | Y | Standart ACL | L3 | Joker maske, yerleşim, örtük ret | v1.1 5.6 · v2 4.6 | ✅ |
| LAB-065 | Y | Genişletilmiş ACL | L3–L4 | Protokol ve port filtreleme, `established` | v1.1 5.6 · v2 4.6 | ✅ |
| LAB-066 | Y | İsimli ACL'ler ve VTY erişim kontrolü | L3–L4 | Sıra numaraları, düzenleme, `access-class` | v1.1 5.6 · v2 4.6 | ✅ |
| LAB-067 | Y | Port security derinlemesine | L2 | maximum, sticky, ihlal modları, err-disabled kurtarma | v1.1 5.7 · v2 4.7 | ✅ |
| LAB-068 | Y | DHCP snooping ve Dynamic ARP Inspection | L2–L3 | trusted/untrusted portlar, binding tablosu, ARP doğrulama | v1.1 5.7 · v2 4.7 | DHCP snooping ✅ · DAI ⚠️ |
| LAB-069 | Y ⏸ | Storm control ve RA guard | L2–L3 | Eşikler ve eylemler, sahte RA | — · v2 4.7 | ⚠️ (ALT: kavramsal + çıktı yorumlama) |
| LAB-070 | Y | AAA: yerel kullanıcılar, RADIUS ve TACACS+ | L7 | `aaa new-model`, sunucu grupları, yedek yöntem | v1.1 2.8, 5.8 · v2 4.1 | ✅ |
| LAB-071 | Y | Kurumsal kablosuz: WLC, hafif AP'ler ve WPA2 | L1–L2 | WLC GUI, WLAN, VLAN eşleme, WPA2-PSK ve Enterprise | v1.1 2.6, 2.7, 2.9, 5.9, 5.10 · v2 2.2, 1.5 | ✅ |
| LAB-072 | Y | Siteler arası VPN: GRE ve IPsec | L3 | Tünel arayüzü; IKE ve ESP kavramları | v1.1 5.5 · v2 4.5 | ⚠️ |
| LAB-073 | T | NAT ve ACL arıza avı (break-fix) | L3–L4 | inside/outside hataları, ACL sırası | v1.1 4.1, 5.6 · v2 4.3, 4.6 | ✅ |
| LAB-074 | Y | Kontrolcü tabanlı ağ: PT Network Controller ve REST API | L7 | REST, JSON, Python betiği | v1.1 6.2, 6.5, 6.7 · v2 5.3 | ⚠️ |
| LAB-075 | T | Küçük ofis ağını uçtan uca kurmak | L1–L7 | VLAN, inter-VLAN, DHCP, DNS, web, NAT | çoklu | ✅ |
| LAB-076 | T | Bir web sitesini açmak: tam yolculuk | L1–L7 | Ev ağı → ISS → DNS → web sunucusu; her adımda PDU | çoklu | ✅ |
| LAB-077 | T | İki katmanlı kampüs: yedekli tasarım | L2–L3 | Rapid PVST+, EtherChannel, HSRP | v1.1 1.2, 2.5, 3.5 · v2 2.1, 2.5, 3.4 | ✅ |
| LAB-078 | T | Çok şubeli WAN: OSPF, merkezi servisler, İnternet çıkışı | L3–L7 | OSPF, DHCP relay, NAT | v1.1 3.4, 4.1, 4.6 · v2 3.3, 1.7, 4.3 | ✅ |
| LAB-079 | Y | Dual-stack kurumsal servisler | L3–L7 | SLAAC ve DHCPv4, AAAA kayıtları, IPv6 statik rotalar | v1.1 1.8, 3.3, 4.3 · v2 1.4, 3.3, 4.4 | ✅ |
| LAB-080 | T | Yönetim düzlemini güvenli hale getirmek | L3–L7 | SSH, AAA, VTY ACL, NTP, syslog, SNMP | v1.1 2.8, 4.2, 4.4, 4.5, 4.8, 5.3, 5.6, 5.8 · v2 4.1, 4.6, 5.4, 5.6 | ✅ |
| LAB-081 | T | Kablolu ve kablosuz entegrasyon | L1–L3, L7 | SSID başına VLAN, DHCP, WLC–switch bağlantısı | v1.1 2.7 · v2 2.2 | ✅ |
| LAB-082 | T | Hatalı ağ diyagramını CDP/LLDP ile düzeltmek | L2–L3 | Dokümantasyon doğrulama | v1.1 2.3 · v2 2.3 | ✅ |

#### EXPERT

Arıza giderme labları (083–090) hatalı yapılandırmaları metin olarak verir. Görev; belirtiyi tanımlamak, hipotez kurmak, doğrulamak ve düzeltmektir. Her labın bir süre hedefi vardır.

| ID | Tür | Başlık | OSI | Ana kavramlar | CCNA (v1.1 · v2.0) | PT |
|---|---|---|---|---|---|---|
| LAB-083 | T | Metodoloji: "Web sitesine erişemiyorum" bileti | L1–L7 | Top-down ve bottom-up yaklaşım, hipotez-test | çoklu · v2 2.4 | ✅ |
| LAB-084 | T | Çok hatalı L2 senaryosu | L2 | VLAN, trunk, STP, EtherChannel | v1.1 2.2, 2.4 · v2 2.4, 2.5 | ✅ |
| LAB-085 | T | Çok hatalı L3 senaryosu | L3 | Adresleme, gateway, statik rota, OSPF | v1.1 1.6, 3.3, 3.4 · v2 1.3, 3.2, 3.3 | ✅ |
| LAB-086 | T | Servis arızaları: DHCP, DNS, NAT | L3–L7 | Relay, kayıt, inside/outside hataları | v1.1 4.1, 4.3 · v2 1.7, 4.3, 4.4 | ✅ |
| LAB-087 | T | Güvenlik arızaları | L2–L4 | ACL sırası, port security, snooping güven ayarı | v1.1 5.7 · v2 4.6, 4.7 | ✅ (DAI ⚠️) |
| LAB-088 | T | IPv6 arızaları | L3 | Adres, RA, statik rota ve OSPFv3 | v1.1 1.8, 3.3 · v2 1.4, 3.2, 3.3 | ✅ |
| LAB-089 | T | Arayüz ve performans arızaları | L1–L2 | Duplex, CRC, giant/runt, err-disabled | v1.1 1.4 · v2 1.1 | ⚠️ (+ çıktı yorumlama) |
| LAB-090 | T | Paket yakalama ile arıza giderme | L2–L7 | Simulation Mode ve Sniffer cihazı | çoklu · v2 2.4 | ✅ (Sniffer ⚠️) |
| LAB-091 | T | Capstone 1: KOBİ ağını sıfırdan kurmak | L1–L7 | Zaman sınırlı tam kurulum | çoklu | ✅ |
| LAB-092 | T | Capstone 2: Yüksek erişilebilir kampüs | L2–L3 | Yedeklilik, yakınsama testi | çoklu | ✅ |
| LAB-093 | Y | Capstone 3: Dual-stack çok şubeli OSPF ağı | L3 | OSPFv2, IPv6 statik rotalar, özetleme | çoklu | ✅ |
| LAB-094 | T | Capstone 4: Servisler ve güvenlik sıkılaştırma | L2–L7 | Servisler, ACL, L2 güvenlik, AAA | çoklu | ✅ |
| LAB-095 | Y | Capstone 5: Şube, kablosuz ve VPN | L1–L7 | WLC, şube bağlantısı, tünel | çoklu | ⚠️ (VPN) |
| LAB-096 | T | CCNA tarzı yapılandırma görevi 1 | çoklu | Süre sınırlı, eksiksiz gereksinim listesi | çoklu | ✅ |
| LAB-097 | T | CCNA tarzı yapılandırma görevi 2 | çoklu | Süre sınırlı, eksiksiz gereksinim listesi | çoklu | ✅ |
| LAB-098 | T | CCNA tarzı arıza giderme görevi 1 | çoklu | Süre sınırlı, birden fazla hata | çoklu | ✅ |
| LAB-099 | T | CCNA tarzı arıza giderme görevi 2 | çoklu | Süre sınırlı, birden fazla hata | çoklu | ✅ |
| LAB-100 | T | Final: tasarla, kur, belgele, boz-düzelt | L1–L7 | Gereksinimden tasarıma, kuruluma, dokümantasyona ve arıza gidermeye | çoklu | ✅ |

## 5. Gerçek host ve kod labları (`16-REAL-HOST-LABS/`) [YENİ]

Bu labların amacı, PT'nin gösteremediği şeyleri gerçek cihazlarda görmektir: gerçek baytlar, gerçek işletim sistemleri, gerçek protokol davranışları. Windows, macOS ve Linux (Fedora) ortamlarında çalışacak şekilde yazılacaklar. Linux labları Fedora'da yapılacak. "Faz" sütunu labın yapılacağı fazı gösterir; 14 = sınav sonrası.

### 5.1 `HOST/`

| ID | Başlık | İlgili teori | CCNA | Faz |
|---|---|---|---|---|
| H01 | IP yapılandırmasını doğrulamak: Windows, macOS, Linux | 03-06, 11-03 | v2 1.6 · v1.1 1.10 | 4 |
| H02 | Wireshark'a giriş: ilk yakalama, Ethernet çerçevesinin alanları, FCS ve checksum offload uyarısı | 00-09, 02-03 | v2 2.4 | 3 |
| H03 | ARP ve IPv6 NDP trafiğini yakalamak | 02-10, 03-17 | v2 1.4 | 6 |
| H04 | Kablosuz ortam analizi: bant, kanal, RSSI, girişim | 01-08 | v2 1.5, 1.6 | 2 |
| H05 | MTU ve PMTUD: DF bitli ping | 03-12 | — | 14 |
| H06 | traceroute türleri: Windows'ta ICMP, Linux ve macOS'ta UDP | 03-11 | v2 2.4 | 5 |
| H07 | TCP'yi Wireshark'ta incelemek: el sıkışma, pencere, yeniden iletim; `ss` ve `netstat` | 04-03 – 04-05 | v1.1 1.5 | 7 |
| H08 | UDP ve QUIC trafiğini gözlemlemek | 04-02, 04-06 | v1.1 1.5 | 14 |
| H09 | TLS 1.3 el sıkışması: Wireshark ve `openssl s_client` | 06-06 | — | 14 |
| H10 | HTTP'yi `curl -v` ile çözümlemek | 07-04 | — | 14 |
| H11 | DNS'i `dig` ve `nslookup` ile incelemek: A, AAAA, CNAME, MX, NS, PTR | 07-02 | v2 4.4 | 9 |
| H12 | DHCP'yi gerçek host'ta izlemek: release/renew ve DORA yakalama | 07-03 | v2 1.7 | 9 |
| H13 | SSH, SCP ve SFTP | 07-06, 07-07 | v2 4.2 | 9 |
| H14 | Linux'ta syslog ve SNMP | 07-09 | v2 5.4, 5.6 | 14 |
| H15 | Hypervisor ağ modları: VirtualBox NAT, bridged, host-only, internal | 15-02 | v2 1.2 | 14 |
| H16 | Linux network namespace, veth ve bridge ile "switch" ve "router" kurmak | 15-02, 02-06, 03-07 | v2 1.2 | 14 |
| H17 | Docker ağları: bridge, port yayınlama, NAT kuralları | 15-02, 03-20 | v2 1.2 | 14 |
| H18 | Ansible ile komut çalıştırmak | 15-05 | v2 5.5 | 14 |
| H19 | Ağ operasyonları için üretken AI istemi seçmek | 15-06 | v2 5.2 | 14 |

### 5.2 `CODE/` — "Kodla-Anla" (Python)

Bir mekanizmayı kodla yazmak, onu gerçekten anlayıp anlamadığını sınar. Bu alıştırmalar kısa tutulacak ve yalnızca Python standart kütüphanesi kullanılacak. Sınav takvimi nedeniyle hepsi Faz 14'e ertelendi; plandan öndeysen ilgili teori dosyasının hemen ardından yapabilirsin.

| ID | Başlık | İlgili teori | Faz |
|---|---|---|---|
| K01 | Sayı sistemi dönüştürücü ve bit işlemleri | 00-02, 00-03 | 14 |
| K02 | Hat kodlaması simülatörü: NRZ, Manchester, MLT-3 | 01-03 | 14 |
| K03 | CRC-32 hesaplamak ve bozuk çerçeveyi yakalamak | 02-04 | 14 |
| K04 | Oyuncak switch: MAC öğrenme ve flooding simülasyonu | 02-06 | 14 |
| K05 | IPv4 başlık checksum'ı ve alt ağ hesaplayıcı | 03-02, 03-04 | 14 |
| K06 | Mini router: en uzun önek eşleşmesiyle tablo araması | 03-08 | 14 |
| K07 | Soket programlama: TCP ve UDP echo sunucusu | 04-07 | 14 |
| K08 | UTF-8 kodlayıcı/çözücü ve Base64 | 06-02, 06-03 | 14 |

## 6. Soru bankası tasarımı (`10-QUESTION-BANK/`)

### 6.1 Soru kategorileri

| Kod | Kategori | Ne ölçer |
|---|---|---|
| B | Temel anlama | Kavramın doğru tanımı ve rolü |
| O | Orta düzey teknik | Alan değerleri, davranışlar, komut çıktıları |
| İ | İleri muhakeme | Neden-sonuç; "şu değişirse ne olur" |
| S | Gerçek dünya senaryosu | Bilgiyi verilen ağa uygulama |
| A | Arıza giderme | Belirtiden nedene ulaşma |
| MC | CCNA tarzı çoktan seçmeli | Sınav formatı; tek veya çok cevaplı |
| K | Kendi cümlelerinle | Açık uçlu; cevap anahtarında puanlama ölçütleri (rubric) |
| KK | Karşılaştır | İki teknolojinin ne zaman ve neden seçildiği |

### 6.2 Dosya düzeni

- Soru dosyası: `10-QUESTION-BANK/<ALAN>/Q-<ALAN>-<KONU>.md`. Her soruda kimlik, kategori, zorluk (1–3) ve teori bağlantısı bulunur.
- Cevap dosyası: `10-QUESTION-BANK/<ALAN>/answers/A-<ALAN>-<KONU>.md`. Her cevapta doğru cevap, ayrıntılı açıklama, çeldiricilerin neden yanlış olduğu ve teori bağlantısı (ör. `→ 03-04, Bölüm 3`) bulunur.
- Klasörler: `FOUNDATIONS/`, `PHYSICAL/`, `DATA-LINK/`, `NETWORK/`, `TRANSPORT/`, `SESSION/`, `PRESENTATION/`, `APPLICATION/`, `SECURITY/` [YENİ], `OPERATIONS/` [YENİ], `COMPREHENSIVE-EXAMS/`.

### 6.3 Hedef sayılar

Bu sayılar kota değil, yön göstergesidir. Kalite önceliklidir; birbirini tekrar eden sorular yazılmaz.

| Alan | Hedef | Alan | Hedef |
|---|---|---|---|
| FND | ~40 | PRS | ~30 |
| PHY | ~40 | APP | ~60 |
| DL | ~70 | SEC | ~50 |
| NET | ~120 | OPS | ~30 |
| TRN | ~40 | SES | ~10 |

### 6.4 Kapsamlı sınavlar

CE-01 – CE-06 kümülatiftir; her birinde soruların yaklaşık %30'u önceki fazlardan gelir (karışık tekrar). CE-00 ise başlangıç düzeyini ölçen bir tanı testidir; puanı ustalık seviyesine sayılmaz.

| ID | Ne zaman | Kapsam | Yaklaşık soru |
|---|---|---|---|
| CE-00 | Faz 0 | Tanı testi: mevcut notlardaki (USR-OSI-NOTES, Bölüm 19) 25 soru, bu kez cevap anahtarı ve açıklamalarla | 25 |
| CE-01 | Faz 4 sonu | Temeller, L1, L2-I, IPv4 | 40 |
| CE-02 | Faz 6 sonu | L1–L3 tamamı | 50 |
| CE-03 | Faz 9 sonu | Yedi katmanın tamamı | 60 |
| CE-04 | Faz 11 sonu | Güvenlik ve operasyon dahil her şey | 60 |
| CE-05 | Faz 13 | CCNA tarzı deneme sınavı 1 | 100 |
| CE-06 | Faz 13 | CCNA tarzı deneme sınavı 2 | 100 |

## 7. Diyagram planı

| Konu | Dosya | Tür |
|---|---|---|
| İkili temsil ve 2'nin kuvvetleri | 00-02 | ASCII tablo |
| Transistörün anahtarlaması ve CMOS NOT kapısı | 00-05 | ASCII devre + açıklama |
| Bitten sinyale hat | 01-01 | Mermaid flowchart |
| Hat kodlaması dalga biçimleri | 01-03 | ASCII dalga biçimi |
| Diferansiyel sinyal ve büküm | 01-06 | ASCII |
| Fiberde tam iç yansıma | 01-07 | ASCII |
| Ethernet çerçevesi ve 802.1Q etiketi | 02-03, 02-09 | RFC tarzı bit diyagramı |
| Switch'in karar akışı ve MAC öğrenme | 02-06 | Mermaid flowchart + sequenceDiagram |
| VLAN ayrımı | 02-08 | Mermaid flowchart |
| STP topolojisi ve port rolleri | 02-11 | Mermaid flowchart |
| IPv4 ve IPv6 başlıkları | 03-02, 03-16 | RFC tarzı bit diyagramı |
| Subnetting bit tablosu | 03-04 | ASCII tablo |
| Host'un yerel/uzak kararı | 03-06 | Mermaid flowchart |
| Router iletim hattı (pipeline) | 03-07 | Mermaid flowchart |
| OSPF komşuluk durumları | 03-14 | Mermaid stateDiagram |
| NAT çevirisi | 03-20 | Mermaid sequenceDiagram |
| TCP el sıkışması ve durum makinesi | 04-03 | Mermaid sequenceDiagram + stateDiagram |
| Tıkanıklık penceresinin değişimi | 04-05 | ASCII grafik |
| TLS 1.3 el sıkışması | 06-06 | Mermaid sequenceDiagram |
| DNS çözümleme ve DHCP DORA | 07-02, 07-03 | Mermaid sequenceDiagram |
| Kapsülleme ve decapsulation | 08-01 | ASCII katman yığını |
| Uçtan uca yolculuk | 08-09 | Mermaid sequenceDiagram + atlama tablosu |

## 8. Packet Tracer'ın sınırları ve alternatifler

| Konu | PT | Alternatif |
|---|---|---|
| Sinyal, zayıflama, EMI, mesafe | ❌ | 01-05 kavramsal alıştırmalar, K02, gerçek Cisco çıktılarının yorumlanması |
| Duplex uyumsuzluğunun belirtileri | ⚠️ | Gerçek çıktı örnekleriyle yorumlama (LAB-008, LAB-089) |
| Gerçek işletim sistemi istemcileri | ❌ (PT PC'leri genel amaçlıdır) | H01, H04, 11-03 |
| Ham paket baytları | ⚠️ (PDU Details var, ham bayt yok) | H02, H07–H12 |
| MTU ve PMTUD | ⚠️ | H05 |
| TCP tıkanıklık kontrolü | ❌ | H07, 04-05 |
| TLS ayrıntıları | ⚠️ (HTTPS var, el sıkışma ayrıntısı yok) | H09 |
| DNS MX ve PTR kayıtları | ⚠️ | H11 |
| SCP ve SFTP | ⚠️ | H13 |
| SNMP | ⚠️ | H14 |
| VRRP | ⚠️ | 03-19'da çıktı yorumlama |
| DAI, storm control, RA guard | ⚠️ | 14-04'te kavramsal alıştırma ve çıktı yorumlama |
| Hypervisor ve konteyner ağları | ❌ | H15–H17 |
| Ansible | ❌ | H18 |
| Agentic AI ve üretken AI | ❌ | 15-06, H19 |

## 9. CCNA eşlemesi

Kaynaklar: v1.1 için Cisco'nun resmi PDF'i (CISCO-V11), v2.0 için resmi PDF (CISCO-V2). Konu adları kısaltılarak, kendi cümlelerimle verilmiştir. Son ve ayrıntılı matris 13-01'de hazırlanacak.

### 9.1 v1.1 (birincil hedef; son sınav günü 2 Şubat 2027) — 6 alan, 53 konu

| Kod | Konu (özet) | Teori | Pratik |
|---|---|---|---|
| **1.0** | **Network Fundamentals (%20)** | | |
| 1.1 | Ağ bileşenlerinin rolü (router, L2/L3 switch, NGFW/IPS, AP, kontrolcü, uç cihaz, sunucu, PoE) | 00-08, 01-06 | LAB-001, LAB-018 |
| 1.2 | Topoloji mimarileri (iki/üç katman, spine-leaf, WAN, SOHO, şirket içi ve bulut) | 15-01 | LAB-077 |
| 1.3 | Fiziksel arayüz ve kablo türleri; paylaşımlı ortam ve noktadan noktaya | 01-06, 01-07, 01-09, 02-05 | LAB-003, LAB-004 |
| 1.4 | Arayüz ve kablo sorunları (çarpışma, hata, duplex/hız uyumsuzluğu) | 01-10, 02-05 | LAB-007, LAB-008, LAB-011, LAB-089 |
| 1.5 | TCP ve UDP karşılaştırması | 04-01 – 04-06 | LAB-050, LAB-051; H07 |
| 1.6 | IPv4 adresleme ve subnetting | 03-03 – 03-06 | LAB-022, LAB-024, LAB-025, LAB-085 |
| 1.7 | Özel IPv4 adreslemenin gereği | 03-03, 03-20 | LAB-063 |
| 1.8 | IPv6 adresleme ve önek | 03-16, 03-17 | LAB-045, LAB-046, LAB-049, LAB-088 |
| 1.9 | IPv6 adres türleri (GUA, ULA, link-local, anycast, multicast, EUI-64) | 03-16 | LAB-045 |
| 1.10 | İstemci işletim sistemlerinde IP parametrelerini doğrulama | 03-06, 11-03 | H01 |
| 1.11 | Kablosuz ilkeler (örtüşmeyen kanallar, SSID, RF, şifreleme) | 01-08, 02-15, 14-06 | LAB-010; H04 |
| 1.12 | Sanallaştırma temelleri (sunucu sanallaştırma, konteyner, VRF) | 15-02 | — (kavramsal) |
| 1.13 | Switching kavramları (MAC öğrenme ve aging, iletim, flooding, MAC tablosu) | 02-06, 02-07 | LAB-012, LAB-013 |
| **2.0** | **Network Access (%20)** | | |
| 2.1 | VLAN'lar (data ve voice access port, default VLAN, VLAN'lar arası bağlantı) | 02-08, 03-10 | LAB-015, LAB-018, LAB-034, LAB-035 |
| 2.2 | Switch'ler arası bağlantı (trunk, 802.1Q, native VLAN) | 02-09 | LAB-016, LAB-017, LAB-020, LAB-084 |
| 2.3 | CDP ve LLDP | 02-14 | LAB-019, LAB-082 |
| 2.4 | L2/L3 EtherChannel (LACP) | 02-13 | LAB-029, LAB-035, LAB-084 |
| 2.5 | Rapid PVST+ (root, port rolleri ve durumları, PortFast, root/loop guard, BPDU filter/guard) | 02-11, 02-12 | LAB-026 – LAB-028, LAB-030, LAB-077 |
| 2.6 | Cisco kablosuz mimarileri ve AP modları | 02-16 | LAB-071 |
| 2.7 | WLAN bileşenlerinin fiziksel bağlantıları (AP, WLC, access/trunk port, LAG) | 02-16 | LAB-071, LAB-081 |
| 2.8 | Cihaz yönetim erişimi (Telnet, SSH, HTTP/HTTPS, konsol, TACACS+/RADIUS, bulut yönetimi) | 07-06, 14-02, 15-03 | LAB-005, LAB-014, LAB-059, LAB-070, LAB-080 |
| 2.9 | WLAN GUI yapılandırmasını yorumlama | 02-16, 14-06 | LAB-071 |
| **3.0** | **IP Connectivity (%25)** | | |
| 3.1 | Yönlendirme tablosunun bileşenleri | 03-08 | LAB-023, LAB-038 |
| 3.2 | Router'ın iletim kararı (LPM, AD, metrik) | 03-07, 03-08 | LAB-023, LAB-033, LAB-038 |
| 3.3 | IPv4 ve IPv6 statik yönlendirme (default, ağ, host, floating) | 03-09, 03-18 | LAB-031 – LAB-033, LAB-039, LAB-047, LAB-049, LAB-085, LAB-088 |
| 3.4 | Tek alan OSPFv2 (komşuluk, point-to-point, broadcast DR/BDR, router ID) | 03-14, 03-15 | LAB-040 – LAB-043, LAB-078, LAB-085 |
| 3.5 | İlk atlama yedeklilik protokolleri (FHRP) | 03-19 | LAB-044, LAB-077 |
| **4.0** | **IP Services (%10)** | | |
| 4.1 | Inside source NAT (statik ve havuz) | 03-20 | LAB-062, LAB-063, LAB-073, LAB-078, LAB-086 |
| 4.2 | NTP istemci ve sunucu modu | 07-08 | LAB-060, LAB-080 |
| 4.3 | DHCP ve DNS'in ağdaki rolü | 07-02, 07-03 | LAB-052, LAB-055, LAB-086; H11, H12 |
| 4.4 | SNMP'nin işlevi | 07-09 | LAB-061, LAB-080 |
| 4.5 | Syslog tesisleri ve şiddet seviyeleri | 07-09 | LAB-060, LAB-080 |
| 4.6 | DHCP istemci ve relay | 07-03 | LAB-053, LAB-054, LAB-078 |
| 4.7 | QoS atlama başına davranış | 03-21 | — (kavramsal) |
| 4.8 | SSH ile uzaktan erişim | 07-06 | LAB-059, LAB-080; H13 |
| 4.9 | TFTP ve FTP | 07-07 | LAB-057 |
| **5.0** | **Security Fundamentals (%15)** | | |
| 5.1 | Güvenlik kavramları (tehdit, zafiyet, istismar, azaltma) | 14-01 | — (kavramsal) |
| 5.2 | Güvenlik programı (farkındalık, eğitim, fiziksel erişim) | 14-01 | — (kavramsal) |
| 5.3 | Yerel parolalarla cihaz erişim kontrolü | 14-02 | LAB-006, LAB-080 |
| 5.4 | Parola politikası (yönetim, karmaşıklık, MFA, sertifika, biyometri) | 14-01 | — (kavramsal) |
| 5.5 | IPsec uzaktan erişim ve siteler arası VPN | 06-05, 14-05 | LAB-072 |
| 5.6 | ACL'ler | 14-03 | LAB-064 – LAB-066, LAB-073, LAB-080 |
| 5.7 | L2 güvenlik (DHCP snooping, DAI, port security) | 14-04 | LAB-067, LAB-068, LAB-087 |
| 5.8 | AAA kavramları | 14-02 | LAB-070, LAB-080 |
| 5.9 | WPA, WPA2, WPA3 | 14-06 | LAB-071 |
| 5.10 | GUI'de WPA2-PSK WLAN yapılandırması | 14-06 | LAB-010, LAB-071 |
| **6.0** | **Automation and Programmability (%10)** | | |
| 6.1 | Otomasyonun ağ yönetimine etkisi | 15-03 | — (kavramsal) |
| 6.2 | Geleneksel ve kontrolcü tabanlı ağ | 03-01, 15-04 | LAB-074 |
| 6.3 | Kontrolcü tabanlı ve yazılım tanımlı mimari (overlay, underlay, fabric; kontrol/veri düzlemi; northbound/southbound API) | 15-04 | — (kavramsal) |
| 6.4 | Ağ operasyonlarında üretken ve tahmine dayalı AI, makine öğrenmesi | 15-06 | — (kavramsal) |
| 6.5 | REST API özellikleri (kimlik doğrulama, CRUD, HTTP fiilleri, veri kodlama) | 07-10 | LAB-074 |
| 6.6 | Yapılandırma yönetimi araçları (Ansible, Terraform) | 15-05 | — (kavramsal; H18 Faz 14'te) |
| 6.7 | JSON verisinin bileşenleri | 06-03, 07-10 | LAB-074 |

### 9.2 v2.0 farkları (Faz 14; sınav 2 Şubat'tan sonraya kalırsa önce bunlar)

| v2.0 kodu | Konu | Nerede |
|---|---|---|
| 1.2 | Hypervisor, VM ve konteynerin uygulamalı anlaşılması | 15-02; H15, H16, H17 |
| 1.7 | DHCPv4 arıza giderme (v1.1'de "yapılandır ve doğrula") | 07-03; LAB-054, LAB-086 (çekirdekte zaten var) |
| 2.2 | Uç cihaz port profilleri | LAB-018 (çekirdekte zaten var) |
| 2.4 | Paket yakalama dahil arıza giderme araçları | 11-02; LAB-090; H02 (çekirdekte zaten var) |
| 3.3 | Tek alan OSPFv3 | 03-18; LAB-048 ⏸ |
| 3.4 | VRRP durumunu yorumlama | 03-19 |
| 4.2 | SFTP ve SCP ile dosya yönetimi | 07-07; H13 |
| 4.4 | DNS kayıt arızalarını teşhis | 07-02; LAB-055; H11 |
| 4.7 | Storm control ve RA guard | 14-04; LAB-069 ⏸ |
| 5.1, 5.2 | Agentic AI; üretken AI için istem seçimi | 15-06; H19 |
| 5.3 | Ağ yönetim yaklaşımları ve IaC | 15-03 |
| 5.5 | Ansible ile komut çalıştırma | 15-05; H18 |

### 9.3 Kapsam dışı (ön liste, 13-03'te kesinleşecek)

Çok alanlı OSPF, EIGRP ve BGP'nin yapılandırması (03-13'teki kavramsal giriş dışında), MPLS, SD-WAN'ın ayrıntıları, multicast yönlendirme, ileri düzey QoS yapılandırması, bulut sağlayıcı ağları (AWS VPC vb.), Kubernetes CNI'ın ayrıntıları, Python ile ağ otomasyonunun ileri düzeyi.

## 10. Eksikler, iyileştirmeler ve gerekçeler

1. **CCNA sürümü.** Prompt v1.1'e göre yazılmıştı; Mayıs 2026'da v2.0 duyuruldu. Senin kararınla birincil hedef v1.1. v2.0 farkları Faz 14'te hazır tutuluyor (Bölüm 9.2). Arıza avı ağırlığı her iki sürüm için de yararlı olduğu için korundu (LAB-011, 020, 030, 039, 043, 049, 054, 073, 083–090).
2. **00-09: OSI ve TCP/IP modelleri eklendi.** Önerilen temeller listesinde modelin kendisi yoktu; katman modüllerinden önce gerekli.
3. **14-SECURITY-FUNDAMENTALS eklendi.** ACL'ler L3/L4'e, L2 savunmaları DHCP, ARP ve NDP'ye, VPN kriptografiye dayanır. Bu konular tek bir katmana ait değildir ve hepsinden sonra gelmelidir. Bu yüzden 02 modülündeki "temel L2 güvenliği" 14-04'e taşındı.
4. **15-NETWORK-OPERATIONS-AUTOMATION-AI eklendi.** v2.0'ın 5. alanı ve 1.2 konusu OSI katmanlarının hiçbirine ait değil.
5. **16-REAL-HOST-LABS eklendi.** PT; fiziksel sinyalleri, gerçek işletim sistemi istemcilerini (v2.0 1.6), Ansible'ı (5.5), SCP/SFTP'yi (4.2) ve hypervisor'ları (1.2) gösteremez. Gerçek paket yakalama (2.4) da ancak gerçek bir sistemde mümkündür.
6. **"Kodla-Anla" alıştırmaları (K01–K08).** Yazılım mühendisliği geçmişini kullanarak mekanizmaları kodla doğrulaman için. İsteğe bağlıdır.
7. **CURRICULUM.md eklendi.** STUDY-ROADMAP.md'nin "sıra", bu dosyanın "kapsam" olması tekrarı önler.
8. **Arıza giderme metodolojisi başa alındı.** 11-01 Faz 2'de okunur; her katman kendi arıza giderme bölümünü bu metodolojiye göre yazar.
9. **Lab sırası, çalışma sırasıyla aynı yapıldı.** IPv6'ya ayrı blok açıldı, güvenlik entegrasyondan önceye alındı (Bölüm 4.3).
10. **Kalıcılık.** Her oturum boş bir çalışma alanıyla başlar. Projenin bilgisayarında ya da bir Git deposunda tutulması gerekir (bkz. PROGRESS.md, Açık Kararlar).
11. **Mevcut notlarla bağlantı kuruldu.** Notlarda bulunup müfredatta eksik olan konular eklendi: SCTP (04-06), RIP, EIGRP, IS-IS ve BGP örnekleri (03-13), L4 ve L7 ara cihazları (04-01, 07-01). Cevapsız test bölümü CE-00 tanı testine dönüştürüldü (Bölüm 11).

## 11. Mevcut OSI notlarıyla ilişki (USR-OSI-NOTES)

Notlar yukarıdan aşağıya (L7 → L1) giden, genel bakış düzeyinde ve büyük ölçüde doğru bir anlatımdır. Müfredatta üç işe yarar:

1. **Başlangıç haritası:** Faz 0'da CE-00 tanı testiyle birlikte kullanılır.
2. **Yanılgı kaynağı:** Notların 17. bölümündeki 12 yanılgı, ilgili teori dosyalarının "Yaygın Yanılgılar" bölümlerine dağıtılır.
3. **Çapraz referans:** Teori dosyaları gerektiğinde notların bölüm numarasına atıf yapar (ör. "Notlar §11.14"). Notların metni bu projeye kopyalanmaz.

**Terim notu:** Notlarda "Veri Bağı Katmanı", bu müfredatta ise prompttaki "Veri Bağlantı Katmanı" kullanılıyor. GLOSSARY.md'de ikisi eş anlamlı olarak yer alacak.

### 11.1 Bölüm eşlemesi

| Notlar bölümü | Konu | Derinleştiği dosyalar |
|---|---|---|
| §1–2 | OSI'ye giriş, TCP/IP farkı, PDU, header ve trailer | 00-09, 08-01 |
| §3 | Uygulama katmanı protokolleri (HTTP, DNS, DHCP, FTP, e-posta, SSH, SNMP) | 07-01 – 07-09, 06-06 |
| §4 | Sunum katmanı (kodlama, veri biçimleri, şifreleme, sıkıştırma) | 06-01 – 06-06 |
| §5 | Oturum katmanı | 05-01, 05-02 |
| §6.1–6.5 | Portlar, TCP, UDP | 04-01 – 04-06 |
| §6.6 | SCTP | 04-06 |
| §6.7 | L4 firewall ve yük dengeleyici | 04-01, 14-03 |
| §7.1–7.4 | IP adresleme, public ve private adresler, yönlendirme tablosu, LPM | 03-01 – 03-08 |
| §7.5–7.6 | TTL ve ICMP | 03-02, 03-11 |
| §7.7 | Yönlendirme protokolleri | 03-13, 03-14, 03-15 |
| §7.8 | ARP | 02-10 |
| §8.1–8.4 | MAC adresi, Ethernet, switch | 02-02 – 02-07 |
| §8.5–8.6 | VLAN, trunk, STP | 02-08, 02-09, 02-11, 02-12 |
| §8.7 | Wi-Fi | 01-08, 02-15, 02-16, 14-06 |
| §8.8 | PPP | 02-01 |
| §9 | Fiziksel katman | 01-01 – 01-10 |
| §10 | Kapsülleme ve decapsulation | 08-01 |
| §11 | Bir paketin yolculuğu (HTTPS, NAT) | 08-03, 08-04, 08-08, 08-09 |
| §12–13 | Switch ve router farkı; MAC, IP ve port | 02-06, 03-07, 08-01 |
| §14–15 | TCP/UDP; VLAN, subnet, ARP, NAT | 04-06, 02-08, 03-04, 02-10, 03-20 |
| §16 | OSI'ye göre arıza giderme; Windows ve Linux komutları | 11-01, 11-03, 11-04, H01 |
| §17 | Sık yapılan hatalar | İlgili dosyaların "Yaygın Yanılgılar" bölümleri |
| §19 | Kendini test et (25 soru, cevap anahtarı yok) | CE-00 |

### 11.2 Düzeltilecek noktalar

Bu noktalar, karşılarındaki dosyaların "Yaygın Yanılgılar" bölümlerinde açıkça ele alınacak.

| Notlar | Notlarda yazan | Doğrusu | Ele alınacağı yer |
|---|---|---|---|
| §11.14–11.15 | Ev router'ından çıkan paketin kaynak IP'si değişmeden gösteriliyor; NAT sonraki bir aşama olarak anlatılıyor | Senaryoda NAT'ı yapan aynı ev router'ı. Bu yüzden WAN arayüzünden çıkan paketin kaynak adresi zaten public adrestir. "IP adresleri değişmez" kuralı yalnızca NAT yapılmayan atlamalar için geçerlidir | 03-20, 08-08 |
| §15.2 | "Subnetting, router'ın hedefin yerel ağda olup olmadığını anlamasına yardımcı olur" | Yerel/uzak kararını gönderen **host**, kendi IP adresi ve maskesiyle verir. Router ise yönlendirme tablosuna bakar ve en uzun önek eşleşmesini kullanır | 03-06, 03-08 |
| §7.2 | "IPv6 router'ları IPv4'teki gibi header checksum güncellemez" | IPv6 başlığında checksum alanı **hiç yoktur** (RFC 8200). Bütünlük kontrolü L2'deki FCS'e ve L4'teki checksum'a bırakılmıştır | 03-16 |
| §8.6 | "Ethernet frame'lerinde router'lardaki gibi TTL alanı bulunmaz" | TTL, router'ın değil, **IP başlığının** bir alanıdır. Ethernet çerçevesinde atlama sayacı olmadığı için L2 döngüsündeki bir çerçeve hiç ölmez | 02-11 |
| §7.7 | Yönlendirilen protokol ile yönlendirme protokolü ayrımı belirsiz bir cümleyle anlatılıyor | IP yönlendirilen (routed) protokoldür. OSPF, RIP ve BGP ise rota bilgisini dağıtan yönlendirme (routing) protokolleridir. Bunlar da farklı katmanların üzerinde çalışır (IP 89, UDP 520, TCP 179); bu, katman yerleşiminin neden tartışmalı olduğunun iyi bir örneğidir | 03-13 |

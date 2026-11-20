# FND-HW Cevap Anahtarı

> Sorular: `../Q-FND-HW.md`. Önce soruları çöz, sonra bu dosyayı aç. Puanlama kuralları: `10-QUESTION-BANK/README.md`.

---

### FND-HW-001
**Cevap:** a) **12 W**. b) **0,625 W**.

**Açıklama:** a) P = V × I = 48 × 0,25 = 12 W. b) Kayıp = I² × R = 0,25² × 10 = 0,0625 × 10 = 0,625 W.

**Puan:** Her parça 0,5.

**Teori:** → 00-04, Bölüm 3.5 ve 4.1

---

### FND-HW-002
**Cevap:** A ve C

**Açıklama:** Belirti, motorun değişen manyetik alanının veri kablosuna gürültü indüklemesidir (EMI). Gürültü, gürültü payını aşınca bitler yanlış okunur ve FCS kontrolü başarısız olur (CRC hatası). Kaynağa olan mesafeyi artırmak (A) gürültüyü azaltır. Fiber (C) ışık kullandığı için EMI'den etkilenmez.

**Çeldiriciler:**
- B) Kablo uzadıkça zayıflama artar; sorun büyür, küçülmez.
- D) Daha yüksek hız daha dar gürültü payı ve daha yüksek frekanslar demektir; sorun büyüyebilir.
- E) Yeniden başlatma, sayaçları sıfırlar ama gürültünün kaynağını ortadan kaldırmaz.

**Teori:** → 00-04, Bölüm 3.6, 5 ve 9

---

### FND-HW-003
**Cevap:** a) NMH = **0,7 V**, NML = **0,6 V**. b) **Düşük seviye (0)** risk altındadır.

**Açıklama:**
a) NMH = VOH − VIH = 3,0 − 2,3 = 0,7 V. NML = VIL − VOL = 1,0 − 0,4 = 0,6 V.
b) 0,65 V'luk gürültü, 0 gönderilirken en kötü durumda çıkışı 0,4 + 0,65 = 1,05 V'a çıkarabilir; bu VIL'in (1,0 V) üstündedir ve tanımsız bölgeye girer. 1 gönderilirken en kötü durumda 3,0 − 0,65 = 2,35 V olur; bu hâlâ VIH'in (2,3 V) üstündedir, yani güvenlidir.

**Puan:** (a) 0,5 (iki pay doğru); (b) 0,5 (doğru seviye ve gerekçe).

**Teori:** → 00-05, Bölüm 3.5; 00-01, Bölüm 3.2

---

### FND-HW-004
**Cevap:** B

**Açıklama:** `configure terminal` altındaki her komut anında RAM'deki running-config'e işlenir ve hemen etkili olur. RAM uçucudur (DRAM); elektrik kesilince silinir. Kalıcı olması için `copy running-config startup-config` ile NVRAM'e kaydedilmelidir.

**Çeldiriciler:**
- A) NVRAM'e yalnızca kaydetme komutuyla yazılır.
- C) Flash'ta IOS imajı ve dosyalar durur; yapılandırma komutları imajı değiştirmez.
- D) ROM'daki bootstrap ve POST, kullanıcı tarafından değiştirilmez.

**Teori:** → 00-05, Bölüm 3.8 ve 7

---

### FND-HW-005
**Cevap:** Hostname yalnızca RAM'deki running-config'teydi ve kaydedilmediği için kayboldu. VLAN'lar ise oluşturuldukları anda flash'taki `vlan.dat` dosyasına yazıldığı için kaldı.

**Açıklama:** **[CISCO-ÖZEL]** Catalyst switch'lerde iki ayrı kalıcı kayıt vardır: startup-config (2960'ta flash'taki `config.text`) ve VLAN veritabanı (`flash:vlan.dat`). `hostname` bir yapılandırma komutudur; `copy running-config startup-config` yapılmadığı için açılışta yüklenen yapılandırmada yoktur. Varsayılan ayarlarda VLAN oluşturmak ise `vlan.dat` dosyasını hemen günceller; bu dosya flash'ta olduğu için elektrik kesintisinden etkilenmez. VLAN veritabanının ayrıntıları 02-08'de.

**Puan:** Hostname'in neden kaybolduğu 0,5; VLAN'ların neden kaldığı (`vlan.dat`, flash) 0,5.

**Teori:** → 00-05, Bölüm 7

---

### FND-HW-006
**Cevap:** B

**Açıklama:** CRC sıfır olduğu için çerçeveler kabloda bozulmuyor. `rx_missed_errors`, NIC'in yeni gelen çerçeveyi yazacak boş tanımlayıcı bulamadığı durumları sayar: RX halka tamponu doludur, çünkü sürücü ve CPU çerçeveleri işleme hızına yetişemez. Çözüm halka tamponu büyütmek, yükü daha fazla kuyruğa ve çekirdeğe dağıtmak ya da trafiği azaltmaktır.

**Çeldiriciler:**
- A) Kablo arızası CRC hatası üretirdi.
- C) Duplex uyuşmazlığı çarpışma ve CRC hatası (özellikle late collision) üretir (01-10).
- D) IP çakışması L3 sorunudur; NIC'in alma sayaçlarını artırmaz.

**Teori:** → 00-07, Bölüm 3.3, 5 ve 9

---

### FND-HW-007
**Cevap:** a) ≈ **148.810** çerçeve/s. b) **6,72 µs**.

**Açıklama:** Kablodaki bayt süresi = 64 (çerçeve) + 8 (preamble ve SFD) + 12 (IFG) = 84 bayt = 672 bit. a) 10⁸ / 672 ≈ 148.810. b) 672 / 10⁸ s = 6,72 µs.

**Puan:** Her parça 0,5. 20 baytlık ek yük unutulursa (512 bit → ~195.313 çerçeve/s) puan 0.

**Teori:** → 00-07, Bölüm 4

---

### FND-HW-008
**Örnek cevap:** Düşük trafikte **kesme** daha uygundur: Çerçeve gelmedikçe CPU başka işler yapar ve bir çerçeve geldiğinde hemen haber alınır; boşuna yoklama yapılmaz. Yüksek trafikte **yoklama** daha uygundur: Her çerçeve için kesme üretmek CPU'nun zamanını kesmeleri işlemeye harcatır; yoklama ise halkadaki çerçeveleri toplu hâlde işler. NAPI ilk çerçevede kesmeyi kullanır, sonra kesmeleri kapatıp halkayı belirli bir bütçeyle yoklayarak boşaltır; halka boşalınca kesmeleri yeniden açar.

**Puanlama ölçütü (toplam 1):**

| Ölçüt | Puan |
|---|---|
| Düşük trafikte kesmenin avantajı (boşa çevrim yok, hızlı tepki) | 0,25 |
| Yüksek trafikte kesme yükü ve yoklamanın toplu işleme avantajı | 0,25 |
| NAPI'nin sırası: kesme → kesmeleri kapat → bütçeyle yokla → boşalınca kesmeleri aç | 0,5 |

**Teori:** → 00-07, Bölüm 3.4

---

### FND-HW-009
**Cevap:** a) **Haklı değil.** En olası açıklama **checksum offload**'dur. b) Karşı tarafta (ya da arada) yakalama yapmak; offload ayarını kontrol etmek.

**Açıklama:**
a) Checksum offload açıkken ağ yığını checksum alanını doldurmaz; NIC, paketi kabloya göndermeden hemen önce hesaplar. Wireshark paketi yığın ile sürücü arasında, yani checksum hesaplanmadan önce yakaladığı için alan yanlış görünür. Kablodaki paket doğrudur. Gelen paketlerde sorun görülmemesi de bunu destekler: Onların checksum'ı karşı tarafta hesaplanmıştır.
b) Doğrulama yolları (herhangi ikisi):
- Aynı trafiği **karşı bilgisayarda** ya da aradaki bir noktada yakalamak; orada checksum doğru görünür.
- Offload ayarını kontrol etmek: Fedora'da `ethtool -k <arayüz> | grep -i checksum`, Windows'ta `Get-NetAdapterAdvancedProperty`.
- Switch portunda CRC hatası olup olmadığına bakmak; kablo bozuk olsaydı CRC artardı.
- Yakalama süresince offload'u geçici olarak kapatıp tekrar bakmak.

**Puan:** (a) 0,5; (b) iki geçerli yol 0,5 (bir yol 0,25).

**Teori:** → 00-07, Bölüm 3.6 ve 5

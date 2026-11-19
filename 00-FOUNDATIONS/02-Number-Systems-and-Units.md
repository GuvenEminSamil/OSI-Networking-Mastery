# 00-02 Sayı Sistemleri ve Birimler (Number Systems and Units)

> Önkoşullar: 00-01 | Tahmini süre: ~2 saat | CCNA: v1.1 1.6, 1.8, 1.9 (altyapı)

## Öğrenme Hedefleri

- Konumsal sayı sistemini (positional notation) kullanarak onluk, ikili ve onaltılık sayıları yorumlamak.
- 8 bitlik bir değeri bu üç sistem arasında 30 saniyede çevirmek.
- Ağda onaltılığın neden yaygın olduğunu açıklamak.
- Bit, nibble, bayt ve oktet terimlerini doğru kullanmak.
- SI ve IEC öneklerini ayırt etmek; Mbps ile MB/s arasında dönüşüm yapmak.

## 1. Sezgisel Giriş

"2026" yazdığında aslında şunu söylüyorsun: 2 tane bin, 0 tane yüz, 2 tane on, 6 tane bir. Her rakamın değeri **bulunduğu konuma** bağlıdır. Bu fikir, yalnızca 10 tabanına özgü değildir. Taban 2 olursa her konum bir öncekinin iki katı değerindedir; taban 16 olursa on altı katı. Bilgisayarlar ve ağlar bu üç sistemi (10, 2, 16) birlikte kullanır. Bir ağ mühendisi aralarında akıcı biçimde geçiş yapabilmelidir; subnetting, IPv6 ve MAC adresleri bunu gerektirir.

## 2. Neden Var?

- **İkili (binary)**, donanımın doğal dilidir: Her bit iki durumdan birine karşılık gelir (00-01, 00-05).
- **Onluk (decimal)**, insanların doğal dilidir. IPv4 adreslerini `192.168.1.10` biçiminde yazmamız bu yüzdendir.
- **Onaltılık (hexadecimal, hex)**, ikisi arasında bir köprüdür. Bir onaltılık basamak tam olarak 4 bite karşılık gelir; bu sayede uzun bit dizileri kısa ve hatasız yazılabilir. 48 bitlik bir MAC adresi ikili olarak 48 karakter tutarken onaltılık olarak yalnızca 12 karakterdir.

## 3. Mekanizma: Konumsal gösterim

Taban (base, radix) b olan bir sistemde bir sayının değeri, her basamağın kendi konum ağırlığıyla çarpılıp toplanmasıdır:

> değer = dₙ·bⁿ + … + d₂·b² + d₁·b¹ + d₀·b⁰

| Sistem | Taban | Basamaklar | Konum ağırlıkları (sağdan sola) | Yazım örneği |
|---|---|---|---|---|
| Onluk | 10 | 0–9 | 1, 10, 100, 1000 … | 2026 |
| İkili | 2 | 0, 1 | 1, 2, 4, 8, 16 … | `0b1011` ya da 1011₂ |
| Onaltılık | 16 | 0–9, A–F (A=10 … F=15) | 1, 16, 256, 4096 … | `0x7E4` ya da 7E4₁₆ |

Örnek: 1011₂ = 1·8 + 0·4 + 1·2 + 1·1 = **11**.
Örnek: 0x7E4 = 7·256 + 14·16 + 4·1 = 1792 + 224 + 4 = **2020**.

**Not:** `0x` öneki onaltılığı, `0b` öneki ikiliyi belirtir. Bu önekler programlama dillerinden gelir ve ağ belgelerinde de yaygındır. `0x0800` ile `800` aynı sayı değildir: 0x0800 = 8·256 = **2048**.

## 4. Teknik Ayrıntı

### 4.1 Ağ mühendisinin tablosu: 8 bitlik ağırlıklar

Bir baytın (8 bit) konum ağırlıklarını ezbere bilmek, subnetting'in yarısıdır:

| Bit konumu | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|---|
| Ağırlık | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

En soldaki bite **en anlamlı bit (MSB, Most Significant Bit)**, en sağdakine **en az anlamlı bit (LSB, Least Significant Bit)** denir. Sekiz bitin hepsi 1 olduğunda değer 128 + 64 + … + 1 = **255** olur. Bir IPv4 adresinin her bölümünün 0–255 aralığında olmasının nedeni budur: Her bölüm bir bayttır.

### 4.2 İkiliden onluğa

1'lerin bulunduğu konumların ağırlıklarını topla.

```
  1  1  0  0  0  0  0  0      ikili: 11000000
128 64 32 16  8  4  2  1
128+64                    = 192
```

### 4.3 Onluktan ikiliye: çıkarma yöntemi

Ağ dünyasında en hızlı yöntem budur. Soldan başla; ağırlık kalan değere sığıyorsa o konuma 1 yaz ve ağırlığı çıkar, sığmıyorsa 0 yaz.

Örnek: **200**

| Ağırlık | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|---|---|---|---|---|---|---|---|---|
| Kalan | 200 → 72 | 72 → 8 | 8 | 8 | 8 → 0 | 0 | 0 | 0 |
| Bit | 1 | 1 | 0 | 0 | 1 | 0 | 0 | 0 |

Sonuç: 200 = **11001000**₂. Kontrol: 128 + 64 + 8 = 200 ✓

Alternatif olarak **ikiye bölme yöntemi** de kullanılabilir: Sayıyı tekrar tekrar 2'ye böl, kalanları alttan üste oku. Uzun sayılarda işe yarar ama baytlar için çıkarma yöntemi daha hızlıdır.

### 4.4 İkili ve onaltılık arasında: nibble yöntemi

Dört bitlik gruba **nibble** denir. Bir nibble 0–15 arası değer alır; bu da tam olarak bir onaltılık basamaktır. Bu yüzden dönüşüm için hesap yapmana gerek yoktur; yalnızca 4 bitlik grupları eşlersin:

| Onaltılık | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| İkili | 0000 | 0001 | 0010 | 0011 | 0100 | 0101 | 0110 | 0111 | 1000 | 1001 | 1010 | 1011 | 1100 | 1101 | 1110 | 1111 |

Örnek: `11001000` → `1100 1000` → `C 8` → **0xC8** (= 200).
Örnek: `0x2F` → `0010 1111` → **00101111**₂ (= 47).

Onaltılıktan onluğa geçmek için ya doğrudan konum ağırlıklarını (16'nın kuvvetleri) kullan ya da önce ikiliye, sonra onluğa çevir.

### 4.5 2'nin kuvvetleri

Bu değerler ağ mühendisliğinde sürekli karşına çıkar. İlk satırı ezberle; ikinciyi tanı.

| n | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2ⁿ | 1 | 2 | 4 | 8 | 16 | 32 | 64 | 128 | 256 | 512 | 1024 | 2048 | 4096 | 8192 | 16384 | 32768 | 65536 |

| n | 2ⁿ | Nerede karşına çıkacak |
|---|---|---|
| 16 | 65.536 | Port numarası sayısı (0–65535), 04-01 |
| 24 | 16.777.216 | Bir /8 ağındaki adres sayısı; MAC adresinde OUI'den sonraki adres alanı |
| 32 | 4.294.967.296 | Tüm IPv4 adres alanı |
| 48 | ≈ 2,8 × 10¹⁴ | Tüm MAC adres alanı |
| 128 | ≈ 3,4 × 10³⁸ | Tüm IPv6 adres alanı |

### 4.6 Maskelerde kullanılan sekiz değer

Bir alt ağ maskesinin baytları soldan doldurulan 1'lerden oluşur. Bu yüzden bir maske baytı yalnızca dokuz değerden biri olabilir. 0'ı ve sekiz değeri ezberle; Faz 4'te hayatını kolaylaştıracak:

| İkili | 10000000 | 11000000 | 11100000 | 11110000 | 11111000 | 11111100 | 11111110 | 11111111 |
|---|---|---|---|---|---|---|---|---|
| Onluk | 128 | 192 | 224 | 240 | 248 | 252 | 254 | 255 |

Her adımda bir önceki değere bir sonraki ağırlık eklenir: 128 + 64 = 192, 192 + 32 = 224, …

### 4.7 Bit, nibble, bayt, oktet

| Terim | Boyut | Not |
|---|---|---|
| bit | 1 bit | Bilginin temel birimi (00-01). Kısaltması küçük **b** |
| nibble | 4 bit | Bir onaltılık basamak |
| bayt (byte) | 8 bit | Kısaltması büyük **B** |
| oktet (octet) | tam olarak 8 bit | RFC'ler ve ağ standartları "byte" yerine bunu kullanır |

Neden "oktet"? Bilgisayar tarihinin ilk dönemlerinde bayt her zaman 8 bit değildi; bazı makinelerde 6 ya da 9 bitlik baytlar vardı. İnternet standartları belirsizliği önlemek için "tam 8 bit" anlamına gelen oktet terimini seçti. Bugün pratikte ikisi aynı anlama gelir.

### 4.8 Birimler: SI ve IEC önekleri

İki ayrı önek sistemi vardır ve karıştırılmaları yaygın hatalara yol açar:

| SI (ondalık) | Değer | IEC (ikili) | Değer |
|---|---|---|---|
| k (kilo) | 10³ = 1.000 | Ki (kibi) | 2¹⁰ = 1.024 |
| M (mega) | 10⁶ | Mi (mebi) | 2²⁰ = 1.048.576 |
| G (giga) | 10⁹ | Gi (gibi) | 2³⁰ = 1.073.741.824 |
| T (tera) | 10¹² | Ti (tebi) | 2⁴⁰ |

IEC önekleri, IEC 80000-13 standardında tanımlıdır [STD-IEC80000].

Ağda kural basittir: **Bağlantı hızları her zaman ondalık SI birimleri ve bit cinsindendir.** 1 Gbps = 10⁹ bit/saniye. "Gigabit Ethernet" tam olarak saniyede bir milyar bit demektir.

Bellek boyutları ise genellikle ikili önekleri kullanır. Depolama üreticileri ondalık birim kullanırken bazı işletim sistemleri ikili hesaplayıp "GB" etiketiyle gösterir. Bu yüzden 1 TB'lık bir disk Windows'ta yaklaşık "931 GB" görünür: 10¹² / 2³⁰ ≈ 931.

### 4.9 Mbps ile MB/s

1 bayt = 8 bit olduğundan:

> MB/s = Mbps ÷ 8

| Bağlantı | Ham kapasite (bayt) |
|---|---|
| 100 Mbps | 12,5 MB/s |
| 1 Gbps | 125 MB/s |
| 10 Gbps | 1,25 GB/s |

Gerçek dosya aktarım hızı bundan daha düşüktür, çünkü her çerçeve ve paket başlık taşır (protokol ek yükü, 08-01), TCP'nin kendi davranışları vardır (04-05) ve yol üzerindeki en yavaş bağlantı hızı belirler.

> **[DERİN]** Bitlerin kabloya hangi sırayla gönderildiği de bir anlaşmadır. IEEE 802.3 Ethernet, her okteti **en az anlamlı biti önce** olacak şekilde gönderir [IEEE-8023]. Bir MAC adresinin multicast olup olmadığını belirten bit, ilk oktetin en az anlamlı bitidir; dolayısıyla kabloya çıkan ilk adres bitidir. Bu tasarım, alıcının adresin multicast olduğunu ilk bitte anlamasını sağlar (02-02).

## 5. Gerçek Dünya Örnekleri

- **MAC adresleri** 48 bittir ve onaltılık yazılır. Aynı adres farklı araçlarda farklı biçimlerde görünür:

  | Araç | Biçim |
  |---|---|
  | Windows (`ipconfig /all`) | `00-1A-2B-3C-4D-5E` |
  | Linux (`ip link`) | `00:1a:2b:3c:4d:5e` |
  | Cisco IOS | `001a.2b3c.4d5e` |

- **EtherType:** Ethernet çerçevesindeki `0x0800` değeri yükün IPv4, `0x86DD` değeri IPv6, `0x0806` değeri ARP olduğunu söyler (02-03).
- **IPv6 adresleri** 128 bittir ve 16 bitlik 8 grup halinde onaltılık yazılır: `2001:0db8:0000:0000:0000:0000:0000:0001`. Kısaltma kuralları 03-16'da.
- **İnternet paketin:** Evindeki "100 Mbps" bağlantıda bir oyunun 50 GB'lık güncellemesi en iyi durumda 50 × 8 / 100 = 4000 saniye, yani yaklaşık 67 dakika sürer. Bu hesabı yaparken baytı bite çevirmeyi unutmak, sonucu sekiz kat yanlış bulmak demektir.

## 6. Diğer Konularla Bağlantı

| Bu dosyadaki fikir | Nerede kullanılıyor |
|---|---|
| 8 bitlik ağırlıklar ve maske değerleri | 03-03, 03-04, 03-05 |
| Onaltılık ve nibble | 02-02 (MAC), 02-03 (EtherType), 03-16 (IPv6) |
| 2'nin kuvvetleri | 03-04 (host sayısı), 04-01 (port aralığı) |
| Bit/bayt ve SI birimleri | 01-09 (Ethernet hızları), 04-05 (pencere ve BDP) |
| Bit gönderim sırası | 02-02 |

## 7. Cisco ve Pratik

Cisco cihazlarında bu sistemlerin hepsiyle karşılaşırsın:

```
Router# show interfaces GigabitEthernet0/0
GigabitEthernet0/0 is up, line protocol is up
  Hardware is ..., address is 001a.2b3c.4d5e (bia 001a.2b3c.4d5e)
  ...
  MTU 1500 bytes, BW 1000000 Kbit/sec, DLY 10 usec,
```

(Çıktının biçimi gerçek, değerler örnektir.) Burada MAC adresi onaltılık, MTU bayt, bant genişliği (BW) kilobit/saniye cinsindendir: 1.000.000 Kbit/sec = 1 Gbps.

Programlama tarafında, Python bu dönüşümleri doğrudan yapar. Kendi cevaplarını kontrol etmek için kullanabilirsin:

```python
bin(200)           # '0b11001000'
hex(200)           # '0xc8'
int('11001000', 2) # 200
int('0x0800', 16)  # 2048
format(10, '08b')  # '00001010'  (8 haneye tamamlanmış ikili)
```

## 8. Yaygın Yanılgılar

| Yanılgı | Doğrusu |
|---|---|
| "1 Gbps bağlantıyla 1 GB'lık dosya 1 saniyede iner." | 1 GB = 8 gigabit. En iyi durumda 8 saniye, protokol ek yüküyle daha uzun. |
| "0x0800 sekiz yüz demektir." | Onaltılık 0800 = 8·256 = 2048. |
| "Onaltılık başka türde bir sayıdır." | Sayı aynıdır; yalnızca yazılış biçimi farklıdır. 200, 11001000₂ ve 0xC8 aynı değerdir. |
| "1 KB her zaman 1024 bayttır." | SI'da 1 kB = 1000 bayt, IEC'de 1 KiB = 1024 bayt. Ağ hızlarında her zaman ondalık birimler kullanılır. |
| "Bayt ile oktet farklı boyutlardır." | Bugün ikisi de 8 bittir. Standartların "oktet" demesinin nedeni tarihsel belirsizliği önlemektir. |

## 9. Arıza Giderme Yaklaşımı

Sayı sistemi hataları gerçek arızalara yol açar. Sık görülen iki örnek:

- Bir maske baytını yanlış çevirmek (örneğin /26'yı 255.255.255.224 sanmak). Doğrusu 255.255.255.192'dir. Sonuç: Host, yerel ağındaki bir cihazı uzak sanar ya da tersini yapar (03-06).
- Hız ve boyut birimlerini karıştırmak. "Hat 100 Mbps ama dosya 12 MB/s geliyor, hat bozuk" şikâyeti çoğu zaman birim hatasıdır; 12 MB/s, 100 Mbps'nin yaklaşık %96'sıdır.

Bir değerden şüphelendiğinde onu ikiliye çevir ve bit bit kontrol et.

## 10. CCNA Bağlantısı

CCNA sınavında hesap makinesi kullanamazsın. v1.1'in 1.6 (IPv4 subnetting), 1.8 ve 1.9 (IPv6 adresleme ve EUI-64) konuları hızlı ve hatasız sayı dönüşümü gerektirir. Bu dosyadaki tabloları ezbere bilmek, sınavda zamandan önemli ölçüde tasarruf sağlar.

## 11. Kendini Kontrol Et

1. 172'yi ikiliye ve onaltılığa çevir.
   <details><summary>Cevap</summary>
   172 = 128 + 32 + 8 + 4 → <code>10101100</code>₂ → <code>1010 1100</code> → <b>0xAC</b>.
   </details>

2. `11100000`₂ kaçtır? Bu değeri hangi bağlamda çok göreceksin?
   <details><summary>Cevap</summary>
   128 + 64 + 32 = <b>224</b>. Bir maske baytı olarak (/27 maskesinin son baytı: 255.255.255.224). Ayrıca 224.0.0.0, IPv4 multicast aralığının başlangıcıdır.
   </details>

3. `0x86DD` onluk tabanda kaçtır?
   <details><summary>Cevap</summary>
   8·4096 + 6·256 + 13·16 + 13 = 32768 + 1536 + 208 + 13 = <b>34525</b>. (Ethernet'te IPv6'nın EtherType değeridir.)
   </details>

4. Bir MAC adresi 48 bittir. Onaltılık yazıldığında kaç karakter tutar? Neden?
   <details><summary>Cevap</summary>
   12 karakter. Her onaltılık basamak 4 bit taşır: 48 / 4 = 12.
   </details>

5. 300 Mbps'lik bir bağlantıda 9 GB'lık bir dosya en iyi durumda kaç saniyede iner?
   <details><summary>Cevap</summary>
   9 GB × 8 = 72 gigabit = 72.000 megabit. 72.000 / 300 = <b>240 saniye</b> (4 dakika). Gerçekte protokol ek yükü yüzünden biraz daha uzun sürer.
   </details>

6. Bir host bölümünde 6 bit varsa kaç farklı adres ifade edilebilir?
   <details><summary>Cevap</summary>
   2⁶ = <b>64</b>. (Kaçının host'lara atanabileceği 03-04'te.)
   </details>

## 12. Uygulama

Bu dosyanın PT pratiği yoktur. Kendi hızını ölç: Kâğıda rastgele 10 sayı yaz (0–255) ve her birini ikiliye ve onaltılığa çevir. Süreyi tut; hedef her biri için 30 saniye. Cevaplarını Python ile kontrol et (Bölüm 7). Hedefe ulaşana kadar her gün 5 dakika tekrar et.

## 13. Ustalık Kontrol Listesi

- [ ] 0–255 arasındaki her değeri ikili, onluk ve onaltılık arasında 30 saniyede çevirebiliyorum (10 denemede 10 doğru).
- [ ] 8 bitlik ağırlık tablosunu ve maskelerde kullanılan sekiz değeri ezbere yazabiliyorum.
- [ ] 2⁰'dan 2¹⁶'ya kadar kuvvetleri ezbere biliyorum.
- [ ] Onaltılığın ağda neden kullanıldığını nibble kavramıyla açıklayabiliyorum.
- [ ] Mbps ile MB/s arasında ve SI ile IEC önekleri arasında hatasız dönüşüm yapabiliyorum.

## Kaynaklar

- [STD-IEC80000] IEC 80000-13: ikili önekler (kibi, mebi, gibi).
- [IEEE-8023] IEEE 802.3: oktetlerin en az anlamlı bit önce gönderilmesi; EtherType değerleri için ayrıca [IEEE-RA].
- [TXT-PETZOLD] Code, 2. baskı: ikili ve onaltılık sistemlere sezgisel giriş (ek okuma).

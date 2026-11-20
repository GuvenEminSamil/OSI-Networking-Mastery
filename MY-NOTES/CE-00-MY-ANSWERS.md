# CE-00 Cevaplarım

> Soruları `10-QUESTION-BANK/COMPREHENSIVE-EXAMS/CE-00.md` dosyasından oku, cevaplarını buraya yaz. Emin olmadıklarının yanına `?` koy. Puanlamayı cevap dosyasıyla yap.

**Başlangıç saati:** ··· **Bitiş saati:** ···

## Bölüm A (1'er puan)

1. 7
2. fiziksel, uygulama
3. 4. katman
4. 3. katman
5. 2. katman
6. 3. katman
7. 2. katman
8. paket
9. 2. katman
10. birisi verinin yola çıkması için paketlenmesi diğeri ise paketin çöümlenmesi

## Bölüm B (2'şer puan)

11. 1. katmanı kontrol ederim. Belki kabloda bir problem vardır.
12. Switchte problem olabilir. 1. ve 2. katmanları kontol ederim.
13. 3. katmanı kontrol ederim. Belki DNS sunucusu ile bir kopukluk vardır.
14. LAN'ın dışına veri göndereceğimiz için öncelikle router'a gitmelidir.
15. LAN'daki bütün cihazlara flood yapar.
16. Source IP ve MAC ve Destination IP ve MAC
17. ?
18. ?
19. şifreleme-güvenlik amacıyla
20. ARP?

## Bölüm C (2'şer puan)

21. Mutlak olarak hangi iki cihazın haberleştiği karışmasın diye.
22. Hız sebebiyle.
23. Çerçevelerde TTL yoktur ya da TTL değeri yüksektir. TTL protokolü
24. 192.168.1.0/24 seçilir çünkü hedef IP ile aynı ağdadır.
25. İlk senaryoda diğer bilgisayarla aynı ağdadır ve L2 Switch o ağdaki MAC adreslerini bilir. İkinci senaryoda ise WAN'ı kullanacaktır ve bunun için Default Gateway olan Router'ın MAC adresine ihtiyaç duyar.

## Puanlama

> Puanlama Claude tarafından, `answers/CE-00-ANSWERS.md`'deki ölçütlerle yapıldı (2026-11-20).

| Bölüm | Puan |
|---|---|
| A (10 üzerinden) | 10 |
| B (20 üzerinden) | 6 |
| C (10 üzerinden) | 5 |
| **Toplam (40 üzerinden)** | **21** |

Yorum: Katman–kavram eşleştirmeleri sağlam (Bölüm A tam). Eksik olan, mekanizmalar ve ayrıntılar. Müfredat tam olarak bunu kuracak.

## Yanlış ya da eksik olanlar

**Kalın** satırlar, emin olarak verilmiş ama yanlış olan cevaplardır (yanılgı). Bu dosyalara geldiğinde o bölümleri özellikle dikkatle oku.

| Soru | Puan | Derinleştiği yer | Not |
|---|---|---|---|
| 10 | 1/1 | 08-01 | Yön doğru; eksik olan, her katmanın kendi başlığını ekleyip çıkarması |
| 11 | 1/2 | 01-10, 11-01 | L1 doğru; gerekçe (link ışığı = iki PHY birbirini algılıyor) ve ikinci bir kontrol eksik |
| 12 | 0/2 | 03-06, 11-03, 02-15 | İnternet çalıştığına göre senin L1–L2'n büyük olasılıkla sağlam. Sorun hedef tarafta: güvenlik duvarı ICMP'yi engelliyor olabilir, hedefin IP ayarı yanlış olabilir, iki cihaz farklı VLAN'larda olabilir |
| **13** | 1/2 | 07-02, 08-10 | DNS tahmini doğru, ama **DNS L7'dir**. 8.8.8.8'e ping gittiğine göre L3 zaten çalışıyor |
| 14 | 2/2 | 03-06 | Doğru. Cevabı açıkça "router'ın, yani varsayılan ağ geçidinin MAC adresi" diye yazmaya alış |
| 15 | 1/2 | 02-06 | Flooding doğru; ama "LAN'daki bütün cihazlara" değil, **geldiği port hariç, aynı VLAN'daki** portlara |
| **16** | 1/2 | 03-07 | MAC adreslerinin değiştiği doğru, ama **IP adresleri değişmez** (NAT yoksa). Değişen TTL ve IPv4 checksum'ıdır |
| 17 | 0/2 | 04-03 | SYN, SYN-ACK, ACK |
| 18 | 0/2 | 07-03 | Discover, Offer, Request, Acknowledge (DORA) |
| 19 | 0/2 | 06-05, 06-06 | Üç amaç: gizlilik (şifreleme), bütünlük, sunucunun kimlik doğrulaması |
| **20** | 0/2 | 03-10 | **ARP değil**, L3 yönlendirme gerekir: router-on-a-stick ya da L3 switch'te SVI |
| 21 | 1/2 | 03-07, 08-04 | IP'nin uçtan uca rolü doğru; eksik olan, MAC adresinin yalnızca tek bir bağlantıda anlamlı olması |
| 22 | 1/2 | 04-06 | "Hız" yerine: bayat verinin yeniden gönderilmesi anlamsız; TCP'de kaybolan bir segment arkasındakileri bekletir |
| **23** | 1/2 | 02-11, 02-12 | "Çerçevede TTL yok" gözlemi çok iyi. Ama **"TTL protokolü" diye bir protokol yok**; döngüyü önleyen STP'dir |
| 24 | 1/2 | 03-08 | Rota doğru, gerekçe eksik: İki rota da hedefi kapsar; seçilen, en uzun önek eşleşmesidir |
| **25** | 1/2 | 00-03, 03-06 | Sonuç doğru, ama **MAC adresini switch değil, host ARP ile öğrenir**. Yerel/uzak kararını host, maskeyle AND yaparak verir |

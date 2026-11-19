# Buradan Başla (Start Here)

> Bu dosya tek bir soruyu cevaplar: **"Bugün ne yapmalıyım?"** Diğer dosyaların ne işe yaradığını öğrenmek için önce bunu oku. Planın tamamını şimdi anlaman gerekmiyor; her gün yalnızca o günün adımlarını izle.

## Yalnızca dört dosya önemli

| Ne zaman | Dosya | Ne için |
|---|---|---|
| Her sabah | **STUDY-ROADMAP.md**, Bölüm 3 ve 4 | Bugün hangi fazdasın, sıradaki dosya hangisi |
| Çalışırken | **Ders dosyası** (ör. `00-FOUNDATIONS/01-Information-and-Data.md`) | Konuyu öğrenmek |
| Çalışırken | **MY-NOTES/** klasörü | Senin cevapların, teach-back'lerin, soruların |
| Gün sonunda | **MY-NOTES/LOG.md** | Bugün ne yaptın, ne zorladı |

Geri kalanlar (README, CURRICULUM, SOURCES, PROGRESS) başvuru dosyalarıdır. Günlük çalışmada açman gerekmez; PROGRESS.md'yi senin günlüğüne bakarak ben güncellerim.

**Okuma ve yazma:** Ders dosyalarını GitHub'da tarayıcıdan oku; diyagramlar ve katlanmış cevaplar orada doğru görünür. Kendi notlarını bilgisayarındaki kopyada, `MY-NOTES/` içinde VS Code ile yaz ve gün sonunda gönder (`push`).

## Her ders dosyası için aynı 6 adım

| # | Adım | Süre | Nereye yazılır |
|---|---|---|---|
| 1 | Dosyayı baştan sona oku. Katlanmış cevapları **açma**. | 40–60 dk | — |
| 2 | "Kendini Kontrol Et" sorularını önce kendin cevapla, sonra katlanmış cevapla karşılaştır. | 10 dk | Defter ya da kafandan |
| 3 | **Teach-back:** Dosyayı kapat ve konuyu sıfırdan öğrenen birine anlatıyormuş gibi yaz ya da sesli anlat. Takıldığın yer, yeniden okuman gereken yerdir. | 10 dk | `MY-NOTES/TEACH-BACK.md` |
| 4 | **Kartlar:** `12-REVISION/anki/` içindeki o dosyanın kartlarını Anki'ye aktar ve en az 2 kart da kendin yaz. | 10 dk | Anki |
| 5 | Dosyadaki "Uygulama" alıştırmasını yap. | 10–30 dk | `MY-NOTES/` |
| 6 | "Ustalık Kontrol Listesi"ni gözden geçir. Tik atamadığın madde varsa günlüğe yaz. | 5 dk | `MY-NOTES/LOG.md` |

Anlamadığın bir nokta olursa `MY-NOTES/QUESTIONS.md` dosyasına yaz ve devam et. Bir sonraki oturumda bana getir.

## 1. gün: 20 Kasım, Cuma (~4,75 saat)

### Oturum 1 — Tanışma ve tanı testi (~1,5 saat)

1. **Bu dosya** (10 dk).
2. **`12-REVISION/01-Spaced-Repetition-Guide.md`** (25 dk). Kart sistemini ve tekrar takvimini anla.
3. **`10-QUESTION-BANK/COMPREHENSIVE-EXAMS/CE-00.md`** (40 dk). Zamanlayıcıyı kur. Notlara ya da cevap dosyasına bakmadan çöz. Cevaplarını `MY-NOTES/CE-00-MY-ANSWERS.md` dosyasına yaz. Emin olmadıklarının yanına `?` koy.
4. **`10-QUESTION-BANK/COMPREHENSIVE-EXAMS/answers/CE-00-ANSWERS.md`** (15 dk). Puanla. Yanlış ya da `?` işaretli her soru için cevap dosyasındaki "Derinleştiği yer"i not et.

15 dakika mola.

### Oturum 2 — Kurulum (~1,5 saat)

1. **Anki** (15 dk): Bilgisayarına Anki'yi kur ve `CCNA` adında bir deste (deck) oluştur.
2. **Packet Tracer kontrolü** (20 dk): Faz 0 kapısının ilk yarısı.
   1. PT 9.0'ı aç. Cihaz paletinden iki **PC** ve bir **2960** switch'i çalışma alanına sürükle.
   2. Bağlantılardan **Copper Straight-Through** kabloyu seç; PC0'ı switch'in Fa0/1 portuna, PC1'i Fa0/2 portuna bağla. Bağlantı ışıkları önce turuncu yanar; yaklaşık 30 saniye sonra yeşile döner. Nedenini 02-11'de öğreneceksin.
   3. PC0 → Desktop → IP Configuration → Static: `192.168.1.1`, maske `255.255.255.0`. PC1 için aynı adımlarla `192.168.1.2`.
   4. PC0 → Desktop → Command Prompt → `ping 192.168.1.2`. "Reply from 192.168.1.2" görmelisin.
3. **Wireshark, Windows** (20 dk): Wireshark'ı kur; kurulumda Npcap'i de kabul et. Açılışta trafik grafiği hareket eden arayüzü (Wi-Fi ya da Ethernet) seç, yakalamayı başlat, bir web sitesi aç, yakalamayı durdur. Faz 0 kapısının ikinci yarısı budur. Paketlerin anlamını şimdilik bilmen gerekmiyor.
4. **Wireshark, Fedora** (20 dk; bugün Fedora'da değilsen hafta içinde yap):
   ```bash
   sudo dnf install wireshark
   sudo usermod -aG wireshark $USER   # yakalama izni; ardından oturumu kapatıp yeniden aç
   ```
5. **Git ve VS Code** (15 dk): Depoyu klonla ve VS Code'da aç.
   ```bash
   git clone https://github.com/GuvenEminSamil/OSI-Networking-Mastery.git
   ```

15 dakika mola.

### Oturum 3 — İlk ders: 00-01 (~1,5 saat)

**`00-FOUNDATIONS/01-Information-and-Data.md`** dosyasında yukarıdaki 6 adımı uygula. 4. adımda Anki'ye `12-REVISION/anki/00-01.txt` dosyasını aktar: File → Import, deste olarak `CCNA` seçilir.

### Gün sonu (~10 dk)

1. `MY-NOTES/LOG.md` dosyasına bugünün kaydını yaz: CE-00 puanın, bitirdiğin dosyalar, zorlandığın yerler.
2. Notlarını gönder:
   ```bash
   git add MY-NOTES
   git commit -m "20 Kasım günlüğü"
   git push
   ```

## Sonraki günler

Her sabah:

1. **STUDY-ROADMAP.md**, Bölüm 3'teki tabloda bugünün tarihine denk gelen fazı bul.
2. Aynı dosyanın Bölüm 4'ünde o fazın **Sıra** satırına bak ve sıradaki ilk bitmemiş öğeyi aç.
3. Günü üç oturuma böl: iki oturum ders dosyası (6 adım), bir oturum pratik (`LAB-`, `H-`) ya da soru bankası. Her gün 15 dakika Anki.
4. Bir fazın son öğesini bitirdiğinde aynı fazın **Ustalık kapısı** maddelerini dene ve sonucu günlüğe yaz.

**Pazar:** Yeni konu yok. Yaklaşık 2 saat tekrar yap (12-01, Bölüm 4.3).

**Bu hafta:**

| Gün | Plan |
|---|---|
| 20 Kas, Cuma | Yukarıdaki 1. gün |
| 21 Kas, Cumartesi | 00-02, ardından 00-03 |
| 22 Kas, Pazar | Tekrar (~2 saat) |
| 23 Kas, Pazartesi | 00-04, ardından 00-05 |
| 24 Kas, Salı | 00-06, ardından 00-07 |
| 25 Kas, Çarşamba | 00-08, 00-09, FND soruları ve Faz 1 kapısı |

00-05 – 00-09 henüz yazılmadı. En geç **22 Kasım pazar** günü yeni bir oturum aç ve "devam" yaz; o zaman hazırlanacak.

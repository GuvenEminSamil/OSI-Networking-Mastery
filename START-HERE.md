# Buradan Başla (Start Here)

> Bu dosya tek bir soruyu cevaplar: **"Bugün ne yapmalıyım?"** Planın tamamını anlaman gerekmiyor; her gün yalnızca aşağıdaki rutini izle.

## Her sabah

1. **STUDY-ROADMAP.md**, Bölüm 3: Tabloda bugünün tarihine denk gelen fazı bul.
2. Aynı dosyanın Bölüm 4'ünde o fazın **Sıra** satırına bak ve sıradaki ilk bitmemiş öğeyi aç.

Geri kalan dosyalar (README, CURRICULUM, SOURCES, PROGRESS) başvuru dosyalarıdır. Günlük çalışmada açman gerekmez; PROGRESS.md'yi ben güncellerim.

## Her ders dosyası için 5 adım

| # | Adım | Süre |
|---|---|---|
| 1 | Dosyayı baştan sona oku. Katlanmış cevapları **açma**. | 40–60 dk |
| 2 | "Kendini Kontrol Et" sorularını önce kendin cevapla, sonra katlanmış cevapla karşılaştır. | 10–15 dk |
| 3 | `12-REVISION/anki/` içindeki o dosyanın kartlarını Anki'ye aktar (File → Import, deste: `CCNA`). İstersen kendi kartlarını da ekle. | 5–10 dk |
| 4 | Dosyadaki "Uygulama" alıştırmasını yap. | 10–30 dk |
| 5 | Dosyanın sonundaki "Ustalık Kontrol Listesi"nde yapabildiklerine `[X]` koy. | 5 dk |

## Günün yapısı (pazartesi–cumartesi, ~4,75 saat)

| Oturum | İçerik |
|---|---|
| 1 (1,5 saat) | Ders dosyası, 1. ve 2. adım |
| 2 (1,5 saat) | Ders dosyasının devamı ya da ikinci ders dosyası |
| 3 (1,5 saat) | Pratik (`LAB-` yönergesi, tam lab ya da `H-` host labı) veya soru bankası |
| Her gün | 15 dk Anki |

**Pazar:** Yeni konu yok. Yaklaşık 2 saat tekrar yap (12-01, Bölüm 4.2).

## Senin yazacağın yerler

| Dosya | Ne zaman |
|---|---|
| Ders dosyasındaki ustalık listesi | Her dosyanın sonunda `[X]` işaretle |
| `MY-NOTES/RESULTS.md` | Bir test (CE-, soru bankası) ya da faz kapısı bitince tek satır |
| `MY-NOTES/QUESTIONS.md` | İsteğe bağlı: anlamadığın bir şey olursa yaz, devam et |

Gün sonunda değişiklikleri gönder: `git add -A`, `git commit -m "..."`, `git push`.

## Bu hafta

| Gün | Plan |
|---|---|
| 21 Kas, Cumartesi | 00-02, ardından 00-03 |
| 22 Kas, Pazar | Tekrar (~2 saat) |
| 23 Kas, Pazartesi | 00-04, ardından 00-05 |
| 24 Kas, Salı | 00-06, ardından 00-07 |
| 25 Kas, Çarşamba | 00-08, 00-09, FND soruları ve Faz 1 kapısı |

Kurulumda eksik kaldıysa: Fedora'da Wireshark (`sudo dnf install wireshark`, ardından `sudo usermod -aG wireshark $USER` ve oturumu kapatıp aç). İlk kullanım Faz 3'te.

## Yeni bir sohbet açtığında

Her yeni sohbet boş başlar; önceki sohbeti hatırlamaz. Bu yüzden ilk mesaj olarak şunu yapıştır:

```
OSI-Networking-Mastery projesine devam. GuvenEminSamil/OSI-Networking-Mastery deposunu
bağla, README.md'deki "Yeni oturumda çalışmaya devam etme protokolü"nü uygula ve
PROGRESS.md'deki sıradaki paketi yaz.
```

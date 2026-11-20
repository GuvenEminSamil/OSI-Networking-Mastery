# Soru Bankası (Question Bank)

> Pratik testler burada. Teori dosyalarındaki "Kendini Kontrol Et" soruları ısınmadır; bu klasördeki sorular ise faz kapılarında sayılan testlerdir. Tasarım: CURRICULUM.md, Bölüm 6.

## Düzen

| Klasör | Alan kodu | Kapsam |
|---|---|---|
| `FOUNDATIONS/` | FND | 00-01 – 00-09 |
| `PHYSICAL/` | PHY | 01-* |
| `DATA-LINK/` | DL | 02-* |
| `NETWORK/` | NET | 03-* |
| `TRANSPORT/` | TRN | 04-* |
| `SESSION/`, `PRESENTATION/`, `APPLICATION/` | SES, PRS, APP | 05-*, 06-*, 07-* |
| `SECURITY/`, `OPERATIONS/` | SEC, OPS | 14-*, 15-* |
| `COMPREHENSIVE-EXAMS/` | CE | CE-00 – CE-06 |

Her konu dosyasının (`Q-<ALAN>-<KONU>.md`) ayrı bir cevap dosyası vardır: `answers/A-<ALAN>-<KONU>.md`. Soru kimlikleri `<ALAN>-<KONU>-NNN` biçimindedir (ör. `FND-OSI-004`).

## Soru kategorileri

| Kod | Kategori | Ne ölçer |
|---|---|---|
| B | Temel anlama | Kavramın doğru tanımı ve rolü |
| O | Orta düzey teknik | Hesaplar, alan değerleri, davranışlar, çıktılar |
| İ | İleri muhakeme | Neden-sonuç; "şu değişirse ne olur" |
| S | Gerçek dünya senaryosu | Bilgiyi verilen ağa uygulama |
| A | Arıza giderme | Belirtiden nedene ulaşma |
| MC | CCNA tarzı çoktan seçmeli | Tek ya da çok cevaplı ("İki tane seçin") |
| K | Kendi cümlelerinle | Açık uçlu; cevap anahtarında puanlama ölçütü |
| KK | Karşılaştır | İki seçenekten hangisinin, ne zaman ve neden seçildiği |

Zorluk: 1 (temel) – 3 (zor).

## Nasıl çözülür?

1. Bir dosyayı **tek oturumda**, teori dosyalarına ve cevap anahtarına bakmadan çöz. Hesap makinesi kullanma; sınavda yok.
2. Cevaplarını kâğıda ya da ayrı bir dosyaya yaz. Emin olmadıklarının yanına `?` koy.
3. Bitince cevap dosyasıyla puanla. Yanlış ve `?` işaretli her soru için cevaptaki teori bağlantısını aç ve o bölümü yeniden oku.

## Puanlama

- Her soru **1 puandır**.
- Çok cevaplı MC sorularında puan için seçeneklerin **hepsi** doğru olmalıdır (sınavdaki gibi kısmi puan yok).
- Birden fazla parçası olan O, İ, S ve A sorularında her parça eşit ağırlıktadır (ör. iki parçalı soruda her parça 0,5).
- K ve KK sorularında cevap anahtarındaki ölçütler (rubric) kullanılır; puan 0,25'lik adımlarla verilir.

**Faz kapısı:** Bir alanın sorularında toplam **≥ %85** (ör. 40 FND sorusunda en az 34 puan). Sonucu `MY-NOTES/RESULTS.md`'ye tek satır olarak yaz:

```
| 2026-11-25 | FND (40 soru) | 35/40 | Yanlışlar: FND-DAT-006, FND-OSI-005 |
```

## Mevcut dosyalar

| Dosya | Soru | Kapsam |
|---|---|---|
| `FOUNDATIONS/Q-FND-DAT.md` | 12 | Bilgi, sayı sistemleri, Boole mantığı, veri temsili (00-01, 00-02, 00-03, 00-06) |
| `FOUNDATIONS/Q-FND-HW.md` | 9 | Elektrik, transistörler, bilgisayar mimarisi (00-04, 00-05, 00-07) |
| `FOUNDATIONS/Q-FND-NET.md` | 9 | Ağ temelleri (00-08) |
| `FOUNDATIONS/Q-FND-OSI.md` | 10 | Katmanlı modeller (00-09) |
| `COMPREHENSIVE-EXAMS/CE-00.md` | 25 | Tanı testi (ustalık seviyesine sayılmaz) |

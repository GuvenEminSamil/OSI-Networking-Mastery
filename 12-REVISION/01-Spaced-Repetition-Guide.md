# 12-01 Aralıklı Tekrar Rehberi (Spaced Repetition Guide)

> Önkoşullar: — | Tahmini süre: ~30 dk | CCNA: —

## Öğrenme Hedefleri

- Bu projede neden okumak yerine **hatırlamaya** dayalı çalışıldığını açıklamak.
- Tekrar kartlarını doğru yazmak ve 1-3-7-14-30 günlük takvimi uygulamak.
- Günlük ve pazar tekrar rutinlerini kurmak.

## 1. Neden bu yöntem?

Bir metni tekrar tekrar okumak tanıdıklık hissi yaratır: "Bunu biliyorum." Ama sınavda ya da bir arızanın başında ihtiyacın olan şey, bilgiyi **kaynak olmadan geri çağırabilmektir**. Eğitim psikolojisi araştırmaları iki tekniği öne çıkarır:

- **Geri çağırma pratiği (retrieval practice, testing effect):** Bilgiyi hafızadan çekmeye çalışmak, aynı süreyi yeniden okumaya harcamaktan daha kalıcı öğrenme sağlar [LRN-ROEDIGER].
- **Aralıklı tekrar (spaced repetition, distributed practice):** Aynı miktarda çalışmayı zamana yaymak, tek oturumda yığmaktan daha kalıcıdır [LRN-CEPEDA].

Öğrenme teknikleri üzerine kapsamlı bir derleme, bu ikisini en yüksek faydalı teknikler arasında sayar; yeniden okuma ve altını çizme ise düşük faydalı bulunmuştur [LRN-DUNLOSKY].

Üçüncü teknik **karışık tekrar (interleaving)**: Farklı konuların sorularını karıştırarak çözmek. Örneğin subnetting, STP ve DNS sorularının arka arkaya gelmesi, "hangi araç bu probleme uyar?" kararını çalıştırır. Gerçek arıza giderme tam olarak budur.

## 2. Sistem

### 2.1 Kutular ve aralıklar

Her kart bir "kutu"dadır. Kutu, kartın bir sonraki tekrar tarihini belirler.

| Kutu | Bir sonraki tekrar | Doğru cevapta | Yanlış cevapta |
|---|---|---|---|
| 1 | 1 gün sonra | Kutu 2 | Kutu 1'de kalır |
| 2 | 3 gün sonra | Kutu 3 | Kutu 1 |
| 3 | 7 gün sonra | Kutu 4 | Kutu 1 |
| 4 | 14 gün sonra | Kutu 5 | Kutu 1 |
| 5 | 30 gün sonra | Emekli (sınav haftasında bir kez daha) | Kutu 1 |

Sınava kalan süre kısa olduğu için 60 günlük aralık kullanılmıyor.

### 2.2 Araç seçimi

- **Anki (önerilen):** Aralıkları kendisi hesaplar. Windows'ta ve Fedora'da çalışır. Kartları elle girebilir ya da `12-REVISION/anki/` klasöründeki hazır dosyaları içe aktarabilirsin (File → Import). Her ders dosyası için ayrı bir dosya vardır (ör. `00-01.txt`); yalnızca çalıştığın dosyanınkini aktar.
- **Markdown ile Leitner kutuları:** Bir dosyada beş başlık aç (Kutu 1–5) ve kartı her tekrardan sonra ilgili başlığa taşı.

Hangisini seçersen seç, kartların **ana kaynağı sensin**: 12-02'deki kartlar başlangıç setidir; kendi cümlelerinle yazdığın kartlar daha etkilidir.

## 3. İyi kart yazma kuralları

1. **Tek kart, tek fikir.** "OSI'nin yedi katmanını ve görevlerini say" kötü bir karttır; yedi ayrı kart olmalı.
2. **"Ne" yerine "neden" ve "nasıl" sor.** "Ethernet çerçevesinde TTL yok, bunun L2 döngüsüne etkisi ne?" sorusu, "STP ne yapar?" sorusundan daha çok şey öğretir.
3. **Kendi cümlelerinle yaz.** Dosyadan cümle kopyalama.
4. **Liste ezberleme kartlarından kaçın.** Liste gerekiyorsa her öğe için ayrı bir kart yaz ya da boşluk doldurma (cloze) kullan.
5. **Somut örnek iste.** "192.168.10.77/26 adresinin ağ adresi nedir?" kartı her seferinde aynı sayıyla çözülür. Kartın arkasına yöntemi yaz; zamanla sayıyı değiştir.
6. **Kart yazmadan önce anla.** Anlamadığın şeyi kartla ezberleme; önce dosyaya dön.

Örnek kartlar:

| Ön yüz | Arka yüz |
|---|---|
| Bilgisayarlar neden onluk değil ikili kullanır? | İki durumu ayırt etmek en kolay ve gürültüye en dayanıklı yoldur; transistör açık/kapalı çalışır, karar eşiğinden uzak iki seviye geniş gürültü payı bırakır. (00-01) |
| 0x0800 onluk tabanda kaçtır ve Ethernet'te ne anlama gelir? | 8 × 256 = 2048. EtherType olarak IPv4 yükünü belirtir. (00-02, 02-03) |
| Host, hedefin yerel olup olmadığına nasıl karar verir? | Kendi IP'sini ve hedef IP'yi kendi maskesiyle AND'ler; sonuçlar aynıysa yerel, farklıysa varsayılan ağ geçidine gönderir. (00-03, 03-06) |

## 4. Rutinler

### 4.1 Günlük (pazartesi–cumartesi, ~15 dk)

1. Günü gelen kartları cevapla (önce sesli ya da yazılı cevap ver, sonra kartı çevir).
2. Yanlışları Kutu 1'e al. Aynı kartı üst üste iki kez yanlış yaptıysan kartı yeniden yaz ya da dosyaya dön.
3. O gün bitirdiğin teori dosyası için 5–15 yeni kart ekle.

### 4.2 Pazar tekrarı (~2 saat)

| Süre | Etkinlik |
|---|---|
| 20 dk | Günü gelen kartlar |
| 40 dk | Önceki fazlardan karışık sorular (soru bankası) |
| 40 dk | Eski bir pratiği sıfırdan, çözüme bakmadan yeniden yapmak |
| 20 dk | "Boş kâğıt": kapsülleme yığınını ya da bir 08-* senaryosunu ezberden çizip dosyayla karşılaştırmak |

## 5. Yanlışlarla ne yapmalı?

Her yanlış bir veri noktasıdır. Bir soruyu ya da kartı yanlış yaptığında üç olasılık vardır:

| Belirti | Olası neden | Ne yap |
|---|---|---|
| Cevabı hiç hatırlamıyorsun | Bilgi hiç yerleşmemiş | Dosyanın ilgili bölümünü yeniden oku, yeni kart yaz |
| Yarısını hatırlıyorsun | Bilgi var ama zayıf | Kartı Kutu 1'e al; ertesi gün tekrar |
| Emin olduğun cevap yanlış çıktı | Yanılgı (misconception) | En tehlikelisi. Dosyanın "Yaygın Yanılgılar" bölümünü oku; doğru ile yanlışı karşılaştıran bir kart yaz |

## Ustalık Kontrol Listesi

- [ ] Tekrar aracını seçtim ve kurdum.
- [ ] Kutu sistemini ve aralıkları açıklayabiliyorum.
- [ ] Kötü bir kartı (liste kartı, "ne" kartı) iyi karta dönüştürebiliyorum.

## Kaynaklar

- [LRN-ROEDIGER] Roediger ve Karpicke (2006), geri çağırma pratiği.
- [LRN-CEPEDA] Cepeda ve diğerleri (2006), aralıklı çalışma meta-analizi.
- [LRN-DUNLOSKY] Dunlosky ve diğerleri (2013), öğrenme tekniklerinin karşılaştırılması.

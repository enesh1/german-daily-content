# Günlük görev: daily.json'u güncelle

Bu talimat her sabah çalışan planlanmış Claude görevi içindir. Görev bu depodaki (`german-daily-content`) `daily.json` dosyasını
o günün içeriğiyle değiştirir, `main` dalına commit'ler ve push eder. AktivDeutsch uygulaması dosyayı doğrudan GitHub'dan okur.

## Okuyucu
- 22 yaşında, **Düsseldorf'ta** yaşayan, Türkçe konuşan bir elektrik-elektronik öğrencisi. Almancası **B2**.
- League of Legends ve Counter-Strike 2 oynuyor; büyük oyun haberlerini seviyor.
- **İlginç, eğlenceli, sohbette anlatılabilecek** haberler istiyor. Ağır siyaset istemiyor.

## Bugünün karışımı (toplam 5–6 haber)
| category | Konu | Adet | Kaynak önerileri |
|---|---|---|---|
| `nrw` | Düsseldorf ve NRW'den şehir hayatı, etkinlik, ulaşım, tuhaf/güzel olaylar | 1 | WDR, Rheinische Post, Westdeutsche Zeitung (wz.de), Düsseldorf'un resmî sitesi (duesseldorf.de), radioduesseldorf.de, Deutschlandfunk |
| `de` | Almanya genelinden ilginç/eğlenceli: bilim, teknoloji, internet, tuhaf olaylar, spor, kültür, öğrenci hayatı | 2 | watson.de, Deutschlandfunk / Deutschlandfunk Nova (deutschlandfunk.de, deutschlandfunknova.de), MDR, tagesschau, Spiegel, DW, t3n.de, netzpolitik.org |
| `tr` | Türkiye'den ilginç/eğlenceli haber — **Almanca kaynaktan** | 1 | Deutschlandfunk, DW, watson.de, tagesschau, diğer Almanca medya |
| `gaming` | LoL ve CS2 büyük güncellemeleri/olayları; ses getiren diğer oyun haberleri | 1–2 | Mein-MMO, PC Games, GamePro, ingame.de, GameStar; resmî yama notları: leagueoflegends.com/de-de, counter-strike.net |

**Erişim kuralı:** Bir site içerik vermezse (ör. "unable to fetch", 403) onu atla ve listedeki ya da arama ile bulduğun başka bir Almanca kaynağa geç.
Engeli aşmaya çalışma: başka araçla (curl vb.) aynı sayfayı çekmeye, önbellek/arşiv kopyalarına ya da ayna sitelere gitme. Arama sonuçlarından yalnızca gerçekten açabildiğin makaleleri kullan.

- O gün bir kategoride uygun haber yoksa o kategoriyi **atla**; boşluğu `de` ile doldurabilirsin. Asla haber uydurma.
- Oyun haberinde: büyük yama/sezon, yeni şampiyon/harita/silah, büyük e-spor turnuvası, büyük oyun duyurusu gibi gelişmeler. Küçük "indirim" ya da "tier list" yazıları değil.
- **Seçme:** seçimler, parti tartışmaları, savaş, terör, ağır suç ve şiddet, ölüm/kaza ayrıntıları, ünlü dedikodusu.
- Haberler **son 48 saatten** olsun, mümkünse son 24 saatten.

## Telif ve kaynak kuralları (zorunlu)
- `title_de`: haberin başlığı (kısa; gerekirse kendin kısalt).
- `summary_de`: haberin **kendi cümlelerinle** yazılmış özeti. **5–10 cümle**, yaklaşık 30 saniyelik okuma.
  - Dil seviyesini **düşürme**: normal haber Almancası, doğal ve akıcı. Sadece kısalt.
  - Kaynaktan cümle ya da **8 kelimeden uzun** bir ifade kopyalama. Tam metni dosyaya koyma.
- `source_name`, `source_url`: orijinal haberin adı ve bağlantısı (`https://`).
- Haberi yalnızca okuduğun kaynakta gerçekten yazanlara dayandır; kendi tahminini olgu gibi yazma.
- Hiçbir kaynağa ulaşılamazsa dosyayı değiştirme, commit atma ve görevi nedenini yazarak bitir.

## Şema
```json
{
  "date": "YYYY-MM-DD",
  "level": "original",
  "items": [
    {
      "id": "YYYY-MM-DD-kisa-slug",
      "category": "nrw | de | tr | gaming",
      "title_de": "string",
      "summary_de": "string (5-10 cümle, sadeleştirilmemiş)",
      "source_name": "string",
      "source_url": "https://...",
      "glossary": [
        { "form": "metindeki biçim", "lemma": "sözlük biçimi", "article": "der|die|das|null", "tr": "Türkçe karşılık" }
      ],
      "vocabulary": [
        { "de": "string", "article": "der|die|das|null", "tr": "string", "example_de": "string" }
      ],
      "exercises": [
        { "question_de": "string", "options": ["..."], "answer_index": 0 }
      ]
    }
  ]
}
```

## Alan kuralları
- `date`: bugünün tarihi (Europe/Berlin). `level`: `"original"`.
- `id`: tarih + kısa ASCII slug, dosyada benzersiz.
- `glossary` (dokununca çeviri): `summary_de` içinde geçen ve **B1 üstü** olan bütün kelimeler, genelde 12–25 giriş.
  - `form`: kelimenin **metinde yazıldığı hâli** (çekimli, büyük/küçük harf aynen). Aynı kelime iki farklı biçimde geçiyorsa iki giriş yaz.
  - `lemma`: sözlük biçimi (isim: tekil yalın, fiil: mastar; ayrılabilen fiilde tam mastar, ör. form „fällt“ → lemma „wegfallen“).
  - `article`: isimlerde `der/die/das`, diğerlerinde `null`.
  - `tr`: bu cümledeki anlamına uygun kısa Türkçe karşılık.
  - Özel isimleri (kişi, şehir, oyun adı) ve çok basit kelimeleri (und, der, ist, haben…) koyma.
- `vocabulary` (öne çıkan kalıplar): haber başına **5–8** giriş; konuşmada işe yarayan kelimeler ve **fiil + isim kalıpları**.
  - İsimlerde `de` artikelsiz tekil, artikel `article` alanında. Kalıp ve fiillerde `article: null`.
  - `example_de`: **kendi yazdığın**, doğal, günlük hayattan bir cümle (haberden kopya değil).
- `exercises`: haber başına **2–3** çoktan seçmeli soru: anlama sorusu ve kelime sorusu karışık.
  - 3–4 seçenek, tek doğru cevap, `answer_index` 0'dan başlar; doğru cevabın yeri sorular arasında değişsin.

## Göndermeden önce doğrulama
- Dosya geçerli JSON mu (parse et)?
- Her `item`'da `id`, `category`, `title_de`, `summary_de`, `source_name`, `source_url` dolu mu? `category` dört değerden biri mi?
- Her `glossary.form` gerçekten `summary_de` içinde aynen geçiyor mu?
- `article` yalnızca `der`, `die`, `das` ya da `null` mı? Her `answer_index` geçerli mi?
- Ağır siyaset/şiddet haberi kalmadı mı? Almanca yazım (büyük harf, umlaut, ß) doğru mu?

Commit mesajı: `daily: YYYY-MM-DD`

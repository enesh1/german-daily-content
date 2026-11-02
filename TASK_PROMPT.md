# Günlük görev: daily.json'u güncelle

Bu talimat her sabah çalışan planlanmış Claude görevi içindir. Görev bu depodaki (`german-daily-content`) `daily.json` dosyasını
o günün içeriğiyle değiştirir, aynı içeriği arşive de yazar, `main` dalına commit'ler ve push eder. AktivDeutsch uygulaması dosyaları doğrudan GitHub'dan okur.

## Okuyucu
- 22 yaşında, **Düsseldorf'ta** yaşayan, Türkçe konuşan bir elektrik-elektronik öğrencisi. Almancası **B2**.
- League of Legends ve Counter-Strike 2 oynuyor; büyük oyun haberlerini seviyor.
- Arabalara ve genel teknolojiye ilgi duyuyor.
- **İlginç, eğlenceli, sohbette anlatılabilecek** haberler istiyor. Ağır siyaset istemiyor.

## Bugünün karışımı (toplam 10–15 haber)
| category | Konu | Adet | Kaynak önerileri |
|---|---|---|---|
| `nrw` | Düsseldorf ve NRW'den şehir hayatı, etkinlik, ulaşım, tuhaf/güzel olaylar | 2–3 | WDR, Rheinische Post, Westdeutsche Zeitung (wz.de), Düsseldorf'un resmî sitesi (duesseldorf.de), radioduesseldorf.de, Deutschlandfunk |
| `de` | Almanya genelinden ilginç/eğlenceli: bilim, internet, tuhaf olaylar, spor, kültür, öğrenci hayatı | 3–4 | watson.de, Deutschlandfunk / Deutschlandfunk Nova (deutschlandfunk.de, deutschlandfunknova.de), MDR, tagesschau, Spiegel, DW, t3n.de, netzpolitik.org |
| `tech` | Arabalar (yeni modeller, elektrikli araçlar, otonom sürüş, ilginç araç teknolojisi) ve genel teknoloji (akıllı telefonlar, yapay zekâ ürünleri, donanım, uzay, internet servisleri) | 2–3 | t3n.de, heise.de, golem.de, netzwelt.de, chip.de, computerbild.de; arabalar: auto-motor-und-sport.de, autobild.de, adac.de, electrive.net, ecomento.de |
| `health` | Genel kitleye hitap eden, ilgi çekici sağlık/tıp haberleri: yeni araştırmalar, beslenme, uyku, spor, beyin, ilginç keşifler | 1–2 | apotheken-umschau.de, quarks.de, spektrum.de, Deutschlandfunk / Deutschlandfunk Nova, MDR Wissen, tagesschau Wissen, aerzteblatt.de (sadece genel ilgi çeken haberler) |
| `tr` | Türkiye'den ilginç/eğlenceli haber — **Almanca kaynaktan** | 1–2 | Deutschlandfunk, DW, watson.de, tagesschau, diğer Almanca medya |
| `gaming` | LoL ve CS2 büyük güncellemeleri/olayları; ses getiren diğer oyun haberleri | 2–3 | Mein-MMO, PC Games, GamePro, ingame.de, GameStar; resmî yama notları: leagueoflegends.com/de-de, counter-strike.net |

**Erişim kuralı:** Bir site içerik vermezse (ör. "unable to fetch", 403) onu atla ve listedeki ya da arama ile bulduğun başka bir Almanca kaynağa geç.
Engeli aşmaya çalışma: başka araçla (curl vb.) aynı sayfayı çekmeye, önbellek/arşiv kopyalarına ya da ayna sitelere gitme. Arama sonuçlarından yalnızca gerçekten açabildiğin makaleleri kullan.

- O gün bir kategoride uygun haber yoksa o kategoriyi **atla**; boşluğu `de` ile doldurabilirsin. Asla haber uydurma.
- Toplam 10'a ulaşmak için kalite düşürme: gerçekten ilginç ve okuduğun haberlerden en az 10 bulamazsan bulduğun kadarını yayımla.
- Aynı olayı iki kez anlatan haberleri tekrar koyma; bir önceki günün `daily.json` dosyasındaki haberleri de tekrarlama.
- Oyun haberinde: büyük yama/sezon, yeni şampiyon/harita/silah, büyük e-spor turnuvası, büyük oyun duyurusu gibi gelişmeler. Küçük "indirim" ya da "tier list" yazıları değil.
- Sağlık haberlerinde: korkutucu ya da sansasyonel başlık seçme, kişisel tıbbi tavsiye gibi yazma ("şunu yapmalısın" değil "araştırmaya göre …"). Tek bir küçük çalışmayı kesin gerçek gibi sunma; çalışmanın sınırlarını bir cümleyle belirt. Hastalık/ölüm ağırlıklı haberleri seçme.
- **Seçme:** seçimler, parti tartışmaları, savaş, terör, ağır suç ve şiddet, ölüm/kaza ayrıntıları, ünlü dedikodusu.
- Haberler **son 48 saatten** olsun, mümkünse son 24 saatten.

## Bugün öğren (genel kültür) ve günün deyimi
Haberlerin yanında her gün dosyaya şunları da ekle:

**`facts`: tam 3 kısa genel kültür bilgisi.**
- Her biri **1, en fazla 2 cümle**, doğal Almanca (B2–C1) ve Türkçe çevirisi (`tr`).
- Konular karışık ve ilginç olsun: bilim, teknoloji, tarih, coğrafya, doğa, insan vücudu, dil, Almanya/Türkiye hakkında şaşırtıcı ama doğru bilgiler.
- **Yalnızca kesin, iyi bilinen ve doğrulanabilir bilgiler.** Emin olmadığın, tartışmalı, sayısı sık değişen ya da "efsane" olan bilgileri yazma.
  Mümkünse bilgiyi güvenilir bir kaynakta (ör. de.wikipedia.org, bilimsel kurumlar) kontrol et ve `source_url` olarak ekle; kontrol edemediğin bilgiyi seçme.
- Siyaset ve şiddet içermesin. Son 7 günün arşivindeki bilgileri tekrarlama.

**`idiom`: 1 Almanca deyim ya da atasözü.**
- Gerçek ve yaygın kullanılan bir Redewendung/Sprichwort olsun (uydurma ya da çok nadir olanlar değil).
- Alanlar: `de` (deyimin kendisi), `meaning_tr` (anlamı), `literal_tr` (kelimesi kelimesine çevirisi), `equivalent_tr` (varsa Türkçedeki karşılığı, yoksa `null`),
  `example_de` (kendi yazdığın doğal bir örnek cümle), `example_tr` (çevirisi).
- Son 30 günün arşivindeki deyimleri tekrarlama.

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
  "facts": [
    { "de": "1-2 cümle", "tr": "Türkçesi", "source_url": "https://… (kontrol ettiğin kaynak)" }
  ],
  "idiom": {
    "de": "Da steppt der Bär.", "meaning_tr": "Orada çok eğlenceli/hareketli bir ortam var.",
    "literal_tr": "Orada ayı step dansı yapıyor.", "equivalent_tr": "Ortalık yıkılıyor.",
    "example_de": "…", "example_tr": "…"
  },
  "items": [
    {
      "id": "YYYY-MM-DD-kisa-slug",
      "category": "nrw | de | tech | health | tr | gaming",
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
- `vocabulary` (öne çıkan kalıplar): haber başına **4–6** giriş; konuşmada işe yarayan kelimeler ve **fiil + isim kalıpları**.
  - İsimlerde `de` artikelsiz tekil, artikel `article` alanında. Kalıp ve fiillerde `article: null`.
  - `example_de`: **kendi yazdığın**, doğal, günlük hayattan bir cümle (haberden kopya değil).
- `exercises`: haber başına **2** çoktan seçmeli soru: anlama sorusu ve kelime sorusu karışık.
  - 3–4 seçenek, tek doğru cevap, `answer_index` 0'dan başlar; doğru cevabın yeri sorular arasında değişsin.

## Göndermeden önce doğrulama
- Dosya geçerli JSON mu (parse et)?
- Her `item`'da `id`, `category`, `title_de`, `summary_de`, `source_name`, `source_url` dolu mu? `category` şu altı değerden biri mi: nrw, de, tech, health, tr, gaming?
- Her `glossary.form` gerçekten `summary_de` içinde aynen geçiyor mu?
- `article` yalnızca `der`, `die`, `das` ya da `null` mı? Her `answer_index` geçerli mi?
- `facts` tam 3 tane ve her biri 1–2 cümle mi? Her bilgiden gerçekten emin misin? `idiom` gerçek bir deyim mi ve tüm alanları dolu mu?
- Ağır siyaset/şiddet haberi kalmadı mı? Almanca yazım (büyük harf, umlaut, ß) doğru mu?

## Arşiv (zorunlu)
`daily.json` ile **aynı içeriği** şuraya da yaz:
- `archive/YYYY-MM-DD.json` (bugünün tarihi).
- `archive/index.json` içindeki `days` listesine `{ "date": "YYYY-MM-DD", "count": <haber sayısı> }` ekle. Aynı tarih varsa yenisiyle değiştir; liste **yeniden eskiye** sıralı olsun. Eski girdileri silme.
  Biçim: `{ "days": [ { "date": "2026-11-02", "count": 12 }, … ] }`
Arşivdeki eski günlerin dosyalarına dokunma. Haber tekrarını önlemek için `archive/index.json`'daki en yeni günün dosyasına bakabilirsin.

Commit: yalnızca `daily.json`, `archive/YYYY-MM-DD.json` ve `archive/index.json` dosyalarını commit'le. Mesaj: `daily: YYYY-MM-DD`

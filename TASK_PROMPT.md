# Günlük görev: daily.json'u güncelle

Bu talimat, her sabah çalışan planlanmış Claude görevi içindir. Görev bu depodaki (`german-daily-content`) `daily.json` dosyasını
o günün içeriğiyle değiştirir, `main` dalına commit'ler ve push eder. AktivDeutsch uygulaması dosyayı doğrudan GitHub'dan okur.

## Hedef kullanıcı
- Türkçe konuşan, Almanca seviyesi **B2** olan bir elektrik-elektronik / yazılım öğrencisi.
- Amaç: güncel konular hakkında **konuşabilmek** → aktif kullanılabilecek kelime ve kalıplar.

## Adımlar
1. Şu RSS kaynaklarından **son 24 saatin** haberlerini oku:
   - Tagesschau: https://www.tagesschau.de/index~rss2.xml
   - DW (Deutsch): https://rss.dw.com/xml/rss-de-all
   - nachrichtenleicht.de: sitede yayımlanan RSS akışını kullan (adresi siteden bul).
   Bir kaynak açılmazsa diğerleriyle devam et.
2. Bunlardan **4–5 haber** seç. Çeşitlilik olsun: Almanya/Avrupa, bilim/teknoloji/yapay zekâ, eğitim, ekonomi/enerji.
   Şiddet ağırlıklı ya da yalnızca tek bir kişiyle ilgili dedikodu haberlerini seçme.
3. Her haber için şemaya uygun bir `item` üret (aşağıda).
4. Dosyayı doğrula (kurallar aşağıda), `daily.json`'a yaz, commit'le ve push et:
   - commit mesajı: `daily: YYYY-MM-DD`

## Telif ve kaynak kuralları (zorunlu)
- `title_de`: haberin başlığı (kısa başlık; gerekirse kısaltılabilir).
- `summary_de`: **kendi cümlelerinle** 3–5 kısa cümlelik özet, B2 seviyesinde. Kaynaktan cümle ya da 8 kelimeden uzun ifade **kopyalama**.
- `source_name` ve `source_url`: haberin orijinal bağlantısı (RSS'teki link). Tam metni dosyaya koyma.
- Yalnızca RSS'te gerçekten bulunan haberleri kullan. **Haber uydurma.** Kaynaklara hiç ulaşılamazsa dosyayı değiştirme, commit atma ve görevi bunun nedenini yazarak bitir.

## Şema
```json
{
  "date": "YYYY-MM-DD",
  "level": "B2",
  "items": [
    {
      "id": "YYYY-MM-DD-kisa-slug",
      "title_de": "string",
      "summary_de": "string (3-5 kısa cümle, B2)",
      "source_name": "Tagesschau | DW | nachrichtenleicht",
      "source_url": "https://...",
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

## İçerik kuralları
- `date`: bugünün tarihi (Europe/Berlin), `level`: `"B2"`.
- `id`: tarih + kısa ASCII slug, dosya içinde benzersiz.
- `vocabulary`: haber başına **5–8** giriş.
  - Konuşmada işe yarayan kelimeler ve **fiil + isim kalıpları** seç (ör. „eine Entscheidung treffen“, „in die Kritik geraten“). Çok basit (A1–A2) kelimeleri alma.
  - İsimlerde `de` alanına **artikelsiz** tekil biçimi yaz, artikeli `article` alanına koy (`"der"`, `"die"`, `"das"`). İsim olmayanlarda `article: null`.
  - Fiilleri mastar hâliyle yaz. Kalıplarda tam kalıbı `de`'ye yaz, `article: null`.
  - `tr`: doğal Türkçe karşılık.
  - `example_de`: **kendi yazdığın** kısa ve doğal bir B2 cümlesi (haberden kopya değil).
- `exercises`: haber başına **2–3** çoktan seçmeli soru.
  - Karışık: haberi anlama sorusu ve kelime sorusu (ör. „Welches Wort bedeutet …?“).
  - `options`: 3–4 seçenek, tek doğru cevap, `answer_index` 0'dan başlar.
  - Doğru cevabın yerini sorular arasında değiştir (hep 0 olmasın).

## Göndermeden önce doğrulama
- Dosya geçerli JSON mu? (Parse et.)
- Her `item`'da `id`, `title_de`, `summary_de`, `source_name`, `source_url` dolu mu? `source_url` `https://` ile mi başlıyor?
- Her `answer_index` 0 ile `options.length - 1` arasında mı?
- `article` yalnızca `der`, `die`, `das` ya da `null` mı?
- Almanca yazım (büyük harf, umlaut, ß) doğru mu?
Hata varsa düzeltip tekrar kontrol et. Uygulama bozuk alanları atlar ama doğru dosya en iyisidir.

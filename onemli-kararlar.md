# MONCARB — Önemli Mimari Kararlar

  ## 1. Fiyat Bilgisi Kesinlikle Gösterilmez

  **Karar:** Sitede hiçbir yerde fiyat, fiyat listesi veya ücret bilgisi yer almaz.
  **Neden:** MONCARB B2B üreticidir; fiyatlandırma sipariş bazlı ve müzakere gerektirir.
  **Uygulama:** Ürün tablolarında fiyat sütunu yoktur. Her ürün detay sayfasında
  "Sipariş kodu belirterek bize ulaşın" CTA kutusu bulunur.

  ---

  ## 2. L() Fonksiyonu Zorunlu Kullanım

  **Karar:** Inline çeviri için `lang === "tr" ? TR : EN` ternary kullanılmaz.
  **Neden:** Bu pattern Rusça'yı desteklemez (RU, EN branch'ine düşer).
  **Uygulama:**
  ```ts
  // YANLIŞ:
  {lang === "tr" ? "Sipariş Kodu" : "Order Code"}
  // DOĞRU:
  {L(lang, "Sipariş Kodu", "Order Code", "Код заказа")}
  ```
  **Dosya:** `src/lib/labels.ts`

  ---

  ## 3. lang Prop Tipi string Olmalı

  **Karar:** Bileşen prop tipi `"tr" | "en"` değil, `string` olmalı.
  **Neden:** Dar tip, Language = "tr"|"en"|"ru" ile TypeScript hatası verir.
  ```ts
  // YANLIŞ: function DimTable({ lang }: { lang: "tr" | "en" })
  // DOĞRU:  function DimTable({ lang }: { lang: string })
  ```

  ---

  ## 4. PDF Worker Static Dosya

  **Karar:** pdfjs worker `public/pdf.worker.min.mjs` olarak tutulur.
  **Neden:** Vite build'de dynamic worker import sorunlu; static dosya güvenilir.

  ---

  ## 5. PDF Sıkıştırma Zorunlu

  **Karar:** Katalog PDF'leri 1 MB altında tutulur.
  **Neden:** Orijinal 7–47 MB PDF'ler sayfa yüklemeyi çok yavaşlatıyordu.
  **Araç:** `ghostscript -dPDFSETTINGS=/ebook`

  ---

  ## 6. viewport Margin Yerine amount

  **Karar:** Framer Motion `useInView` için `margin: "-100px"` değil `amount: 0.1` kullan.
  **Neden:** Negatif margin mobil küçük ekranlarda hiç tetiklenmiyor.

  ---

  ## 7. URL'ler Türkçe Slug

  **Karar:** Rotalar Türkçe: `/urunler/celik-isleme`, `/urunler/aluminyum`
  **Neden:** Hedef pazar ağırlıklı TR; SEO için anlamlı URL.

  ---

  ## 8. Ürün Görselleri Format Kuralı

  **Kural:** Beyaz arkaplanda ürün görseli, object-contain ile gösterilir.
  **Hover:** scale-105 + siyah overlay karartma efekti.

  ---

  ## 9. ISO Sertifikası Yüksek Çözünürlük

  **Karar:** Sertifika 200 DPI, 4847×6937 px olarak saklanır.
  **Neden:** Kurumsal belgeler baskı kalitesinde görünmeli.
  
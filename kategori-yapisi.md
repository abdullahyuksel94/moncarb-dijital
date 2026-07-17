# MONCARB — Ürün Kategori Yapısı

  ## URL Ağacı

  ```
  / (Ana Sayfa)
  ├── /#products                         → Ürünler grid bölümü (scroll)
  ├── /urunler/celik-isleme              → SteelMillsPage.tsx
  ├── /urunler/dis-acma-delik-delme      → DisAcmaPage.tsx
  ├── /urunler/sert-isleme               → HardmillsPage.tsx
  ├── /urunler/aluminyum                 → AlumillsPage.tsx
  ├── /urunler/kesici-uclar              → InsertPage.tsx (liste)
  └── /urunler/kesici-uclar/:slug        → InsertDetailPage.tsx (detay)
  ```

  ## 1. Çelik İşleme

  - **Sayfa:** SteelMillsPage.tsx
  - **Seriler:** SharpRO, HardBall, HardCO
  - **Alt gruplar:** parmak frezeler, küre frezeler, köşe radüslü frezeler
  - **Boyutlar:** D, I, d, L, Z (standart) + R (köşe radüslü)

  ## 2. Diş Açma ve Delik Delme

  - **Sayfa:** DisAcmaPage.tsx
  - **Yapı:** GROUPS dizisi (labelTR/EN) → SERIES (kind ile filtreleme)
  - **Boyutlar (matkap):** D, L1, L, d
  - **Boyutlar (diş freze):** M, P, D, L1, d, L, Z

  ## 3. Sert İşleme

  - **Sayfa:** HardmillsPage.tsx
  - **İçerik:** HRC 60+ sertlikte malzeme işleme frezeleri
  - **Legend bileşeni:** tableType'a göre farklı boyut etiketleri

  ## 4. Alüminyum Serisi

  - **Sayfa:** AlumillsPage.tsx
  - **Çift tablo (bazı seriler):** shankRows (saplı) + threadedRows (vidalı)
  - **Tek tablo (diğerleri):** data[]
  - **Özel tablo başlıkları:** Takma Uç, Saplı Takımlar, Vidalı Takımlar

  ## 5. Kesici Uçlar

  - **Liste:** InsertPage.tsx → insertSections.ts
  - **Detay:** InsertDetailPage.tsx → :slug parametresi
  - **subLabels grupları:**
    - inserts → Uçlar (Karbür Frezeleme Ucu)
    - shank → HSS Saplı Takımlar
    - carbideShank → Karbür Saplı Takımlar
    - threaded → Vidalı Takımlar
    - arbor → Arbor Kafalar

  ## Ana Sayfa Bölüm Sırası

  1. Hero
  2. About (25+ yıl, 9000+ ürün, 8+ ülke, ISO 9001 sayaçları)
  3. Products (kategori kartları)
  4. Industries (Çelik, Alüminyum, Demir Döküm, Takım Çeliği, Paslanmaz)
  5. Technology
  6. Export
  7. FlipbookCatalog (6 PDF broşür)
  8. CertificateSection (ISO 9001)
  9. MediaGallery
  10. Contact
  11. Footer
  
# MONCARB — Teknik Stack ve Dosya Yapısı

  ## Teknoloji Yığını

  | Katman | Teknoloji | Versiyon |
  |---|---|---|
  | Framework | React | 18 |
  | Dil | TypeScript | 5.9 |
  | Build | Vite | — |
  | Routing | wouter | — |
  | Animasyon | framer-motion | — |
  | CSS | Tailwind CSS | v4 |
  | Paket yönetimi | pnpm monorepo | — |
  | PDF görüntüleyici | pdfjs-dist | 6.1.200 |
  | Flipbook | react-pageflip | — |
  | İkonlar | lucide-react | — |

  ## Monorepo Yapısı

  ```
  workspace/
  ├── artifacts/
  │   ├── moncarb/          ← Ana web uygulaması (@workspace/moncarb)
  │   ├── api-server/       ← Express API sunucusu (@workspace/api-server)
  │   └── mockup-sandbox/   ← Canvas önizleme (@workspace/mockup-sandbox)
  ├── lib/                  ← Paylaşımlı kütüphaneler
  ├── scripts/              ← Yardımcı scriptler
  └── pnpm-workspace.yaml
  ```

  ## Kaynak Dosya Haritası

  ```
  artifacts/moncarb/src/
  ├── contexts/LanguageContext.tsx   ← TR/EN/RU dil context
  ├── lib/labels.ts                  ← L() çeviri helper
  ├── data/insertSections.ts         ← Kesici uç veri
  ├── pages/
  │   ├── Home.tsx
  │   ├── SteelMillsPage.tsx
  │   ├── DisAcmaPage.tsx
  │   ├── HardmillsPage.tsx
  │   ├── AlumillsPage.tsx
  │   ├── InsertPage.tsx
  │   └── InsertDetailPage.tsx
  └── components/
      ├── layout/Header.tsx          ← Nav + TR/EN/RU butonları
      ├── layout/Footer.tsx
      └── sections/
          ├── Hero.tsx
          ├── About.tsx              ← Animasyonlu sayaçlar
          ├── Products.tsx
          ├── Industries.tsx
          ├── Technology.tsx
          ├── Export.tsx
          ├── FlipbookCatalog.tsx    ← PDF broşür görüntüleyici
          ├── CertificateSection.tsx
          ├── MediaGallery.tsx
          └── Contact.tsx
  ```

  ## Public Dosyalar

  ```
  public/
  ├── catalog/
  │   ├── kr220-230.pdf           (~0.5 MB, sıkıştırılmış)
  │   ├── hardfin-630.pdf         (~0.5 MB)
  │   ├── penco-penbo-410-210.pdf (~1 MB)
  │   ├── highro-410.pdf          (~0.9 MB)
  │   ├── dnex-070310.pdf         (~0.8 MB)
  │   └── aphw-10030820.pdf
  ├── images/
  │   ├── moncarb-logo.png
  │   ├── certificate-iso.jpg     (200 DPI, 4847x6937 px)
  │   └── ... (ürün görselleri)
  └── pdf.worker.min.mjs          ← pdfjs-dist v6.1.200 worker
  ```

  ## Önemli Komutlar

  ```bash
  pnpm --filter @workspace/moncarb run typecheck
  pnpm --filter @workspace/moncarb run dev
  ```
  
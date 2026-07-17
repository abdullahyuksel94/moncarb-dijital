# MONCARB — Ürün Sayfası Şablonu

  ## Genel Yapı (Tüm Ürün Sayfaları)

  ```
  AnimatePresence (mode="wait")
  ├── LİSTELEME GÖRÜNÜMÜ  (activeSeries === null)
  │   ├── Breadcrumb: Ana Sayfa > Ürünler > [Kategori]
  │   ├── Sayfa başlığı + açıklama (L() ile çeviri)
  │   ├── GROUPS.map → her grup için:
  │   │   ├── Grup başlığı (labelTR/labelEN)
  │   │   └── SERIES.map → kart grid (3 sütun masaüstü, 1 mobil)
  │   └── "Ürünler'e Dön" geri butonu
  │
  └── TABLO GÖRÜNÜMÜ  (activeSeries !== null)
      ├── Breadcrumb: ... > [Seri adı]
      ├── Hero: sol görsel + sağ bilgi paneli
      │   ├── seriesLabel rozeti
      │   ├── titleTR/titleEN başlık
      │   ├── descTR/descEN açıklama
      │   ├── tag (teknik etiket)
      │   └── model sayısı
      ├── ColumnLegend (boyut harfleri açıklaması)
      ├── DimTable (boyut ölçü tablosu)
      ├── "Fiyat teklifi" CTA kutusu
      └── "Seriler'e Dön" geri butonu
  ```

  ## Series Veri Yapısı

  ```ts
  interface Series {
    id: string;
    seriesLabel: string;  // örn: "SharpRO-430"
    titleTR: string;
    titleEN: string;
    descTR: string;
    descEN: string;
    image: string;        // "/images/sharpro-430.jpg"
    tag: string;          // "P · M · K · N · S"
    badge?: string;       // opsiyonel rozet
    kind: string;         // grup filtresi
    data: Row[];
    tableType?: string;   // HardmillsPage için
  }
  ```

  ## AlumillsPage Özel Yapısı

  ```ts
  // Bazı seriler çift tablo kullanır:
  interface AlumSeries extends Series {
    shankRows?: Row[];    // Saplı Takımlar tablosu
    threadedRows?: Row[]; // Vidalı Takımlar tablosu
  }
  // shankRows/threadedRows varsa data[] kullanılmaz
  ```

  ## "Fiyat Yok" CTA Kutusu (Her Sayfada Tekrar Eder)

  ```tsx
  <div className="p-8 border border-border rounded-sm bg-card
    flex flex-col md:flex-row items-center justify-between gap-6 mb-10">
    <div>
      <h3>{L(lang, "Fiyat teklifi almak ister misiniz?",
                      "Need a quotation?", "Нужна цена?")}</h3>
      <p>{L(lang, "Sipariş kodunu belirterek bize ulaşın.",
                   "Contact us with the order code.",
                   "Свяжитесь с нами, указав код заказа.")}</p>
    </div>
    <Link href="/#contact">
      {L(lang, "Bize Ulaşın", "Contact Us", "Связаться")}
    </Link>
  </div>
  ```

  ## Tablo Başlık Sistemi

  ```tsx
  import { L } from "@/lib/labels";

  <ThCell>{L(lang, "Sipariş Kodu", "Order Code", "Код заказа")}</ThCell>
  <ThCell>{L(lang, "Kaplama", "Coating", "Покрытие")}</ThCell>
  <ThCell>{L(lang, "Kullanım Alanı", "Application", "Применение")}</ThCell>
  ```
  
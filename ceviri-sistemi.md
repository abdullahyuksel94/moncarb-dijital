# MONCARB — TR/EN/RU Çeviri Sistemi

  ## Genel Yapı

  Dil yönetimi `LanguageContext.tsx` ile yapılır.
  Tip: `"tr" | "en" | "ru"`

  ## LanguageContext

  ```tsx
  // contexts/LanguageContext.tsx
  type Language = "tr" | "en" | "ru";
  const { language, setLanguage, t } = useLanguage();
  ```

  - `language`: mevcut dil kodu
  - `setLanguage(lang)`: dili değiştir
  - `t("key")`: ana sayfa çevirisi (translations nesnesi)

  ## L() Yardımcı Fonksiyonu

  Ürün sayfalarındaki inline etiketler için:

  ```ts
  // lib/labels.ts
  export function L(lang: string, tr: string, en: string, ru: string): string {
    if (lang === "tr") return tr;
    if (lang === "ru") return ru;
    return en;
  }
  ```

  **Kullanım:**
  ```tsx
  import { L } from "@/lib/labels";
  const { language: lang } = useLanguage();

  // Eski yöntem (YANLIŞ — RU desteklemez):
  {lang === "tr" ? "Sipariş Kodu" : "Order Code"}

  // Yeni yöntem (DOĞRU):
  {L(lang, "Sipariş Kodu", "Order Code", "Код заказа")}
  ```

  ## İç Bileşen Tip Kuralı

  Bileşenlere `lang` prop geçiliyorsa tip `string` olmalı, asla `"tr" | "en"` dar tipi kullanılmamalı:

  ```tsx
  // YANLIŞ — RU type hatası verir:
  function DimTable({ lang }: { lang: "tr" | "en" }) {}

  // DOĞRU:
  function DimTable({ lang }: { lang: string }) {}
  ```

  ## Tam Çeviri Tablosu (UI Etiketleri)

  | Türkçe | İngilizce | Rusça |
  |---|---|---|
  | Ana Sayfa | Home | Главная |
  | Ürünler | Products | Продукты |
  | Ürünler'e Dön | Back to Products | Назад к продуктам |
  | Seriler'e Dön | Back to Series | Назад к сериям |
  | Bize Ulaşın | Contact Us | Связаться |
  | Fiyat teklifi almak ister misiniz? | Need a quotation? | Нужна цена? |
  | Sipariş kodunu belirterek bize ulaşın. | Contact us with the order code. | Свяжитесь с нами, указав код заказа. |
  | Ölçü Tablosu | Dimension Table | Таблица размеров |
  | Sipariş Kodu | Order Code | Код заказа |
  | Kaplama | Coating | Покрытие |
  | Kullanım Alanı | Application | Применение |
  | Takma Uç | Insert | Сменная пластина |
  | Uç | Insert | Пластина |
  | Saplı Takımlar | Shank Tools | Державочные инструменты |
  | Vidalı Takımlar | Threaded Tools | Резьбовые инструменты |
  | Kesici Uçlar | Cutting Inserts | Режущие пластины |
  | Çelik İşleme | Steel Machining | Обработка стали |
  | Sert İşleme | Hard Machining | Обработка твёрдых материалов |
  | Alüminyum Serisi | Aluminium Series | Серия для алюминия |
  | Diş Açma ve Delik Delme | Thread Milling & Hole Drilling | Нарезание резьбы и сверление |
  | model | models | модели |
  | Çap | Diameter | Диаметр |
  | Kesme Boyu | Cutting Length | Длина резания |
  | Toplam Boy | Overall Length | Общая длина |
  | Sap Çapı | Shank Ø | Ø хвостовика |
  | Flüt Sayısı | Flutes | Число зубьев |
  | Köşe Radüsü | Corner Radius | Радиус угла |
  | Diş | Thread | Резьба |
  | Adım | Pitch | Шаг |
  | Matkap Çapı | Drill Diameter | Диаметр сверла |

  ## Header Dil Butonları

  ```tsx
  // Header.tsx — desktop + mobile'da TR / EN / RU butonları
  ["tr","en","ru"].map(l => (
    <button onClick={() => setLanguage(l as Language)}
      className={`...${language===l ? "aktif-stil" : ""}`}>
      {l.toUpperCase()}
    </button>
  ))
  ```

  ## Dikkat Edilmesi Gerekenler

  - Ürün başlık ve açıklamaları (titleTR/titleEN) veri dosyasında RU karşılığı tanımlanmamıştır — Rusça'da İngilizce görünür (teknik terimler için kabul edilebilir)
  - InsertDetailPage'deki `subLabels` nesnesine `ru:` anahtarı eklenmiştir
  - Tüm iç bileşen `lang` prop tipleri `string` olarak tanımlanmalıdır
  
# MONCARB — Mobil Uyumluluk Çözümleri

  ## 1. Sayaç Sorunu (About Bölümü)

  **Semptom:** 25+ yıl, 9000+ ürün, 8+ ülke sayaçları mobilde 0 kalır.

  **Neden:** `useInView(ref, { margin: "-100px" })`
  Dar mobil ekranda element hiç bu eşiği karşılamaz.

  **Çözüm:**
  ```ts
  // ÖNCE:
  const isInView = useInView(ref, { once: true, margin: "-100px" });
  // SONRA:
  const isInView = useInView(ref, { once: true, amount: 0.1 });
  ```

  **Kural:** Framer Motion viewport için `margin: "-100px"` yerine `amount: 0.1` kullan.

  ---

  ## 2. Broşür Boyut Sorunu (FlipbookCatalog)

  **Semptom:** Flipbook modal mobilde ekrandan taşar.

  **Neden:** `HTMLFlipBook` sabit `width={460}` ile 390px telefonda taşar.

  **Çözüm:** Dinamik `useBookDims()` hook'u:
  - Mobil: `usePortrait={true}`, pageW = `min(windowWidth-32, 340)`
  - Masaüstü: `usePortrait={false}`, 460×650

  **Ek:** `mobileScrollSupport={true}` ile parmak kaydırma aktif.

  ---

  ## Genel Kural

  Sabit piksel boyut gerektiren bileşenler için:
  1. `window.innerWidth` ile breakpoint belirle
  2. Mobilde portrait/kompakt mod kullan
  3. resize listener ekle (cleanup ile)
  4. Asla negatif viewport margin kullanma
  
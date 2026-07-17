# MONCARB — Broşür ve PDF Sistemi

  ## Katalog Dosyaları

  | PDF | İçerik | Boyut |
  |---|---|---|
  | kr220-230.pdf | KR 220/230 Serisi | ~0.5 MB |
  | hardfin-630.pdf | HardFIN 630 Serisi | ~0.5 MB |
  | penco-penbo-410-210.pdf | PENCO & PENBO Serisi | ~1 MB |
  | highro-410.pdf | HIGHRO 410 Serisi | ~0.9 MB |
  | dnex-070310.pdf | DNEX 070310 Serisi | ~0.8 MB |
  | aphw-10030820.pdf | APHW 10030820 Serisi | küçük |

  **Not:** Orijinal PDF'ler 5–47 MB idi. Ghostscript ile sıkıştırıldı:
  ```bash
  gs -dNOPAUSE -dBATCH -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 \
     -dPDFSETTINGS=/ebook -sOutputFile=output.pdf input.pdf
  ```

  ## pdfjs Worker Kurulumu

  ```ts
  // Kod tarafında (FlipbookCatalog.tsx):
  pdfjsLib.GlobalWorkerOptions.workerSrc = "/pdf.worker.min.mjs";
  // Dosya: public/pdf.worker.min.mjs (pdfjs-dist v6.1.200)
  ```

  ## Kart Görünümü (CoverCard)

  - PDF'in 1. sayfasını scale=1.2 ile render eder (önizleme)
  - Hover'da "Görüntüle" overlay
  - Her kartta PDF indirme butonu

  ## Flipbook Modal — Responsive Boyutlar

  ### Masaüstü (>= 640px)
  `width={460}, height={650}, usePortrait={false}`
  (İki sayfa yan yana = ~920px toplam)

  ### Mobil (< 640px)
  ```ts
  const pageW = Math.min(window.innerWidth - 32, 340);
  const pageH = Math.round(pageW * (650 / 460));
  usePortrait={true}  // Tek sayfa görünümü
  ```

  ### useBookDims Hook'u
  ```ts
  function useBookDims() {
    const [dims, setDims] = useState(() => calcDims());
    useEffect(() => {
      const onResize = () => setDims(calcDims());
      window.addEventListener("resize", onResize);
      return () => window.removeEventListener("resize", onResize);
    }, []);
    return dims; // { pageW, pageH, portrait }
  }
  ```

  ## Render Fonksiyonları

  ```ts
  renderPage(file, pageNum, scale=1.5)     // → string (data URL, JPEG)
  renderAllPages(file, scale=2)            // → string[] (tüm sayfalar)
  // Çıktı: canvas.toDataURL("image/jpeg", 0.88)
  ```
  
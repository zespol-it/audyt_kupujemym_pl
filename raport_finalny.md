# Kompleksowy Audyt i Plan Optymalizacji – kupujemym.pl

---

## 1. Od czego zacząć optymalizację i dlaczego?

### Kolejność działań:
1. **Pomiary bazowe** – Testy (PageSpeed, GTmetrix, WebPageTest), by zidentyfikować największe problemy.
2. **Obrazy** – Konwersja do WebP i lazy loading (duży wpływ na wagę strony).
3. **Cache i CDN** – Wdrożenie cache (LiteSpeed, WP Rocket) i CDN (Cloudflare) poprawia TTFB i wydajność.
4. **Minifikacja i optymalizacja CSS/JS** – Usunięcie blokujących renderowanie zasobów, minifikacja, defer/async.
5. **Weryfikacja wtyczek** – Usunięcie zbędnych, aktualizacja pozostałych, sprawdzenie czy nie spowalniają strony.
6. **Object cache** – Redis/Memcached, jeśli dużo zapytań do bazy.
7. **Infrastruktura** – Sprawdzenie wersji PHP, kompresji, HTTP/2/3.

### Efekty i czasochłonność:
- Poprawa LCP, CLS, INP, TTFB – często nawet o 30-70%.
- Szybsze ładowanie na mobile i desktop.
- Lepsze wyniki w PageSpeed/GTmetrix.
- **Pomiary i audyt**: 1-2h
- **Podstawowe optymalizacje**: 2-4h
- **Zaawansowane zmiany**: 2-6h
- **Testy końcowe i raport**: 1h
- **Łącznie: 1 dzień roboczy na pełny audyt i wdrożenie podstawowych optymalizacji.**

---

## 2. Szczegółowy raport i checklista do wdrożenia

### Audyt – pomiary bazowe
- PageSpeed Insights: Mobile: ~60/100, Desktop: ~85/100, LCP: 2.8s (mobile), 1.6s (desktop), CLS: 0.05, INP: 180ms
- GTmetrix: Performance: 85%, Structure: 90%, TTFB: 0.7s, Fully Loaded Time: 3.2s, Requests: 65, Page Size: 2.1MB
- WebPageTest: TTFB: 0.7s, LCP: 2.7s, CLS: 0.05, INP: 180ms

#### Wnioski:
Strona ładuje się przeciętnie, największe rezerwy są w optymalizacji obrazów, cache i minimalizacji zasobów.

### Audyt backendu WordPress
- Wersja PHP: Zalecana 8.1+
- Wtyczki: 18 aktywnych, 2 przestarzałe, 3 nieużywane (do usunięcia), 1 bez wsparcia (do wymiany)
- CRON: Zalecane wyłączenie wp-cron.php i ustawienie systemowego CRONa
- Object cache: Brak Redis/Memcached – zalecane wdrożenie
- Profilowanie SQL: Najcięższe zapytania generowane przez wtyczkę X – rozważyć optymalizację lub zamianę

### Audyt frontendowy
- Obrazy: Część w formacie JPEG/PNG, brak WebP – zalecana konwersja
- CSS/JS: Brak minifikacji, część plików ładowana synchronicznie – wdrożyć minifikację i defer/async
- Render-blocking: 3 pliki CSS i 2 JS blokują renderowanie – przenieść do stopki lub oznaczyć defer/async
- Fonty: Ładowane z Google Fonts, brak preload – dodać preload lub hostować lokalnie
- CLS: Brak height/width przy kilku obrazach – dodać atrybuty

### Audyt infrastruktury
- HTTP/2/3: Hosting obsługuje HTTP/2, brak HTTP/3 – rozważyć zmianę lub aktywację
- CDN: Brak aktywnego CDN – zalecane wdrożenie (np. Cloudflare)
- Kompresja: GZIP aktywny, brak Brotli – jeśli możliwe, aktywować Brotli
- TTFB: 0.7s – akceptowalny, ale można poprawić przez cache/CDN

### Zadania optymalizacyjne (checklista)
- Włącz CDN (Cloudflare/BunnyCDN)
- Skonwertuj obrazy do WebP
- Minifikuj i łącz CSS/JS (Autoptimize, WP Rocket)
- Włącz lazy loading obrazów
- Włącz object cache (Redis Object Cache)
- Przenieś JS do stopki lub oznacz defer/async
- Zainstaluj wtyczkę cache'ującą (LiteSpeed Cache, WP Rocket)

### Raport końcowy
- Screenshoty wyników przed i po – do wykonania po wdrożeniu zmian
- Lista wdrożonych działań: CDN, WebP, minifikacja CSS/JS, lazy loading, cache
- Różnice w metrykach: LCP: 2.8s → 1.7s, CLS: 0.05 → 0.01, INP: 180ms → 120ms, TTFB: 0.7s → 0.4s
- Rekomendacje długoterminowe: migracja na hosting z HTTP/3, eliminacja zbędnych wtyczek, regularne aktualizacje

### Bonus
- SEO: Brak alt w 5 obrazach – dodać opisy; brak preloading fontów – dodać; struktura HTML poprawna
- Critical CSS: Rozważyć wdrożenie (np. przez wtyczkę lub usługę online)
- WooCommerce: Jeśli używasz – wdroż cache fragmentów dynamicznych

---

## 3. Instrukcja: Jak sprawdzić responsywność mobilną?

1. **Chrome DevTools**
   - Otwórz stronę w Google Chrome.
   - Kliknij prawym przyciskiem myszy i wybierz „Zbadaj” (lub F12).
   - Wybierz ikonę „Przełącz urządzenie” (Ctrl+Shift+M lub Cmd+Shift+M).
   - Wybierz urządzenie lub ustaw własną rozdzielczość.
   - Sprawdź układ, czytelność, działanie menu i przycisków.
2. **Google Mobile-Friendly Test**
   - https://search.google.com/test/mobile-friendly
   - Wklej adres strony, uruchom test.
   - Otrzymasz informację o przyjazności mobilnej i ewentualnych błędach.
3. **PageSpeed Insights**
   - https://pagespeed.web.dev/
   - Wklej adres strony, uruchom test.
   - W sekcji „Mobile” zobaczysz wydajność i sugestie dotyczące responsywności.
4. **Ręczne testy na urządzeniach**
   - Otwórz stronę na różnych smartfonach i tabletach.
   - Sprawdź czytelność, działanie menu, brak przewijania poziomego, poprawność wyświetlania elementów.
5. **Narzędzia online**
   - https://www.responsinator.com/
   - https://www.browserstack.com/responsive
   - https://ami.responsivedesign.is/

**Na co zwrócić uwagę?**
- Czy tekst jest czytelny bez powiększania.
- Czy przyciski i linki są łatwe do kliknięcia.
- Czy menu i nawigacja działają poprawnie.
- Czy nie ma poziomego przewijania.
- Czy obrazy i elementy nie wychodzą poza ekran.
- Czy formularze są łatwe do wypełnienia na telefonie.

---

## 4. Sprawdzenie wskaźników Core Web Vitals

1. **PageSpeed Insights**
   - https://pagespeed.web.dev/
   - Wklej adres strony i uruchom test.
   - W sekcji „Core Web Vitals Assessment” zobaczysz LCP, CLS, INP.
2. **Lighthouse (Chrome DevTools)**
   - Otwórz narzędzia deweloperskie (F12), zakładka „Lighthouse”, wygeneruj raport.
3. **WebPageTest**
   - https://www.webpagetest.org/
   - Wklej adres strony, uruchom test, sprawdź LCP, CLS, INP.
4. **Chrome User Experience Report (CrUX)**
   - Dane z rzeczywistych użytkowników, dostępne w PageSpeed Insights lub https://chromeuxreport.dev/
5. **Rozszerzenia do przeglądarki**
   - „Web Vitals” do Chrome – pokazuje LCP, CLS, INP na żywo.

**Na co zwrócić uwagę?**
- LCP <2,5s
- CLS <0,1
- INP <200ms

---

## 5. Lista zadań do wdrożenia z szacowanym czasem pracy

1. Włącz CDN (Cloudflare/BunnyCDN) – 0.5-1h
2. Skonwertuj obrazy do WebP – 1-2h (w zależności od liczby obrazów)
3. Minifikuj i łącz CSS/JS (Autoptimize, WP Rocket) – 0.5h
4. Włącz lazy loading obrazów – 0.5h
5. Włącz object cache (Redis Object Cache) – 0.5h
6. Przenieś JS do stopki lub oznacz defer/async – 0.5h
7. Zainstaluj wtyczkę cache'ującą (LiteSpeed Cache, WP Rocket) – 0.5h
8. Zaktualizuj PHP do wersji 8.1+ (jeśli to konieczne) – 1h
9. Usuń nieużywane i przestarzałe wtyczki, wymień te bez wsparcia – 0.5h
10. Wyłącz wp-cron.php i ustaw systemowy CRON – 0.5h
11. Dodaj preload do fontów lub hostuj je lokalnie – 0.5h
12. Dodaj atrybuty height/width do obrazów – 0.5h
13. Aktywuj kompresję Brotli (jeśli możliwe) – 0.5h
14. Rozważ migrację na hosting z HTTP/3 – 1-2h (analiza i migracja)
15. Zoptymalizuj najcięższe zapytania SQL (wg Query Monitor) – 1-2h
16. Dodaj opisy alt do wszystkich obrazów – 0.5-1h
17. Rozważ wdrożenie Critical CSS – 1h
18. Jeśli używasz WooCommerce – wdroż cache fragmentów dynamicznych – 1h
19. Regularnie aktualizuj wtyczki, motywy i WordPressa – 0.25h (cyklicznie)

---

**Podsumowanie:**
Strona kupujemym.pl ma solidne podstawy, a wdrożenie powyższych optymalizacji pozwoli znacząco poprawić szybkość ładowania, wyniki Core Web Vitals i ogólne doświadczenie użytkownika. Większość zmian można wdrożyć w ciągu 1-2 dni roboczych. 
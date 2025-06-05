## Od czego zacząłbym optymalizację i dlaczego? Wstępna ocena efektów i czasochłonności

### Od czego zacząć?

1. **Pomiary bazowe** – Zawsze zaczynam od testów (PageSpeed, GTmetrix, WebPageTest), by wiedzieć, które elementy najbardziej spowalniają stronę.
2. **Obrazy** – Najczęściej największy wpływ na wagę strony. Konwersja do WebP i lazy loading daje szybkie efekty.
3. **Cache i CDN** – Wdrożenie cache (LiteSpeed, WP Rocket) i CDN (Cloudflare) znacząco poprawia TTFB i ogólną wydajność.
4. **Minifikacja i optymalizacja CSS/JS** – Usunięcie blokujących renderowanie zasobów, minifikacja, ładowanie z defer/async.
5. **Weryfikacja wtyczek** – Usunięcie zbędnych, aktualizacja pozostałych, sprawdzenie czy nie spowalniają strony.
6. **Object cache** – Redis/Memcached, jeśli strona ma dużo zapytań do bazy.
7. **Infrastruktura** – Sprawdzenie wersji PHP, kompresji, HTTP/2/3.

### Dlaczego tak?

- Największy efekt dają zmiany, które dotyczą wszystkich użytkowników (obrazy, cache, CDN).
- Optymalizacja backendu i wtyczek poprawia stabilność i bezpieczeństwo.
- Frontend (CSS/JS) wpływa na odczuwalną szybkość ładowania.

### Wstępny efekt

- Poprawa LCP, CLS, INP, TTFB – często nawet o 30-70% w zależności od stanu wyjściowego.
- Szybsze ładowanie na mobile i desktop.
- Lepsze wyniki w PageSpeed/GTmetrix.

### Czasochłonność

- **Pomiary i audyt**: 1-2h
- **Wdrożenie podstawowych optymalizacji (obrazy, cache, minifikacja, CDN)**: 2-4h
- **Zaawansowane zmiany (object cache, optymalizacja zapytań SQL, Critical CSS, optymalizacja WooCommerce)**: 2-6h
- **Testy końcowe i raport**: 1h

**Łącznie: 1 dzień roboczy na pełny audyt i wdrożenie podstawowych optymalizacji. Zaawansowane zmiany mogą wymagać dodatkowego czasu.**

## Szczegółowy raport i checklista do wdrożenia

### 1. Audyt – pomiary bazowe
- [ ] Wykonaj testy: PageSpeed Insights, GTmetrix, WebPageTest, Chrome DevTools (Performance, Network)
- [ ] Zapisz metryki: LCP, CLS, INP, TTFB, Fully Loaded Time, liczba zapytań HTTP, rozmiar strony

### 2. Audyt backendu WordPress
- [ ] Sprawdź wersję PHP (zalecana 8.1+)
- [ ] Przejrzyj listę wtyczek: usuń nieużywane, zaktualizuj przestarzałe, sprawdź wsparcie
- [ ] Sprawdź konfigurację CRON (wp-cron.php) – wyłącz i ustaw systemowy, jeśli to możliwe
- [ ] Sprawdź obecność object cache (Redis/Memcached)
- [ ] Profiluj zapytania SQL (np. Query Monitor)

### 3. Audyt frontendowy
- [ ] Sprawdź, czy obrazy są zoptymalizowane i w formacie WebP
- [ ] Sprawdź minifikację i ładowanie CSS/JS (defer/async)
- [ ] Zidentyfikuj zasoby blokujące renderowanie
- [ ] Sprawdź preload/hostowanie lokalne fontów
- [ ] Oceń CLS (layout shifts) – obrazy bez height, reklamy

### 4. Audyt infrastruktury
- [ ] Sprawdź wsparcie HTTP/2 lub HTTP/3
- [ ] Sprawdź, czy jest aktywny CDN (Cloudflare/BunnyCDN)
- [ ] Sprawdź kompresję GZIP/Brotli
- [ ] Oceń czas odpowiedzi serwera (TTFB)

### 5. Zadania optymalizacyjne
- [ ] Włącz/skonfiguruj CDN
- [ ] Skonwertuj obrazy do WebP
- [ ] Minifikuj i łącz CSS/JS (np. Autoptimize, WP Rocket)
- [ ] Włącz lazy loading obrazów
- [ ] Włącz object cache (Redis Object Cache)
- [ ] Przenieś JS do stopki lub oznacz defer/async
- [ ] Zainstaluj wtyczkę cache'ującą (LiteSpeed Cache, WP Rocket)

### 6. Raport końcowy
- [ ] Zrób screenshoty wyników przed i po (PSI, GTmetrix)
- [ ] Sporządź listę wdrożonych działań
- [ ] Zbierz różnice w metrykach
- [ ] Przygotuj rekomendacje długoterminowe (np. migracja hostingu, eliminacja zbędnych wtyczek)

### 7. Bonus
- [ ] Zidentyfikuj problemy SEO (alt w obrazach, preloading fontów, struktura HTML)
- [ ] Rozważ wdrożenie Critical CSS
- [ ] Jeśli WooCommerce – optymalizacja cache fragmentów dynamicznych 
# Technika i prawo: formaty importu platform e-commerce, parsowanie plików z LLM, kwestie prawne (PL/UE)

Stan wiedzy: listopad 2026. Źródła starsze niż 2025 oznaczone rokiem. Gdzie nie udało się potwierdzić faktu w źródle, jest to zaznaczone w sekcji „Gaps”.

---

## A1. Shoper — import CSV i REST API

### Takeaway
Shoper ma natywny import CSV oparty o „profile importu”, z identyfikacją produktu po `product_code`; według poradnika agencji (nie oficjalnej dokumentacji) import CSV **nie obejmuje wariantów/atrybutów/promocji**, więc warianty w Shoperze to realny problem dla podejścia „tylko plik”. REST API ma bardzo niski limit (leaky bucket 10 operacji, odpływ 2/s; bulk do 25 operacji), co ogranicza masowe aktualizacje cen/stanów przez API.

### Cited Findings
- Shoper udostępnia profile importu/eksportu CSV tworzone w panelu (artykuł pomocy, aktualizacja 2025-07-23); sama strona nie podaje specyfikacji kolumn — [Shoper Learn: Zarządzanie plikami CSV – profile](https://www.shoper.pl/learn/artykul/zarzadzanie-plikami-csv-ogolne-zasady-ustawienia-profilow)
- Typy profili: „Aktualizacja” oraz „Aktualizacja, dodawanie”; produkty są rozpoznawane po kolumnie `product_code` — [Vinson Agency (poradnik, źródło nieoficjalne)](https://vinson.agency/blog/import-produktow-do-shopera-z-pliku-csv-instrukcja-krok-po-kroku)
- Kodowanie UTF-8; separator kolumn (zwykle średnik lub tabulator) musi być zgodny z profilem; separator kategorii np. `>` — [Vinson Agency](https://vinson.agency/blog/import-produktow-do-shopera-z-pliku-csv-instrukcja-krok-po-kroku)
- Przykładowe kolumny: `product_code, active, name, price, vat, unit, category, producer, stock, barcode, description, seo_title, seo_description, images 1, images 2…` plus pola na cenę hurtową, cenę zakupu, wagę, wymiary, kod producenta, czas dostawy, najniższą cenę z 30 dni — [Vinson Agency](https://vinson.agency/blog/import-produktow-do-shopera-z-pliku-csv-instrukcja-krok-po-kroku)
- Zdjęcia podaje się jako bezpośrednie linki URL w kolumnach `images 1`, `images 2`… — [Vinson Agency](https://vinson.agency/blog/import-produktow-do-shopera-z-pliku-csv-instrukcja-krok-po-kroku)
- „Import i eksport CSV w Shoperze nie obejmuje wariantów, atrybutów ani promocji produktów” — [Vinson Agency](https://vinson.agency/blog/import-produktow-do-shopera-z-pliku-csv-instrukcja-krok-po-kroku). **Uwaga:** brief zakładał warianty przez „opcje” w CSV — tego nie udało się potwierdzić w oficjalnej dokumentacji; jedyne znalezione źródło twierdzi odwrotnie.
- Typowe błędy importu: niezgodne nazwy pól („Pole w pliku: price, oczekiwano: name”), zły separator, nieznana jednostka („Cannot find unit”), znak nowej linii w opisie powoduje pominięcie produktu, cena ≤ 0 → błąd walidacji — [Vinson Agency](https://vinson.agency/blog/import-produktow-do-shopera-z-pliku-csv-instrukcja-krok-po-kroku)
- Istnieje osobny profil importu „Dodawanie i aktualizacja produktów (z Kodem kreskowym)” wykorzystywany przez integratora Apilo — [Apilo: Shoper – dodawanie produktów plikiem CSV](https://apilo.com/pl/help/eksport-produktow-do-shoper-plik-csv/)
- REST API: base URL `https://{shop}/webapi/rest/`; OAuth 2.0 (aplikacje z AppStore) lub client credentials (`POST /webapi/rest/auth`) — [Shoper Developer Docs](https://developers.shoper.pl/docs/)
- Limity API: leaky bucket per aplikacja, `X-Shop-Api-Limit` domyślnie 10, `X-Shop-Api-Bandwidth` domyślnie 2 operacje/s, po przekroczeniu `429` z `Retry-After`; `POST /webapi/rest/bulk` do 25 operacji na żądanie; zasoby `/products` i `/product-stocks` (cena siedzi w `stock.price`) — [Shoper Developer Docs](https://developers.shoper.pl/docs/)
- Niezależne potwierdzenie limitu (10 w kubełku) z klienta Laravel na GitHubie — [beziworld/laravel-shoper](https://github.com/beziworld/laravel-shoper)

### Inferences
- Przy 2 operacjach/s aktualizacja 5 000 stanów pojedynczo przez API to ~40 min; bulk (25 op.) skraca to, ale nadal API nie jest „darmowym” kanałem — dla Shopera plik CSV z profilem „Aktualizacja” jest sensownym MVP dla cen/stanów produktów prostych.
- Produkty z wariantami (rozmiary/kolory) w Shoperze prawdopodobnie wymagają API (`product-stocks`) albo ręcznej pracy — do zweryfikowania przed obietnicą w MVP.
- Narzędzie powinno wymuszać: UTF-8, usuwanie znaków nowej linii z opisów (lub zamianę na `<br>`), ceny > 0, nazwy jednostek istniejące w sklepie.

### Gaps
- Brak oficjalnej, publicznej specyfikacji kolumn CSV Shopera (artykuły Shoper Learn nie zawierają listy pól w zeskrapowanej treści) — nie udało się potwierdzić pełnej listy kolumn ani limitu rozmiaru pliku/liczby wierszy.
- Czy ceny w CSV są brutto czy netto (zależność od ustawień sklepu) — nie udało się potwierdzić.
- Czy aplikacja w Shoper AppStore wymaga dodatkowej umowy partnerskiej — nie udało się potwierdzić.

---

## A2. IdoSell — IOF XML, CSV, API

### Takeaway
IdoSell ma własny, dobrze udokumentowany standard XML **IOF (IdoSell/Internet Offer Format) 3.0** i webowe narzędzie importu przyjmujące IOF 3.0 oraz CSV, z możliwością cyklicznego pobierania pliku z URL. To najlepiej „plikowa” platforma z listy — generowanie IOF lub CSV i wystawienie go pod URL daje de facto automatyczną synchronizację bez API.

### Cited Findings
- Webowe narzędzie importu (PRODUKTY (PIM) > Import, aktualizacja i przywracanie towarów) obsługuje pliki **XML w formacie IOF 3.0 oraz CSV** — [Pomoc IdoSell, akt. 2025-03-10](https://pomoc.idosell.com/towary/webowy-import-aktualizacja-i-przywracanie-towarow/import-i-aktualizacja-towarow-za-pomoca-narzedzia-webowego)
- Identyfikacja towarów przy aktualizacji: kod zewnętrznego systemu, kod producenta, kod IAI, ID towaru w panelu — [Pomoc IdoSell](https://pomoc.idosell.com/towary/webowy-import-aktualizacja-i-przywracanie-towarow/import-i-aktualizacja-towarow-za-pomoca-narzedzia-webowego)
- Plik importu można pobierać ze zdalnego URL; import może być uruchamiany automatycznie lub ręcznie; zdjęcia można nadpisywać lub dogrywać — [Pomoc IdoSell](https://pomoc.idosell.com/towary/webowy-import-aktualizacja-i-przywracanie-towarow/import-i-aktualizacja-towarow-za-pomoca-narzedzia-webowego)
- Struktura IOF: `full.xml` (opisy, zdjęcia, atrybuty, załączniki, grupy towarów, składowe zestawów), `full_change.xml`, `light.xml` (lekki plik do częstych aktualizacji), plus pliki słownikowe — [IdoSell: Dokumentacja IOF](https://www.idosell.com/pl/developers/otwarte-standardy-i-api-do-integracji/internet-offer-format-iof-/dokumentacja-internet-offer-format-iof/); [IdoSell EN: Internet Offer Format](https://www.idosell.com/en/developers/otwarte-standardy-i-api-do-integracji/internet-offer-format-iof/)
- Aktualizacja stanów/cen przez IdoSell Downloader wymaga pliku CSV/XML z identyfikatorem (np. kodem producenta / ID towaru) — [Pomoc IdoSell: Aktualizacja towarów, akt. 2026-10-29](https://pomoc.idosell.com/towary/iai-downloader/aktualizacja-towarow)
- IdoSell publikuje strukturę CSV i XML dla importu klientów oraz FAQ importu danych produktów przez IAI Downloader — [IdoSell: Import danych FAQ](https://www.idosell.com/en/developers/data-import/import-of-customer-and-product-data-in-the-online-store-faq/)

### Inferences
- IOF jest „docelowym” formatem dla hurtowni współpracujących z IdoSell — generator IOF (light.xml dla cen/stanów + full.xml dla katalogu) daje przewagę nad CSV, bo obsługuje rozmiary/warianty i jest standardem rozpoznawalnym przez sprzedawców IdoSell.
- Model „hostujemy plik pod stałym URL, IdoSell pobiera go cyklicznie” pozwala dać UX zbliżony do integracji API, bez kluczy API i bez certyfikacji aplikacji.

### Gaps
- Szczegółowe nazwy elementów IOF (np. `<sizes>`, `<price gross/net>`, `<stock>`), link do XSD, limity rozmiaru pliku — strony dokumentacji IOF nie dały się zeskrapować (timeout); nie udało się potwierdzić szczegółów.
- Dokładna specyfikacja kolumn CSV dla importu towarów i obsługa wariantów w CSV — nie udało się potwierdzić.
- Limity i warunki IdoSell Admin API (rate limit, wymogi dla aplikacji) — nie udało się potwierdzić w tej sesji.

---

## A3. WooCommerce — wbudowany importer CSV i REST API

### Takeaway
WooCommerce ma najlepiej udokumentowany publicznie schemat CSV (aktualizacja dokumentacji 2026-10): warianty to wiersze `Type=variation` z kolumną `Parent`, dopasowanie po ID lub SKU, od WC 11.2 także po GTIN/EAN. Plik w pełni wystarcza dla katalogu i aktualizacji cen/stanów.

### Cited Findings
- Kolumny schematu: `ID, Type, SKU, GTIN/UPC/EAN/ISBN, Name, Published, Is featured?, Visibility in catalog, Short description, Description, Date sale price starts/ends, Tax status, Tax class, In stock?, Stock, Low stock amount, Backorders allowed?, Sold individually?, Weight, Length, Width, Height, Allow customer reviews?, Purchase note, Sale price, Regular price, Categories, Tags, Shipping class, Images, Download…, Parent, Grouped products, Upsells, Cross-sells, External URL, Button text, Position, Attribute N name / value(s) / default / visible / global` — [WooCommerce: Product CSV Importer and Exporter (akt. 2026-10-09)](https://woocommerce.com/document/product-csv-importer-exporter/)
- Warianty: wiersz rodzica `Type=variable` z pełnym zestawem wartości atrybutu (np. `Size: S, M`), wiersze dzieci `Type=variation` z unikalnym SKU, `Parent` = SKU rodzica lub `id:123`, zgodne nazwy/wartości atrybutów — [WooCommerce docs](https://woocommerce.com/document/product-csv-importer-exporter/)
- Aktualizacja: dopasowanie po ID lub SKU; od WooCommerce 11.2, gdy oba puste, po zmapowanej kolumnie GTIN/UPC/EAN/ISBN; podane ID/SKU ma pierwszeństwo bez fallbacku na GTIN — [WooCommerce docs](https://woocommerce.com/document/product-csv-importer-exporter/)
- Kodowanie UTF-8; przecinek jako separator pól; wiele wartości rozdzielane przecinkami, hierarchia kategorii przez `>` — [WooCommerce docs](https://woocommerce.com/document/product-csv-importer-exporter/)
- Zdjęcia: zewnętrzne URL są pobierane do Media Library (może się nie udać, jeśli host blokuje); importer nie ustawia alt-textów — [WooCommerce docs](https://woocommerce.com/document/product-csv-importer-exporter/)
- Limit rozmiaru pliku zależy od konfiguracji serwera (hosting) — [WooCommerce docs](https://woocommerce.com/document/product-csv-importer-exporter/)

### Inferences
- WooCommerce jest najłatwiejszym celem dla MVP „tylko plik” — kompletny, publiczny schemat, deterministyczne reguły dopasowania.
- Ceny netto/brutto: dokumentacja importera nie mówi o tym; w praktyce interpretacja `Regular price` zależy od ustawienia sklepu „ceny wprowadzane z podatkiem / bez” (wniosek, niezweryfikowany) — narzędzie powinno pytać użytkownika o tryb.

### Gaps
- Limity WooCommerce REST API (`/wp-json/wc/v3/products/batch`, maks. liczba obiektów na batch) — nie udało się potwierdzić w tej sesji.
- Czy `Regular price` jest interpretowane jako netto czy brutto w zależności od ustawień podatkowych — nie udało się potwierdzić w dokumentacji importera.

---

## A4. PrestaShop 8/9 — import CSV i Webservice

### Takeaway
PrestaShop importuje CSV/XLS/XLSX/ODS osobno dla Produktów i Kombinacji (warianty w oddzielnym pliku), domyślny separator `;`, wartości wielokrotne `,`, UTF-8; opcja „Use product reference as key” pozwala aktualizować po referencji (SKU). Format plikowy wystarcza, ale wymaga dwóch plików.

### Cited Findings
- Obsługiwane formaty: .csv, .xls, .xlsx, .xlst, .ods, .ots; encje: Categories, Products, Combinations, Customers, Addresses, Brands, Suppliers, Aliases, Store contacts (+ supply orders przy ASM) — [PrestaShop 8 docs: Import](https://docs.prestashop-project.org/v.8-documentation/user-guide/configuring-shop/advanced-parameters/import)
- Separator pól domyślnie `;`, separator wartości wielokrotnych `,`; kodowanie UTF-8 (inaczej ISO-8859-1) — [PrestaShop 8 docs](https://docs.prestashop-project.org/v.8-documentation/user-guide/configuring-shop/advanced-parameters/import)
- Opcje: „Use product reference as key”, „Force all ID numbers”, „Delete all … before import”, „Skip thumbnails regeneration”; URL zdjęć muszą być absolutne; cena w domyślnej walucie, podatek przez kolumnę Tax rule ID; pliki przykładowe w `/docs/csv_import` — [PrestaShop 8 docs](https://docs.prestashop-project.org/v.8-documentation/user-guide/configuring-shop/advanced-parameters/import)
- Kolumny pliku Kombinacji: Product ID, Product reference, `Attribute (Name:Type:Position)` (wymagane), `Value (Value:Position)` (wymagane), Supplier reference, Reference, EAN13… — [PrestaShop Specs 1.7 (starsze, ok. 2018–2020)](https://build.prestashop-project.org/prestashop-specs/1.7/back-office/advanced-parameters/import/configure-import.html); potwierdzenie w praktyce: [forum PrestaShop](https://www.prestashop.com/forums/topic/915805-import-csv-products-combinations/)

### Inferences
- Dla PrestaShop narzędzie musi generować 2 pliki (products.csv + combinations.csv) i instruować kolejność importu (najpierw produkty, potem kombinacje).
- Ceny: kolumna ceny jest typowo „tax excluded” lub „tax included” w zależności od wybranej kolumny w mapowaniu — wymaga weryfikacji na instancji (patrz Gaps).

### Gaps
- Limity rozmiaru pliku importu (zależne od `upload_max_filesize` serwera — nie potwierdzone w docs).
- Dokładny podział kolumn ceny (Price tax excluded / Price tax included) w PS 8/9 — nie udało się potwierdzić w zeskrapowanym fragmencie.
- PrestaShop Webservice API (limity, batch) — nie udało się potwierdzić w tej sesji.
- Czy PrestaShop 9 zmienił importer — nie udało się potwierdzić.

---

## A5. Allegro — wystawianie z pliku i REST API

### Takeaway
Allegro **ma** oficjalne masowe wystawianie z pliku (tylko konto firmowe): „Importuj i wystaw” (CSV/link, do 50 MB) i „Wystaw z pliku” (do 10 000 ofert, do 5 MB), z dopasowaniem do Katalogu Allegro po GTIN/EAN i obsługą danych GPSR. Plikiem można też masowo edytować istniejące oferty (cena, ilość). REST API wymaga zgód/warunków (od 23.09.2025 nowy regulamin, kary umowne 50 000 zł za udostępnianie kluczy) i limitu 20 000 nowych produktów w katalogu/miesiąc.

### Cited Findings
- Narzędzie „Importuj i wystaw” — masowe wystawianie dla kont firmowych; plik lub link do pliku, przykładowy CSV; max 50 MB. Narzędzie „Wystaw z pliku” — szablon generowany dla wybranych kategorii („Utwórz plik Allegro”), max 5 MB i do 10 000 ofert — [Allegro Pomoc: Jak wystawiać oferty z pliku](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku)
- Kluczowa kolumna GTIN (EAN), opcjonalnie MPN / ID produktu Allegro; narzędzie szuka produktów w Katalogu Allegro, przy braku tworzy propozycje produktów — [Allegro Pomoc](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku)
- Zdjęcia: URL rozdzielone `|` w kolumnie `IMAGES` lub kolumny `IMAGE1`…`IMAGE16`, pierwsze = główne, max 16 — [Allegro Pomoc](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku)
- Każda dodatkowa kolumna jest traktowana jako parametr produktu (nazwa kolumny = nazwa parametru) — [Allegro Pomoc](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku)
- Cena brutto w kolumnie `PRICE` (np. `129.99`, bez waluty); ilość w `STOCK` (brak = domyślnie 1) — [Allegro Pomoc](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku)
- Można masowo edytować istniejące oferty plikiem (cena, opis, zdjęcia, cennik dostawy, liczba sztuk) — [Allegro Pomoc](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku)
- Dane GPSR (producent, informacje o bezpieczeństwie) uzupełnia się grupowo („ustaw GPSR”) lub automatycznie (AI) albo mapuje w nowym pliku — [Allegro Pomoc](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku)
- REST API: tworzenie oferty na bazie produktu (`productSet`, `idType: GTIN`, parametry kategorii) — [Allegro Developer Portal: dokumentacja](https://developer.allegro.pl/documentation)
- Limit: każdy użytkownik może dodać do Katalogu Allegro do 20 000 produktów miesięcznie (wypowiedź pracownika Allegro, 2025-07, z linkiem do ogłoszenia); oferty mają w API pola `responsibleProducer`, `responsiblePerson`, `safetyInformation`, `marketedBeforeGPSRObligation` — [GitHub allegro/allegro-api #11793](https://github.com/allegro/allegro-api/issues/11793)
- Regulamin REST API: dostęp do części funkcji (m.in. zarządzanie ofertami) może wymagać udziału w programie partnerskim lub min. 100 użytkowników aplikacji; zakaz udostępniania kluczy osobom trzecim pod karą umowną 50 000 zł za każdy przypadek; zakaz naruszania praw autorskich, scrapingu, prezentowania ofert Allegro w serwisach konkurencyjnych; odpowiedzialność za treści spoczywa na twórcy oprogramowania; nieużywanie aplikacji 90 dni → utrata dostępu — [Allegro Developer Portal: Regulamin](https://developer.allegro.pl/rules)
- Nowy regulamin REST API obowiązuje od 23.09.2025 — [xSale (źródło wtórne)](https://xsale.ai/zmiany-w-regulaminie-allegro-rest-api-2025-co-musi-wiedziec-kazdy-wlasciciel-e-commerce/); [Shopgold](https://www.shopgold.pl/zmiany-regulaminu-allegro-rest-api-23-wrzesnia-2025-roku-n-377.html)
- Limity zapytań API (~9 000 req/min ogólnie) — [Marqetir (źródło wtórne, niezweryfikowane w oficjalnej dokumentacji)](https://marqetir.com/docs/allegro-api-guide)

### Inferences
- Allegro jest obsługiwalne plikiem w MVP: generujemy CSV w formacie „Importuj i wystaw” (GTIN, PRICE brutto, STOCK, IMAGES, kolumny parametrów). Najsłabszy punkt: brak EAN u części dostawców → produkty spoza Katalogu wymagają kompletnych parametrów kategorii.
- Integracja API z Allegro dla zewnętrznego SaaS niesie ryzyko regulaminowe (warunki autoryzacji, 100 użytkowników, kary) — dodatkowy argument, by zacząć od pliku.

### Gaps
- Oficjalna specyfikacja wszystkich kolumn pliku „Importuj i wystaw” (np. pełna lista nazw kolumn) — tylko częściowo z pomocy Allegro.
- Oficjalne limity rate-limit REST API — nie udało się potwierdzić w dokumentacji Allegro.
- Czy plik akceptuje XLSX (pomoc mówi o CSV; brief wspominał „arkusz XLSX”) — strona operuje na CSV; XLSX nie udało się potwierdzić.

---

## A6. Shopware 6 — Import/Export i Admin API

### Takeaway
Shopware 6 importuje CSV przez profile w module Ustawienia > Import/Export; warianty wymagają kilku kroków (produkty → właściwości → konfiguracja wariantów → warianty z `parent_id` i `optionIds` rozdzielonymi `|`). Plik działa, ale wymaga znajomości UUID-ów Shopware, co utrudnia „czysty” plik bez dostępu do sklepu.

### Cited Findings
- Import/eksport CSV oparty o profile; profil określa mapowanie kolumn na tabele bazy; domyślne pliki-szablony „Default product profile.csv”, „Default properties profile.csv” — [Shopware Docs: Import & Export](https://docs.shopware.com/en/shopware-en/settings/importexport)
- Import wariantów wymaga zaznaczenia „import product variants” w domyślnym profilu produktu; kroki: produkty → właściwości → (konfiguracja) → warianty — [Shopware Docs](https://docs.shopware.com/en/shopware-en/settings/importexport)
- Wiele zdjęć: trzeba zduplikować i rozszerzyć profil standardowy — [Shopware Docs](https://docs.shopware.com/en/shopware-en/settings/importexport)
- Wiersze wariantów wymagają `parent_id` (ID produktu głównego), `active`, `optionIds` (ID właściwości rozdzielone `|`) — [Firebear Studio: Shopware 6 Import Guide 2026 (źródło wtórne)](https://firebearstudio.com/blog/ultimate-guide-to-shopware-6-import.html)

### Inferences
- Shopware ma sens w drugiej fazie; dla wariantów praktycznie potrzebny jest odczyt UUID-ów ze sklepu (eksport lub Admin API) — „tylko plik” działa dobrze głównie dla aktualizacji cen/stanów po `productNumber`.

### Gaps
- Admin API (`/api/_action/sync`), limity, autoryzacja integracji — nie udało się potwierdzić w tej sesji.
- Czy profil domyślny pozwala dopasować aktualizację po `productNumber` zamiast `id` — nie udało się potwierdzić.

---

## A7. Plik vs API — co da się obsłużyć samym plikiem

### Takeaway
Samym plikiem realnie obsłużysz: **WooCommerce, PrestaShop, IdoSell (najlepiej — import z URL), Allegro (oficjalne narzędzia plikowe)**; warunkowo **Shopware** (proste produkty/aktualizacje). **Shoper** jest najsłabszy przy wariantach (wg źródła nieoficjalnego CSV ich nie obsługuje), a jego API jest mocno limitowane.

### Cited Findings
- IdoSell: import z URL, automatyczny — [Pomoc IdoSell](https://pomoc.idosell.com/towary/webowy-import-aktualizacja-i-przywracanie-towarow/import-i-aktualizacja-towarow-za-pomoca-narzedzia-webowego)
- Allegro: wystawianie i edycja ofert plikiem, do 10 000 ofert / 50 MB — [Allegro Pomoc](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku)
- WooCommerce: tworzenie i aktualizacja po ID/SKU/GTIN, warianty — [WooCommerce docs](https://woocommerce.com/document/product-csv-importer-exporter/)
- PrestaShop: produkty + kombinacje, „reference as key” — [PrestaShop 8 docs](https://docs.prestashop-project.org/v.8-documentation/user-guide/configuring-shop/advanced-parameters/import)
- Shoper: CSV bez wariantów (źródło nieoficjalne); API 10/2/s, bulk 25 — [Vinson Agency](https://vinson.agency/blog/import-produktow-do-shopera-z-pliku-csv-instrukcja-krok-po-kroku); [Shoper Developer Docs](https://developers.shoper.pl/docs/)

### Inferences
- UX „codziennej” aktualizacji cen/stanów najlepiej rozwiązać przez **hostowany feed pod stałym URL** (IdoSell natywnie; Allegro „Importuj i wystaw” przyjmuje link) zamiast API — to pozwala odłożyć integracje API.
- API będzie potrzebne dla: Shoper (warianty, częste stany), Shopware (warianty), ewentualnie WooCommerce dla automatyzacji bez ręcznego uploadu.

### Gaps
- Brak potwierdzonych informacji, czy Shoper/WooCommerce/PrestaShop natywnie (bez wtyczek) pobierają CSV cyklicznie z URL — nie udało się potwierdzić.

---

## B1. Biblioteki do parsowania Excel/CSV/XML i wykrywania kodowania

### Takeaway
W tej sesji nie zebrano źródeł pierwotnych dla bibliotek parsujących (SheetJS, openpyxl, pandas, Papa Parse, fast-xml-parser) ani detektorów kodowania. Kluczowy fakt potwierdzony w dokumentacji platform: wejście dostawców bywa w ISO-8859-1/Windows-1250, a platformy oczekują UTF-8.

### Cited Findings
- PrestaShop wymaga UTF-8 (alternatywnie ISO-8859-1) — [PrestaShop 8 docs](https://docs.prestashop-project.org/v.8-documentation/user-guide/configuring-shop/advanced-parameters/import)
- WooCommerce wymaga UTF-8 — [WooCommerce docs](https://woocommerce.com/document/product-csv-importer-exporter/)
- Shoper oczekuje UTF-8 — [Vinson Agency](https://vinson.agency/blog/import-produktow-do-shopera-z-pliku-csv-instrukcja-krok-po-kroku)
- LlamaParse rozlicza arkusze kalkulacyjne „1 credit per sheet” (czyli parsowanie XLSX przez usługę jest możliwe, ale niepotrzebne dla czystych arkuszy) — [LlamaParse docs: Pricing](https://developers.llamaindex.ai/llamaparse/general/pricing/)

### Inferences
- (Niezweryfikowane w tej sesji, wiedza ogólna) Typowy stos: Python — pandas + openpyxl (XLSX), xlrd (stary XLS), lxml (XML), charset-normalizer/chardet (kodowanie); JS — SheetJS, Papa Parse, fast-xml-parser, jschardet. Heurystyka dla polskich plików: jeśli nie UTF-8, sprawdzić Windows-1250 vs ISO-8859-2 po częstości znaków „ą, ś, ź” (różnią się kodami w tych dwóch stronach kodowych).
- Deterministyczny parser + walidacja wyjścia zawsze przed LLM; LLM tylko dla mapowania i trudnych PDF.

### Gaps
- Licencje i aktualne wersje SheetJS (CDN vs npm, licencja Community), wydajność na dużych plikach — nie udało się potwierdzić w tej sesji.
- Porównanie dokładności detektorów kodowania dla Windows-1250 vs ISO-8859-2 — nie znaleziono źródła.

---

## B2. Ekstrakcja tabel z PDF — narzędzia, dokładność, koszt

### Takeaway
Dla PDF cenników: open-source **Docling** wygrywa w benchmarkach tabel z klasycznymi bibliotekami (pdfplumber, Camelot); usługi chmurowe kosztują ok. **$1.5–$15 / 1000 stron** (Mistral OCR 4: $4, batch $2; Azure Layout $10; Textract Tables $15; LlamaParse od ~$1.25 za 1000 kredytów, 1–4+ kredytów/strona). Natywne PDF w LLM (Gemini: 258 tokenów/stronę) są tanie, ale gorzej odwzorowują strukturę tabel niż wyspecjalizowane modele.

### Cited Findings
- Benchmark tabel z PDF (arXiv 2511.16134, 2025): Docling F1(TEDS) 0.85 na PubTables, 0.94 na ICDAR-2013; pdfplumber 0.19 / 0.38; Camelot 0.20 / 0.50; Gemini 2.5 Pro 0.75 / 0.74; GPT-4.1 0.56 / 0.79 — [arXiv: Benchmarking Table Extraction from Heterogeneous Scientific PDF Documents](https://arxiv.org/html/2511.16134v2)
- Benchmark Procycons (2025-03): Docling 97,9% dokładności komórek w złożonych tabelach; LlamaParse szybki (~6 s/dokument), słabszy przy złożonych tabelach; Unstructured 100% na prostych, 75% na złożonych, najwolniejszy — [Procycons: PDF Data Extraction Benchmark 2025](https://procycons.com/en/blogs/pdf-data-extraction-benchmark/)
- Test praktyka: Docling miał problemy ze scalonymi komórkami; pdfplumber dobry jako niskopoziomowy ekstraktor, ale słaby przy cieniowanych komórkach; TableFormer (Docling) 93,6% vs Tabula 67,9% i Camelot 73,0% na bankach tabel — [Medium, M. Kramer (opinia)](https://medium.com/@kramermark/i-tested-12-best-in-class-pdf-table-extraction-tools-and-the-results-were-appalling-f8a9991d972e)
- pdfplumber vs Camelot vs tabula: Camelot lattice dobry dla tabel z ramkami, słaby dla bezramkowych; tabula wymaga JRE — [InvoiceDataExtraction (źródło wtórne)](https://invoicedataextraction.com/blog/python-pdf-table-extraction-invoices)
- **Mistral OCR 4**: $4 / 1000 stron, Batch API $2 / 1000; Document AI (schemat JSON) $5 / 1000 — [Mistral: OCR 4](https://mistral.ai/news/ocr-4/); OCR 4.1: $4 / 1000 stron (cached $0.4) — [Mistral docs: API pricing](https://docs.mistral.ai/inference/pricing)
- **Azure Document Intelligence**: Read $1.50 / 1000 stron (0–1M), prebuilt (w tym Layout) $10 / 1000, custom extraction $30 / 1000 — [Azure pricing](https://azure.microsoft.com/en-us/pricing/details/document-intelligence/)
- **AWS Textract**: Analyze Document – Tables $0.015/stronę ($15/1000) do 1M stron, $0.010 powyżej; Tables+Queries $0.020; free tier 100 stron/mies. dla Tables — [AWS Textract pricing](https://aws.amazon.com/textract/pricing/); free tier: [Cloudtech (wtórne)](https://cloudtech.com/resources/aws-textract-pricing-usage-insights)
- **LlamaParse**: $1.25–1.5 za 1000 kredytów; parsowanie od 1 kredytu/stronę, layout extraction +3 kredyty/stronę; 10 000 darmowych kredytów/mies.; Starter $50 / 40 000 kredytów — [LlamaParse docs: Pricing](https://developers.llamaindex.ai/llamaparse/general/pricing/); [LlamaIndex pricing](https://www.llamaindex.ai/pricing); [Extend (wtórne)](https://www.extend.ai/resources/llamaparse-review-features-pricing-alternatives)
- **Gemini API**: każda strona dokumentu = 258 tokenów; PDF rozliczany jak obraz — [Google AI Studio: Document understanding](https://aistudio.google.com/docs/document-processing); [Google Cloud pricing](https://cloud.google.com/model-garden/pricing)
- **Claude**: PDF jako blok `document` (base64 lub Files API); limit 32 MB na żądanie, 600 stron (100 dla modeli z kontekstem 200k) — [Claude docs: PDF support](https://platform.claude.com/docs/en/build-with-claude/pdf-support) (dane z dokumentacji skillu claude-api, cache 2026-10)

### Inferences
- Rekomendowany pipeline PDF: (1) jeśli PDF ma warstwę tekstową — pdfplumber/Docling lokalnie (koszt ~0); (2) skan lub nieudana ekstrakcja — Mistral OCR ($0.002–0.004/stronę) lub LLM z natywnym PDF; (3) zawsze walidacja (sumy, typy, liczba wierszy) i podgląd dla użytkownika.
- 20-stronicowy cennik: Mistral OCR ≈ $0.08 (batch $0.04); Azure Layout ≈ $0.20; Textract Tables ≈ $0.30.

### Gaps
- Brak benchmarku specyficznie dla cenników hurtowych/katalogów (polskie znaki, scalone komórki, wielostronicowe tabele) — nie znaleziono.
- Dokładna liczba tokenów na stronę PDF w Claude (dokumentacja historycznie podawała ~1 500–3 000 tokenów tekstu/stronę + obraz) — nie udało się potwierdzić na stronie w tej sesji.
- Unstructured (cennik API) — nie zebrano.

---

## B3. LLM do mapowania kolumn — podejście, koszt, badania

### Takeaway
Rekomendowany wzorzec: LLM proponuje mapowanie (nagłówki + kilkanaście wierszy próbki → JSON wg schematu, structured outputs), a transformację wykonuje deterministyczny kod; mapowanie zapisuje się per dostawca. Koszt pojedynczego mapowania jest pomijalny (Haiku 5.5 ≈ $0.001, Sonnet 5.5 ≈ $0.02). Badania 2025 pokazują, że metody LLM przewyższają podobieństwo wektorowe w schema matching, ale nie znaleziono benchmarku dla katalogów produktowych.

### Cited Findings
- Aktualne ceny Claude API (cache 2026-10-06): Haiku 5.5 `claude-haiku-5-5` $0.10 / $0.50 za 1M tokenów in/out (do 100K tokenów promptu; powyżej $0.50/$2.50); Sonnet 5.5 `claude-sonnet-5-5` $2 / $10; Opus 5.5 `claude-opus-5-5` $4 / $20; Haiku 4.5 $1 / $5 — [Claude docs: Pricing](https://platform.claude.com/docs/en/about-claude/pricing) (strona nie zwróciła treści przy scrapowaniu; dane z oficjalnego skillu claude-api, cache 2026-10-06)
- Message Batches: przetwarzanie asynchroniczne za 50% ceny — [Claude docs: Batch processing](https://platform.claude.com/docs/en/build-with-claude/batch-processing) (dane ze skillu claude-api)
- Structured outputs: `output_config.format` (JSON schema) lub `strict: true` na narzędziach gwarantują zgodność ze schematem — [Claude docs: Structured outputs](https://platform.claude.com/docs/en/build-with-claude/structured-outputs) (dane ze skillu claude-api)
- Haiku 5.5 ma domyślnie włączone myślenie adaptacyjne (effort domyślnie `medium`); tokeny myślenia liczą się jako output — [Claude docs: Pricing](https://platform.claude.com/docs/en/about-claude/pricing) (dane ze skillu claude-api)
- LLMatch (arXiv 2507.10897, 2025): metody LLM (ReMatch, LLMatch) utrzymują wysoką skuteczność zarówno w prostym, jak i złożonym schema matching; selekcja tabel przez LLM (gpt-4o-mini) konsekwentnie lepsza niż podobieństwo wektorowe — [arXiv: LLMATCH](https://arxiv.org/html/2507.10897v1)
- Magneto (PVLDB vol. 18, 2025): łączenie małych i dużych modeli językowych w celu wysokiej dokładności schema matching przy niskim koszcie — [VLDB: Magneto](https://www.vldb.org/pvldb/vol18/p2681-freire.pdf)
- „Towards Scalable Schema Mapping using LLMs” (ACM 2025): problemy spójności/odporności odpowiedzi LLM; agregacja wielu odpowiedzi (set operations) i ocena pewności (MatchMaker) poprawiają skuteczność; brak próbek wartości utrudnia zadanie — [ACM DL](https://dl.acm.org/doi/full/10.1145/3737412.3743490)

### Inferences
- Szacunek kosztu jednego mapowania (nagłówki + 20 wierszy ≈ 5 000 tokenów in, ≈ 1 000 out, bez dużego myślenia): Haiku 5.5 ≈ $0.0005 + $0.0005 ≈ **$0.001**; Sonnet 5.5 ≈ $0.01 + $0.01 ≈ **$0.02**; Opus 5.5 ≈ **$0.04**. Przy myśleniu na effort `low` koszt rośnie umiarkowanie.
- Ekstrakcja całego 10-stronicowego PDF przez LLM (≈25k in, ≈15k out — założenie): Haiku 5.5 ≈ $0.01, Sonnet 5.5 ≈ $0.20 — droższe od Mistral OCR ($0.04), więc LLM lepiej używać do mapowania i normalizacji, a nie do OCR.
- Na podstawie literatury: dawać LLM próbki wartości (nie tylko nagłówki), prosić o pewność per pole, a niepewne mapowania pokazywać do potwierdzenia; „pamięć” mapowania per dostawca + diff eliminuje powtórne koszty.
- Normalizację rozmiarów/jednostek/netto-brutto (np. „23%”, „szt.”) lepiej robić regułami w kodzie, z LLM jako fallbackiem.

### Gaps
- Brak publicznego benchmarku dokładności LLM dla mapowania kolumn cenników hurtowych → formatów platform e-commerce; liczbowe wyniki F1 z LLMatch/Magneto nie zostały wyciągnięte w tej sesji.
- Ceny alternatyw (OpenAI, Gemini Flash per 1M tokenów) — nie potwierdzono dokładnych stawek w tej sesji.

---

## C1. Prawo autorskie i prawo sui generis do baz danych — zdjęcia i opisy dostawców

### Takeaway
Profesjonalne zdjęcia i kreatywne opisy producentów są zwykle utworami (art. 1 pr. aut.); sam zakup towaru w hurcie **nie daje licencji** na ich publikację — potrzebna zgoda (najlepiej pisemna). Proste „packshoty” mogą nie być utworami (orzecznictwo). Odpowiedzialność za publikację spoczywa przede wszystkim na sprzedawcy; narzędzie powinno to jasno komunikować w regulaminie i nie pobierać/hostować zdjęć bez potrzeby.

### Cited Findings
- Przedmiotem prawa autorskiego jest każdy przejaw działalności twórczej o indywidualnym charakterze (art. 1 pr. aut.); twórcy przysługuje wyłączne prawo korzystania (art. 17); legalny zakup towaru nie uprawnia do kopiowania zdjęć i opisów producenta — przykład sprawy klienta kancelarii — [Kancelaria Lech: Zdjęcia i opisy produktów od producenta](https://znakitowarowe-blog.pl/zdjecia-i-opisy-produktow-od-producenta/)
- SN, wyrok z 20.01.2006 (I CK 281/05): utworem może być kombinacja danych powszechnie dostępnych, jeśli wybór, segregacja i sposób przedstawienia są oryginalne (tabela danych technicznych może być chroniona) — [Kancelaria Lech](https://znakitowarowe-blog.pl/zdjecia-i-opisy-produktow-od-producenta/)
- Kopiowanie cudzych zdjęć/opisów bez licencji jest nielegalne; producenci często udostępniają materiały marketingowe partnerom — należy sprawdzić zakres zgody i uzyskać ją na piśmie — [Trusted Shops (2018, starsze)](https://business.trustedshops.pl/blog/zdjecia-opisy-produktow-prawa-autorskie/)
- Packshot będący prostym odwzorowaniem wyglądu przedmiotu nie jest utworem (omówienie wyroku) — [Lege Artis (2019, starsze)](https://czasopismo.legeartis.org/2019/11/prawa-autorskie-zdjec-produktow-fotografia-packshot-utwor-wyrok/)
- Regulamin Allegro REST API zakazuje wykorzystywania oprogramowania do naruszania praw autorskich i praw do znaków towarowych; odpowiedzialność za treści spoczywa na twórcy oprogramowania REST API — [Allegro Developer Portal: Regulamin](https://developer.allegro.pl/rules)
- Dyrektywa 96/9/WE (ochrona prawna baz danych, prawo sui generis dla twórcy bazy, który poniósł istotną inwestycję) — [EUR-Lex: Dyrektywa 96/9/WE](https://eur-lex.europa.eu/eli/dir/1996/9/oj) (akt 1996; treść nie była analizowana w tej sesji)

### Inferences
- Katalog dostawcy (plik z tysiącami pozycji) może być bazą danych chronioną sui generis; użytkownik, który otrzymał plik od dostawcy w ramach współpracy, ma zwykle dorozumianą zgodę na wykorzystanie danych do sprzedaży — ale zakres (np. publikacja opisów 1:1, zdjęcia) zależy od umowy dystrybucyjnej. To ryzyko sprzedawcy, nie narzędzia, o ile narzędzie tylko przetwarza plik na zlecenie użytkownika.
- Narzędzie powinno: (a) w regulaminie przenieść odpowiedzialność za prawa do treści na użytkownika, (b) przekazywać URL zdjęć zamiast kopiować je na własne serwery (mniejsza ekspozycja), (c) ewentualnie oferować „przepisanie opisu” przez LLM (ale to nie usuwa praw do zdjęć).

### Gaps
- Brak potwierdzonego orzecznictwa dot. odpowiedzialności dostawcy narzędzia SaaS (pośrednika) za naruszenia użytkownika w kontekście konwersji plików — nie znaleziono.
- Konkretne przepisy polskiej ustawy o ochronie baz danych (2001) — nie analizowano w tej sesji.

---

## C2. RODO — dane osobowe w cennikach, umowa powierzenia, hosting w UE

### Takeaway
Cenniki i katalogi produktowe co do zasady nie zawierają danych osobowych; mogą się pojawić dane kontaktowe handlowców/osób odpowiedzialnych (np. jednoosobowa działalność jako producent w polach GPSR). Mimo to SaaS przetwarzający pliki klientów powinien mieć gotową umowę powierzenia (art. 28 RODO) i preferować hosting w UE — w tej sesji nie zebrano źródeł UODO na ten temat.

### Cited Findings
- Dane GPSR wymagane w ofercie obejmują nazwę i adres (pocztowy i elektroniczny) producenta / osoby odpowiedzialnej — mogą to być dane osoby fizycznej prowadzącej działalność — [Komisja Europejska: wytyczne GPSR, EUR-Lex C/2025/6233](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=OJ:C_202506233)
- Rozporządzenie (UE) 2016/679 (RODO), art. 28 — wymóg umowy z podmiotem przetwarzającym — [EUR-Lex: RODO](https://eur-lex.europa.eu/eli/reg/2016/679/oj) (treść nie analizowana w tej sesji)
- Regulamin Allegro REST API wymaga od twórców oprogramowania podania użytkownikom rzetelnej informacji o polityce bezpieczeństwa danych — [Allegro Developer Portal: Regulamin](https://developer.allegro.pl/rules)

### Inferences
- Minimalny pakiet prawny MVP: regulamin + polityka prywatności + wzór DPA (umowy powierzenia) do akceptacji przy rejestracji; hosting i dostawcy LLM z przetwarzaniem w UE lub z SCC (np. opcja `inference_geo` w Claude API — wymaga weryfikacji dostępności regionu UE).
- Dostawcy LLM/OCR są dalszymi podmiotami przetwarzającymi — trzeba ich wymienić w DPA.

### Gaps
- Stanowisko UODO dot. danych B2B w cennikach — nie znaleziono w tej sesji.
- Dostępność przetwarzania w regionie UE dla Claude/Mistral/Gemini oraz warunki ZDR — nie udało się potwierdzić.

---

## C3. Regulaminy platform, DSA i GPSR — znaczenie dla plików importu

### Takeaway
GPSR (rozporządzenie 2023/988, stosowane od 13.12.2024) wymaga, by oferta online zawierała m.in. nazwę/adres producenta (i osoby odpowiedzialnej w UE, gdy producent spoza UE), identyfikację produktu i ostrzeżenia/informacje o bezpieczeństwie. Dlatego plik wyjściowy powinien mieć pola „producent”, „adres producenta”, „osoba odpowiedzialna”, „informacje o bezpieczeństwie” — Allegro już ma je w API i narzędziu plikowym.

### Cited Findings
- GPSR stosuje się od 13 grudnia 2024; ustanawia ogólny wymóg bezpieczeństwa produktów niezależnie od kanału sprzedaży — [Komisja Europejska: wytyczne GPSR, EUR-Lex C/2025/6233](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=OJ:C_202506233)
- Oferta online musi wskazywać m.in. — jeśli producent nie ma siedziby w UE — nazwę, adres pocztowy i elektroniczny osoby odpowiedzialnej (art. 16(1) GPSR / art. 4(1) rozp. 2019/1020) — [EUR-Lex C/2025/6233](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=OJ:C_202506233)
- Art. 19 GPSR: każda oferta online podaje producenta i osobę odpowiedzialną oraz informacje identyfikujące produkt i ostrzeżenia — [EU-Representa (źródło wtórne)](https://eu-representa.com/insights/gpsr-compliance-checklist); [EaseCert (wtórne)](https://easecert.com/blogs/insights/labelling-requirements-for-gpsr-compliance)
- Allegro: w ofertach API pola `responsibleProducer`, `responsiblePerson`, `safetyInformation`, `marketedBeforeGPSRObligation` — [GitHub allegro-api #11793](https://github.com/allegro/allegro-api/issues/11793); w pliku/na liście produktów opcja „ustaw GPSR” i automatyczne uzupełnianie przez AI — [Allegro Pomoc](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku)
- Regulamin Allegro REST API (od 23.09.2025): warunki autoryzacji oprogramowania, kara 50 000 zł za udostępnianie kluczy, zakaz scrapingu i prezentowania ofert w serwisach konkurencyjnych — [Allegro Developer Portal: Regulamin](https://developer.allegro.pl/rules)

### Inferences
- Funkcja „uzupełnij dane GPSR per producent” (zapamiętana w profilu dostawcy, jak mapowanie) to konkretna, prawnie uzasadniona wartość dodana narzędzia.
- DSA: obowiązki DSA dotyczą głównie platform/marketplace'ów (Allegro), nie narzędzia konwersji — nie zebrano źródeł, traktować jako niezweryfikowane.

### Gaps
- Pełny tekst art. 19 GPSR z EUR-Lex (rozporządzenie 2023/988) — nie pobrano bezpośrednio; oparto się na wytycznych KE i źródłach wtórnych.
- Wytyczne UOKiK dot. GPSR — nie znaleziono w tej sesji.
- Regulaminy API Shoper/IdoSell (warunki AppStore/partnerskie) — nie udało się potwierdzić.

---

## C4. Omnibus — najniższa cena z 30 dni

### Takeaway
Przy każdej informacji o obniżce sklep musi pokazać najniższą cenę z 30 dni przed obniżką, a wielkość obniżki liczyć od niej; UOKiK aktywnie karze (2026: Zalando, Temu). Narzędzie, które masowo zmienia ceny z cennika dostawcy, powinno przechowywać historię cen i/lub generować pole „najniższa cena z 30 dni” (Shoper ma taką kolumnę w CSV).

### Cited Findings
- Obowiązek podania najniższej ceny z 30 dni przed obniżką w tym samym miejscu i czasie co informacja o obniżce; okres odniesienia 30 dni; wielkość obniżki liczona od tej ceny; nie można stosować innych określeń typu „cena referencyjna” — [UOKiK: Wyjaśnienia Prezesa UOKiK – Informacja o obniżce ceny (PDF)](https://uokik.gov.pl/storage/archiwum/e6e552a1.pdf); [JD Supra](https://www.jdsupra.com/legalnews/dyrektywa-omnibus-wyjasnienia-uokik-7274220/)
- Kary/zarzuty UOKiK m.in. dla Zalando i Temu (styczeń 2026), H&M, Peek & Cloppenburg, Black Red White — [UOKiK: tag Dyrektywa Omnibus](https://uokik.gov.pl/tag/dyrektywa-omnibus)
- Zalecenie dokumentowania historii cen na wypadek kontroli — [Profisoft (wtórne)](https://e-commerce.profisoft.pl/blog/falszywe-promocje-na-celowniku-uokik/)
- CSV Shopera zawiera pole najniższej ceny z 30 dni — [Vinson Agency](https://vinson.agency/blog/import-produktow-do-shopera-z-pliku-csv-instrukcja-krok-po-kroku)

### Inferences
- Zwykła zmiana ceny regularnej (podwyżka/obniżka cennika dostawcy bez komunikowania promocji) nie wymaga informacji Omnibus; obowiązek powstaje, gdy sklep komunikuje obniżkę (przekreślona cena, „-20%”). Diff „przed/po” w narzędziu + archiwum cen to naturalne wsparcie zgodności.
- Ryzyko: jeśli narzędzie ustawi „cenę promocyjną” z pola dostawcy, użytkownik musi mieć poprawną najniższą cenę z 30 dni — warto ostrzegać.

### Gaps
- Czy platformy (WooCommerce, PrestaShop, IdoSell, Shopware) liczą najniższą cenę z 30 dni automatycznie, czy wymagają pola w imporcie — nie udało się potwierdzić.

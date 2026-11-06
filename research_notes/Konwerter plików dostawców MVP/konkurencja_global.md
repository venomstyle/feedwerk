# Konkurencja międzynarodowa: narzędzia do importu cenników i katalogów dostawców do sklepów

Stan na: 2026-11-06. Strony sprawdzone w listopadzie 2026, chyba że zaznaczono inaczej. Daty względne z wordpress.org ("8 months ago") przeliczono w przybliżeniu względem listopada 2026.
Legenda kolumn porównania: **Dowolny plik** = obsługuje plik dowolnego dostawcy z własnym mapowaniem (a nie tylko predefiniowanych dostawców); **PDF**; **AI**; **Mapowanie pamiętane per dostawca**; **Diff** = pokazuje zmiany względem poprzedniego pliku.

---

## P1. Ogólne SaaS-y workflow / przetwarzania danych (Parabola, Eofferix)

### Takeaway
Parabola (w 2026 przemianowana na "Prowork by Parabola") ma najbliższy naszemu pomysłowi gotowy szablon: e-mail → parsowanie CSV/Excel/PDF z AI → dopasowanie SKU → diff z poprzednią wersją → wypchnięcie do ERP. Jest jednak skierowana do zespołów zakupowych i ERP (NetSuite, Fulfil), nie do sklepów SMB. Płatny plan self-serve kosztuje ok. $400/mies. Eofferix to platforma do przetwarzania katalogów z zapisanymi profilami. Jej cennika nie udało się potwierdzić.

### Cited Findings

**Parabola / Prowork by Parabola**
- Oficjalny cennik (2026) nie podaje kwot. Plan Self-Serve/Basic: "1 user, 1,000 credits, and limited AI", darmowy bezterminowo, z dokupowaniem kredytów pay-as-you-go. Plan Business ma cenę ustalaną ze sprzedażą (SSO, SOC 2, SLA, proof of concept na danych produkcyjnych). Kredyty zużywają się przy uruchomieniach, a "multi-page PDF extraction" kosztuje więcej kredytów. — [Parabola Pricing](https://parabola.io/pricing)
- Według serwisu zewnętrznego (stan "as of July 2026", aktualizacja 28.09.2026): Basic jest darmowy (1,000 kredytów/mies.), Collaborator kosztuje $400/mies. flat (do 3 użytkowników, 30,000 kredytów/mies.), Business ma cenę indywidualną. Stare plany wierszowe Plus (~$80) i Advanced (~$350) zniknęły. Od września 2026 produkt występuje jako "Prowork by Parabola". Kwot nie udało się potwierdzić na stronie Parabola. — [Automation Atlas](https://automationatlas.io/answers/parabola-pricing-explained-2026/)
- Szablon "Vendor price list import" ma 7 kroków: obserwacja skrzynki e-mail z załącznikami, parsowanie CSV/Excel/PDF (krok AI obsługuje formaty specyficzne dla dostawcy i nietypowe nagłówki), normalizacja pól (kod, opis, cena jednostkowa, waluta, data obowiązywania, MOQ), dopasowanie kodu dostawcy do wewnętrznego SKU (niedopasowane wiersze trafiają do kolejki review), **porównanie z poprzednią wersją cennika** (delty w $ i %, flagi: zmiana ceny, nowe pozycje, wycofane pozycje), wypchnięcie do ERP przez API lub staging do akceptacji, e-mail z podsumowaniem zmian do kupca. Strona podaje, że tabele PDF w większości przypadków ekstrahują się poprawnie, a wiersze o niskiej pewności idą do przeglądu. Jako cele wymienia ERP NetSuite i Fulfil. Shopify ani WooCommerce nie są wymienione. — [Parabola use case: vendor price list import](https://parabola.io/use-cases/vendor-price-list-import)
- Na stronie Parabola pojawia się marka "Prowork Table" (staging zmian do akceptacji). — [Parabola use case](https://parabola.io/use-cases/vendor-price-list-import)
- G2: 4.9/5 z 51 recenzji. Najczęstsza krytyka to uciążliwa, sztywna struktura kroków (5 recenzji). Cena nie jest wśród głównych zarzutów na G2. — [G2 Parabola](https://www.g2.com/products/parabola) (dane ze snippetu wyszukiwarki, strony nie pobrano w całości)
- Na forum społeczności Parabola, przy zmianie cennika, klienci zgłaszali obawy, że model będzie "unpredictable and expensive as they scale" i niezrozumiały. Jeden użytkownik pytał, czy dzienny flow za 4 kredyty ma kosztować $1,000/rok. Parabola odpowiedziała ofertą planów indywidualnych. — [Parabola Community: Pricing Update](https://community.parabola.io/t/parabola-pricing-update/1660) (data wątku nie została potwierdzona)
- Według Automation Atlas Parabola działa wyłącznie w chmurze, a często uruchamiane flow szybko zużywają kredyty. — [Automation Atlas](https://automationatlas.io/answers/parabola-pricing-explained-2026/)

**Eofferix**
- Eofferix opisuje się jako "Catalog & data processing platform": konwersja formatów, łączenie katalogów z wielu źródeł, dystrybucja danych do partnerów. — [eofferix.com](https://eofferix.com/) (snippet wyszukiwarki; strona zwracała 503 przy pobieraniu)
- Według dokumentacji przyjmuje CSV, XLS, XLSX, XLSM oraz ZIP z plikiem tabelarycznym. Plik może przyjść jako załącznik e-mail, z Google Sheets lub Drive albo z API dostawcy. — [Eofferix docs: CSV/XLSX price list](https://eofferix.com/docs/import-csv-xlsx-price-list)
- Ma osobną instrukcję dla katalogów XML dostawców. — [Eofferix docs: XML catalog](https://eofferix.com/docs/import-xml-catalog)
- Mapowanie pól dostawcy na model Eofferix obejmuje nazwy kolumn, typy danych, formuły i pola wymagane. — [Eofferix docs: mapping fields](https://eofferix.com/docs/mapping-fields)
- Do pracy cyklicznej zaleca zapisane profile przetwarzania, które powtarzają te same transformacje i mogą działać według harmonogramu. Case study pokazuje wyciąganie ceny regexem z pola z prefiksem waluty. — [Eofferix case: prepare vendor price list](https://eofferix.com/cases/prepare-vendor-price-list-for-import)
- Główny opisany kanał wyjścia to Ozon (rosyjski marketplace): łączenie cenników wielu dostawców w jeden katalog i eksport na Ozon. — [Eofferix: price list to Ozon](https://eofferix.com/price-list-to-ozon)

### Inferences
- Parabola udowadnia, że workflow "plik od dostawcy → AI parsing → dopasowanie → diff → akceptacja" jest wartościowy i da się go sprzedawać. Przy ~$400/mies. za plan płatny i nastawieniu na ERP/procurement nie jest to jednak oferta dla małego sklepu na WooCommerce czy Shoperze. To potencjalna luka cenowa.
- Eofferix wygląda na produkt z kręgu rosyjskojęzycznego (Ozon), co ogranicza jego bezpośrednią konkurencyjność na rynku PL/UE. To wniosek, nie fakt potwierdzony.

### Gaps
- Cennika Eofferix nie udało się potwierdzić: /pricing i strona główna zwracały 503, a Firecrawl zwrócił błąd proxy.
- Nie udało się potwierdzić, czy Eofferix obsługuje PDF, używa AI, pokazuje diff, ani kto za nim stoi i w jakim kraju.
- Oficjalnej ceny planu Collaborator ($400) nie udało się potwierdzić na stronie Parabola.
- Nie znaleziono recenzji Parabola na Capterra ani Trustpilot.

---

## P2. Wtyczki WooCommerce (WP All Import, WebToffee, WP Desk, EmberPrice)

### Takeaway
WooCommerce ma dojrzałe, tanie importery (WP All Import, WebToffee), które obsłużą dowolny CSV/XML/Excel z ręcznym mapowaniem i zapisanym szablonem. Nie czytają jednak PDF, nie używają AI do mapowania i nie pokazują przejrzystego diffu cenowego. Głównym źródłem frustracji w recenzjach jest paywall (np. import do WooCommerce lub produktów wariantowych tylko w płatnej wersji) i trudny UX. Najbliższym koncepcyjnie konkurentem jest nowy EmberPrice (lipiec 2026: mapowanie per dostawca, podgląd stara/nowa cena, rollback), ale ma <10 instalacji i nie obsługuje PDF ani AI.

### Cited Findings

**WP All Import (+ WooCommerce Import Add-On), Soflyy**
- Główna wtyczka: 100,000+ aktywnych instalacji, ocena 4.7/5 z 1,966 recenzji (1,794 × 5★, 120 × 1★), wersja 4.1.4, aktualizacja październik 2026. Obsługuje XML, CSV (własne separatory), XLS/XLSX, TSV, Google Sheets (przez publiczny URL), ZIP, a nieoficjalnie także JSON i SQL. Pro dodaje import z URL, cykliczne importy cron, własne funkcje PHP, obrazy i custom fields. — [wordpress.org: WP All Import](https://wordpress.org/plugins/wp-all-import/)
- Osobna darmowa wtyczka "WP All Import – Product Import for WooCommerce" ma 20,000+ instalacji i ocenę 4.7/5 z 276 recenzji (19 × 1★), aktualizacja październik 2026. Wersja darmowa importuje produkty z XML/CSV/Excel/Google Sheets z mapowaniem drag-and-drop. Pro dodaje pełną obsługę produktów wariantowych, import z URL i cykliczne importy (cron). — [wordpress.org: Product Import for WooCommerce](https://wordpress.org/plugins/woocommerce-xml-csv-product-import/)
- Ceny (rocznie, z "promocyjnymi" przekreśleniami): WooCommerce Import Package $169/rok, Import Pro Package $199/rok, Import+Export Pro $299/rok, Professional $299/rok (z WooCommerce i synchronizacją stanów/cen), Developer $149/rok (bez WooCommerce), Lifetime $1,299 jednorazowo (na stronie miejscami $1,399). Wszystkie pakiety: "unlimited installs", 90-dniowa gwarancja zwrotu. Po wygaśnięciu subskrypcji wtyczka działa dalej, ale bez aktualizacji i wsparcia. Strona jednocześnie zapowiada koniec licencji lifetime. — [WP All Import Pricing](https://www.wpallimport.com/pricing/)
- WP All Import nie obsługuje PDF ani AI. Na stronach nie ma ani wzmianki o PDF lub AI, ani o diffie cen: lista formatów to XML/CSV/Excel/TSV/Sheets/ZIP/JSON/SQL. — [wordpress.org: WP All Import](https://wordpress.org/plugins/wp-all-import/)
- Tematy recenzji 1★ (parafrazy): darmowa wersja jest bezużyteczna bez premium (ok. marzec 2026: ["Useless without a premium account"](https://wordpress.org/support/topic/useless-without-a-premium-account/); ok. listopad 2025: ["The free version is a complete waste of time"](https://wordpress.org/support/topic/the-free-version-is-a-complete-waste-of-time/)); złe wsparcie i UX (ok. grudzień 2025: ["Terrible Support and Terrible UX"](https://wordpress.org/support/topic/terrible-support-and-terrible-ux/)); poczucie wprowadzenia w błąd, że import do Woo jest płatny (ok. 2025: ["Total scam have to pay for Woo"](https://wordpress.org/support/topic/total-scam-have-to-pay-for-woo/), ok. 2023: ["The WooCommerce Add-On is Required to Import Products"](https://wordpress.org/support/topic/the-woocommerce-add-on-is-required-to-import-products/)); Pro dobrze działa tylko dla świeżych danych, a gorzej przy aktualizacjach (ok. 2023: ["Got the pro version, only works well for fresh data"](https://wordpress.org/support/topic/got-the-pro-version-only-works-well-for-fresh-data/)); funkcja "skip unchanged data" przeniesiona do płatnej wersji (ok. 2022: [wątek](https://wordpress.org/support/topic/skip-unchanged-data-was-once-a-free-feature/)). — [wordpress.org: WP All Import 1★ reviews](https://wordpress.org/support/plugin/wp-all-import/reviews/?filter=1)
- G2: 4.3/5, ale z bardzo małej próby (ok. 11 recenzji). Liczba ze snippetu wyszukiwarki jest niespójna. — [G2 WP All Import](https://g2.com/products/wp-all-import/reviews/wp-all-import-review-1596786). Profil Capterra istnieje, ale ocen nie udało się odczytać. — [Capterra UK](https://www.capterra.co.uk/software/1017728/wp-all-import)

**Product Import Export for WooCommerce, WebToffee**
- Wersja darmowa: 80,000+ instalacji, 4.6/5 z 414 recenzji (24 × 1★), wersja 2.6.8 (changelog 2026-10-26). Darmowa obsługuje tylko CSV i produkty proste, grupowe i zewnętrzne, **bez wariantowych**. Pozwala zapisać konfigurację importu jako szablon. — [wordpress.org: Product Import Export for WooCommerce](https://wordpress.org/plugins/product-import-export-for-woo/)
- Premium: $69/rok (1 strona), $129/rok (do 5 stron), $249/rok (do 25 stron), z autoodnowieniem i 30-dniową gwarancją zwrotu, bez wersji trial. Obsługuje CSV, XML, TSV, Excel i Google Sheets z pliku lokalnego, URL lub FTP. Pozwala zapisać mapowanie kolumn jako szablon ("save it as a template"). Ma harmonogram przez FTP/SFTP i cron. PDF nie jest wspomniany. Ocena na stronie producenta 4.85 z 238 recenzji. — [WebToffee: Product Import Export Plugin](https://www.webtoffee.com/product/product-import-export-woocommerce/)
- Tematy recenzji 1★ (parafrazy): bezużyteczna bez płacenia (ok. maj 2026: ["Useles without paying"](https://wordpress.org/support/topic/useles-without-paying/)); brak eksportu produktów wariantowych w wersji darmowej (ok. 2024: [wątek](https://wordpress.org/support/topic/cant-export-variable-products/)); zepsuta strona i słabe wsparcie (ok. 2023: ["Broke our site, desperate support"](https://wordpress.org/support/topic/broke-our-site-desperate-support/)); import nie jest wcale prostszy (ok. 2023: [wątek](https://wordpress.org/support/topic/does-not-make-the-import-of-data-any-easier/)). — [wordpress.org: WebToffee 1★ reviews](https://wordpress.org/support/plugin/product-import-export-for-woo/reviews/?filter=1)

**Dropshipping XML Import for WooCommerce, WP Desk (Polska)**
- Wersja 1.7.5 (aktualizacja 5.11.2026), 700+ instalacji, 4.3/5 z 11 recenzji (2 × 1★). Wersja darmowa importuje produkty proste i wariantowe z CSV/XML po URL (HTTP/HTTPS), z mapperem drag-and-drop pól z podglądu pliku. PRO dodaje harmonogram (cron), logikę warunkową, modyfikatory cen (stałe, procentowe, warunkowe), auto-kategorie i przenoszenie brakujących produktów do kosza. Upload z FTP lub komputera wymaga dodatku. Ceny PRO nie ma na stronie wordpress.org. Jedna recenzja 1★ zgłasza brak opcji narzutu w panelu. — [wordpress.org: Dropshipping XML for WooCommerce](https://wordpress.org/plugins/dropshipping-xml-for-woocommerce/)

**EmberPrice – Supplier Price List Import for WooCommerce (nowość, 2026)**
- Opublikowana 20.07.2026, wersja 1.0.2, <10 instalacji, 0 recenzji. Wymaga WP 6.4+, Woo 8.0+, PHP 8.2+. — [wordpress.org: EmberPrice](https://wordpress.org/plugins/emberprice/)
- Funkcje: XLSX/XLS/CSV (PDF nie, tylko "text-layer PDFs planned"); autodetekcja kolumn kod/opis/cena, którą "potwierdzasz raz per dostawca", a kolejne importy ją reużywają; dopasowanie kaskadowe (nauczone aliasy → SKU/GTIN → dokładna nazwa → fuzzy), niepewne wiersze idą do ręcznego potwierdzenia; reguły marży, VAT, zaokrągleń i ceny promocyjnej; **podgląd przed zapisem: stara cena, nowa cena, % zmiany, pewność, flagi** (eksport podglądu do CSV); "hard floor" (cena nie może spaść poniżej ceny z cennika); snapshot i rollback. — [wordpress.org: EmberPrice](https://wordpress.org/plugins/emberprice/)
- AI: w obecnej wersji brak AI/LLM, wszystko działa lokalnie. Planowane jest opcjonalne AI w Pro z własnym kluczem API. Stany magazynowe, multi-currency i importy harmonogramowane są w roadmapie. Pro jest "planned", bez ceny. — [wordpress.org: EmberPrice](https://wordpress.org/plugins/emberprice/)
- Twórca deklaruje dopasowanie 5,000 wierszy do katalogu 10,000 produktów w <4 min. To deklaracja własna, niezweryfikowana. — [mxp.tw (repost opisu)](https://www.mxp.tw/plugins/emberprice/)

### Inferences
- Rynek Woo jest nasycony importerami ogólnymi. Brakuje warstwy "zrozum dowolny cennik (w tym PDF) i pokaż mi zmiany". EmberPrice celuje dokładnie w tę niszę, ale bez PDF i AI oraz z zerową trakcją. To sygnał, że nisza jest dostrzegana, ale nie zajęta.
- Powtarzające się zarzuty o paywall i UX w WP All Import i WebToffee sugerują, że jasny, uczciwy cennik i prosty kreator mogą być wyróżnikiem.
- Ceny wtyczek Woo ($69–$299/rok) wyznaczają psychologiczny pułap dla właścicieli sklepów Woo. Produkt SaaS za ~€19–29/mies. (≈€230–350/rok) byłby droższy od WebToffee, więc musi oferować wyraźnie więcej (PDF, AI-mapping, diff, multi-platforma).

### Gaps
- Ceny WP Desk Dropshipping XML PRO nie udało się potwierdzić (brak na wordpress.org, strony wpdesk.net nie pobrano).
- Nie udało się potwierdzić, czy WP All Import lub WebToffee mają widok diff z poprzednim plikiem. Opisy wskazują raczej na logi i opcję "skip unchanged", nie na diff cenowy.
- Nie znaleziono profilu WP All Import na Trustpilot.
- Recenzji 1★ dla "Product Import for WooCommerce" (Soflyy) nie przejrzano szczegółowo.

---

## P3. PrestaShop (Store Commander i moduły importu na PrestaShop Addons)

### Takeaway
PrestaShop ma kilka dojrzałych, dobrze ocenianych modułów importu z wieloma dostawcami, zapisaną konfiguracją, formułami cen i cronem (ELEGANTAL 4.9★/110, MyPrestaModules 4.6★/180, OBS Solutions 4.1★/35). Żaden z nich, według stron, nie czyta PDF. AI pojawia się tylko do generowania treści, nie do mapowania. Store Commander to narzędzie do masowej edycji back-office w abonamencie (od 9.99/mies.), a nie wyspecjalizowany konwerter cenników.

### Cited Findings
- **Easy Import & Export Products (ELEGANTAL)**: $149.99, 4.9★ z 110 ocen, aktualizacja 1.11.2026. Importuje CSV, XLS, XLSX, XML, JSON, TXT, ODS, RSS, ASC i TSV. Feedy dostawców automatyzuje przez CRON, dopasowuje po referencji dostawcy, zapisuje całą konfigurację jako wielokrotnego użytku "regułę importu". Ma formuły cen (%, kwoty stałe, przedziały, zaokrąglenia) i **wykrywanie zmian, które blokuje ponowny import niezmienionego pliku** (to nie jest diff cenowy per produkt). AI dotyczy wyłącznie feedów do Google, Meta i OpenAI. PDF nie jest wspomniany. Treści negatywnych recenzji nie były widoczne. — [PrestaShop Addons: ELEGANTAL Easy Import](https://addons.prestashop.com/de/datentransfer-backup/24523-easy-import-products-from-csv-excel-xml-json-txt.html)
- **Import et mise à jour du catalogue – CSV, Excel, XML (MyPrestaModules)**: 4.6★ z 180 ocen, aktualizacja wrzesień 2026. Obsługuje CSV, XLSX i XML, mapowanie pól, zapis konfiguracji do przyszłych importów, formuły cen i zaokrąglenia, warianty, cron i testowy import próbki z logami błędów. Opcjonalne AI do treści wymaga klucza OpenAI. PDF nie jest wspomniany. Ceny w EUR nie było w pobranej treści. — [PrestaShop Addons: MyPrestaModules](https://addons.prestashop.com/fr/transfert-sauvegarde-donnees/19091-catalogue-de-produits-csv-excel-dimportation.html)
- **Bulk Import/Update products via CSV, XML or JSON (OBS Solutions)**: 4.1★ z 35 ocen, aktualizacja styczeń 2026. Import z URL, FTP lub pliku lokalnego, wiele konfiguracji dostawców, cena z hurtowej plus marża (stała lub per produkt), URL-e cron, alerty niskiego stanu i "Test Mode" do walidacji. Ceny nie odczytano. — [PrestaShop Addons: OBS Solutions](https://addons.prestashop.com/en/data-transfer-backup/21973-bulk-import-update-products-via-csv-xml-or-json.html)
- **Store Commander**: cennik (ceny miesięczne netto) obejmuje Solo Start 9.99, Solo 39.99 i Solo Plus 79.99 dla 1 sklepu. Ceny roczne i multisklep nie były widoczne w treści. Na liście funkcji są "konfigurowalne narzędzia importu/eksportu CSV" i AI do edycji zdjęć (kadrowanie, usuwanie tła). Nie wiadomo, które plany zawierają import CSV. — [Store Commander: Licences](https://my.storecommander.com/fr/content/45-licences-store-commander). Moduł jest na Addons — [PrestaShop Addons: Store Commander](https://addons.prestashop.com/fr/transfert-sauvegarde-donnees/86153-store-commander.html). Wersja dla Shopify zaczyna się od $29.99/mies. (Starter) — [Shopify App Store: Store Commander](https://apps.shopify.com/store-commander?locale=en)
- Inni dostawcy importu dla PrestaShop poza Addons: Webkul Prestashop Import Export (CSV, XLS, XLSX, XML, JSON i TXT z URL, FTP lub SFTP, cron) — [Webkul blog](https://webkul.com/blog/prestashop-import-export/amp/); PrestaShow PrestaShop Importer (XML, CSV i API hurtowni, kolejka plików w jednym CRON, mapowanie kategorii; firma polska) — [PrestaShow](https://prestashow.com/en/prestashop-modules/5-prestashop-smart-importer-xml-csv-api-integration.html)

### Inferences
- Moduły PrestaShop to jednorazowy zakup (~$150) z mocną, ale "techniczną" konfiguracją. Konwerter SaaS musiałby konkurować łatwością (AI-mapping, PDF, diff), bo samą automatyzacją CSV/XML nie wygra.
- "Change detection" w ELEGANTAL (pomijanie niezmienionego pliku) pokazuje, że diff jest rozumiany wąsko. Czytelny raport "co się zmieniło u dostawcy" (ceny ±%, nowe i zniknięte pozycje) pozostaje wyróżnikiem.

### Gaps
- Nie udało się potwierdzić cen w EUR modułów MyPrestaModules i OBS ani cen rocznych i multisklep Store Commander.
- Modułów nazwanych dokładnie "Advanced Import Products", "Elastic import" i "Simple Import" nie znaleziono na Addons, więc nie udało się ich potwierdzić. Możliwe, że to nazwy z innych platform (np. "Simple Import" na Shopware lub Magento), ale to również niepotwierdzone.
- Nie udało się odczytać treści negatywnych recenzji modułów na Addons (strona pokazuje tylko liczby).

---

## P4. Shopware (wbudowany Import/Export i wtyczki ze Store)

### Takeaway
Shopware 6 ma wbudowany Import/Export oparty na profilach mapowania CSV (UTF-8, średnik). Natywnie nie obsługuje XML, Excela ani PDF. Wtyczki ze Store są drogie w modelu abonamentowym (np. Kommora Import Export Pro za €49.90/mies.) i świeże, bez recenzji. Nie znaleziono wtyczki wyspecjalizowanej w "imporcie cennika dostawcy". Zarządzanie dostawcami i cenami zakupu ma Pickware ERP.

### Cited Findings
- Shopware 6 trzyma profile w Settings > Shop > Import/Export (zakładka Profiles). Oprócz standardowych profili można tworzyć własne. Domyślny format to CSV w UTF-8, separator średnik, cudzysłów jako separator tekstu. — [Shopware docs: Import/Export](https://docs.shopware.com/en/shopware-en/settings/importexport) (treść ze snippetu wyszukiwarki; bezpośredni URL docs zwrócił 404)
- Wtyczka Firebear ostrzega, że przecinek dziesiętny w cenach powoduje błędny import (wymagana kropka). — [Firebear: Ultimate Guide to Shopware 6 Import](https://firebearstudio.com/blog/ultimate-guide-to-shopware-6-import.html)
- Na forum Shopware (głównie era Shopware 5) użytkownicy pisali, że Shopware nie oferuje importu plików .xml, więc trzeba je konwertować do CSV. — [Forum Shopware: Import von Fremd-CSV/XML](https://forum.shopware.com/t/import-von-fremd-csv-xml/33926) (informacja starsza, prawdopodobnie sprzed 2020)
- Stara wtyczka "Shopware Import/Export" (SwagImportExport, shopware AG) jest darmowa, tylko dla Shopware 5.7, bez następcy, bo "funkcje są już w Shopware 6". Ocena 2.8/5 z 25 recenzji, wsparcie 0.2/5. Skargi dotyczą zawieszających się importów, timeoutów i znikającego menu po aktualizacji. — [Shopware Store: Shopware Import/Export](https://store.shopware.com/en/swagef36a3f0ee25/shopware-import-export.html)
- **Import Export Pro – CSV, XLSX & XML (Kommora, DE)**: €49.90/mies. lub €499/rok netto, 1. miesiąc trial. Kompatybilna z Shopware 6.5.0–6.7.16. Obsługuje CSV, XLSX i XML, własne profile z mapowaniem, dry-run z raportem błędów, harmonogram i dostarczanie e-mailem. Encje: produkty, klienci, zamówienia, producenci, kategorie i newsletter. Dostawców nie wspomina. Wydana 3.06.2026, <10 pobrań, 0 recenzji. — [Shopware Store: Kommora Import Export Pro](https://store.shopware.com/en/kommo52751045368m/import-export-pro-csv-xlsx-xml-import-export.html)
- Pickware (ERP, WMS, POS dla Shopware) pozwala tworzyć dostawców (także importem CSV), przypisywać produkty do dostawców i trzymać dane per dostawca (MOQ, cena). — [Pickware help: suppliers](https://help.pickware.com/en/articles/659853-how-do-i-create-and-edit-suppliers); [Shopware Store: Pickware ERP](https://store.shopware.com/de/pickw81188074364f/pickware-erp-wms-pos.html)
- Firebear "Improved Import, Export & Mass Actions" opisuje masową aktualizację cen zakupu i cen netto/brutto, ze scenariuszem synchronizacji z feedami dostawców. — [Firebear: Shopware 6 advanced pricing import](https://firebearstudio.com/blog/shopware-6-advanced-pricing-import.html)

### Inferences
- Kupcy Shopware płacą dziś ok. €40–50/mies. za ogólny importer bez AI i PDF, więc konwerter SaaS w podobnej cenie, który dodaje PDF, AI i diff, byłby konkurencyjny cenowo w tym ekosystemie.
- Rozróżnienie netto/brutto i przecinek dziesiętny to znane problemy w Shopware (i ogólnie w DACH/PL), co potwierdza wartość automatycznej normalizacji cen.

### Gaps
- Wtyczek o nazwach "Lieferanten-Import", "Supplier import" i "Mapp" w Shopware Store nie udało się potwierdzić. DreiscSeo to wtyczka SEO, nie importer (wiedza ogólna, niezweryfikowana w tej sesji).
- Nie udało się pobrać aktualnej (2026) dokumentacji Shopware 6 Import/Export, by potwierdzić obecne formaty i ograniczenia.
- Ceny Firebear dla Shopware nie zostały sprawdzone.

---

## P5. OpenCart (MAVRui i alternatywy) oraz Odoo

### Takeaway
MAVRui, klasyczny moduł cenników dostawców dla OpenCart (porównuje ceny wielu dostawców i wybiera minimalną, śledzi zmiany), jest **wycofany ze sprzedaży** (ostatnia aktualizacja 10/2023). Liderem jest "Suppliers – XML, CSV, XLS Product Feed Import and Update" (usergio, 4.9★/628, 1,776 UAH). W Odoo są tanie moduły (~$21) do importu cenników zakupu do `product.supplierinfo` ze sztywnym układem kolumn, bez AI i PDF.

### Cited Findings
- **MAVRui** (OpenCart 3.0 i 4.0, ocStore 3.0, ionCube, licencja na domenę): importuje cenniki XLS, XLSX, CSV oraz XML o dowolnej strukturze (dla nietypowego XML wsparcie dostarcza handler za darmo). Automatycznie przetwarza ceny i dostępność, nakłada narzuty względem RRP, porównuje ceny kilku dostawców i wybiera minimalną. Po każdej aktualizacji raportuje "nowe produkty, zmiany cen, stany" (rodzaj diffu). Mapuje kategorie, a dostawcę konfiguruje się raz. 5★ z 11 recenzji, 113 pobrań, cena w metadanych $37. Wersja 2.0.5 z **10/21/2023**. Status: "Withdrawn from sale" / "Продажи остановлены администрацией форума". PDF i AI nie są wspomniane. — [OpenCartForum: MAVRui](https://opencartforum.com/en/files/file/1479-avtomaticheskoe-obnovlenie-cen-na-sayte-iz-excel-i-xml-praysov-postavschikov-mavrui)
- Forum jako analog wskazuje "Suppliers – XML, CSV, XLS Product Feed Import and Update" (dawniej "Автоматична обробка прайс-листів"): usergio, 4.9★ z 628 recenzji, 1,776 UAH, zaktualizowany "yesterday" (listopad 2026), z banerem z 09/2026. — [OpenCartForum: Suppliers feed import](https://opencartforum.com/en/files/file/811-avtomatychna-obrobka-prais-lystiv/)
- Inne pokrewne moduły: SimplePars (parser stron i XML/YML, 1,200 UAH, 5.0★/158; autor od 20.09.2024 nie zapewnia wsparcia) i Data Exchange with Google Spreadsheets (455 UAH). — [OpenCartForum: SimplePars](https://opencartforum.com/en/files/file/6362-simplepars-universalnyi-parser-dlia-im/), [OpenCartForum: MAVRui page (analogi)](https://opencartforum.com/en/files/file/1479-avtomaticheskoe-obnovlenie-cen-na-sayte-iz-excel-i-xml-praysov-postavschikov-mavrui)
- **Odoo, Softhealer "Import purchase pricelist vendor details" (sh_import_supplier_info)**: $21.25 (v18), wersje 8.0–20.0, licencja OPL-1, osobny zakup per wersja. Przyjmuje CSV lub Excel (producent zaleca CSV). **Kolejność kolumn jest sztywna** (A: produkt, B: dostawca … G: cena jednostkowa, H–I: daty ważności, J+: pola własne), kolumn nie wolno przestawiać ani usuwać. Dopasowuje po nazwie, kodzie kreskowym lub referencji wewnętrznej. Obsługuje cron, kolejkę i logi odrzuconych wierszy. FAQ mówi, że nie działa na Odoo Online (SaaS), ale sekcja Availability temu przeczy. Brak ocen. — [Odoo Apps: sh_import_supplier_info 18.0](https://apps.odoo.com/apps/modules/18.0/sh_import_supplier_info/)
- Odoo, Mindphin "Import Supplier Info" (md_import_supplier_info, v14–16): CSV i Excel, wiele produktów naraz. — [Odoo Apps: md_import_supplier_info](https://apps.odoo.com/apps/modules/15.0/md_import_supplier_info)
- OCA (społeczność Odoo) ma moduł `product_supplierinfo_import` dla v18. — [Trobz OCA index](https://odoo-modules.trobz.com/oca/product-attribute/18.0/product_supplierinfo_import.html) (szczegółów nie pobrano)

### Inferences
- Ekosystem OpenCart (rynek UA i RU) pokazuje, że "moduł cenników dostawców" to produkt z wysokim popytem (628 recenzji lidera). W Polsce OpenCart jest jednak niszowy.
- Moduły Odoo wymagają, by użytkownik sam przerobił plik dostawcy do sztywnego szablonu. To dokładnie ta praca, którą nasz konwerter mógłby wykonywać jako "pre-processor" dla Odoo.

### Gaps
- Nie udało się potwierdzić powodu wycofania MAVRui ani treści jego 11 recenzji.
- Nie sprawdzono szczegółów modułu usergio (PDF, AI, diff).

---

## P6. Aplikacje Shopify jako punkt odniesienia (Stock Sync/syncX, Matrixify, Syncee, EasyStock)

### Takeaway
Shopify ma tani i bardzo popularny segment synchronizacji feedów dostawców. syncX: Stock Sync kosztuje od $7/mies. (4.8★/940) i obsługuje CSV, XLSX, XML i JSON z wielu źródeł, ale bez PDF. Matrixify (od $20/mies., 4.9★/1,872) to potężny, ale "techniczny" bulk importer. Syncee to marketplace dostawców (dropshipping), a nie konwerter plików. Zarzuty wobec syncX dotyczą zawodności feedów, złego mapowania (np. czytanie niewłaściwego arkusza Excela) i wsparcia.

### Cited Findings
- **syncX: Stock Sync** (dawniej Stock Sync): Free $0 (do 2,000 produktów, 1 feed, tylko ręcznie); Starter $7/mies. lub $77/rok (500–2,500 produktów, 1–5 feedów, 1×/dobę); Expert $10/mies. lub $110/rok (5,000–100,000 produktów, 1–25 feedów, co godzinę, AI-generated content, zaawansowane reguły cen); Scale "$300/mo or $275/yr" (wartości niespójne na stronie). Dodatkowe feedy kosztują $5–7/szt. Formaty: CSV, XLSX, XML, JSON i "Custom format". Źródła: Google Sheets, FTP/SFTP, Drive, Dropbox, REST API, URL oraz WooCommerce/BigCommerce/Wix/Square. PDF nie jest wspomniany. Ocena 4.8 z 940 (43 × 1★). — [Shopify App Store: syncX Stock Sync](https://apps.shopify.com/stock-sync)
- Recenzje 1–2★ syncX (parafrazy): w październiku 2024 aplikacja czytała zły arkusz w pliku Excel, przez co ceny i stany na żywo były błędne (BellGear); w październiku 2024 feed po raz trzeci przestał pobierać zdjęcia (DownUnderThunder); w czerwcu 2024 kolumny mapowały się na złe dane, a logi pomijały warianty (Zelouf Fabrics); w grudniu 2024 integracja była "overly complicated", dokumentacja słaba, a błędy synchronizacji powodowały overselling (Media Alliance CT); w sierpniu 2026 aplikacja ignorowała ustawione ograniczenie tagów (Moto-Rad); w październiku 2024 feedy losowo przestawały działać, a rozwiązanie problemu wymagało 3–5 kontaktów ze wsparciem (Atomic Dev Store). — [Shopify App Store: syncX 1–2★ reviews](https://apps.shopify.com/stock-sync/reviews?ratings%5B%5D=1&ratings%5B%5D=2)
- **Matrixify**: Free (10 produktów na plik), Basic $20/mies. (5K produktów), Big $50/mies. (50K), Enterprise $200/mies. (bez limitu). Obsługuje Excel, CSV i Google Sheets, pliki do 20 GB, harmonogram i FTP/SFTP. Ma serwer MCP dla agentów AI. Ocena 4.9 z 1,872 recenzji, jedyna wskazana wada to "learning curve". — [Shopify App Store: Matrixify](https://apps.shopify.com/excel-export-import)
- **Syncee**: Free (25 produktów), Basic $39.99/mies. (100 produktów), Pro $59.99 (250), Business $99.99 (10,000). Plany płatne mają "private suppliers", ale strona nie wyjaśnia, jak dodać plik własnego dostawcy. Ocena 4.2 z 555 (44 × 1★). Negatywne recenzje dotyczą głównie realizacji zamówień przez dostawców z marketplace (opóźnienia, podwyżki cen po płatności, chargebacki). — [Shopify App Store: Syncee](https://apps.shopify.com/syncee-1)
- **EasyStock** (Camel Soft): listing opisuje zarządzanie zapasami, aktualizacje produktów i czasy dostawy. Nie udało się potwierdzić, że importuje pliki dostawców. — [Shopify App Store: EasyStock](https://apps.shopify.com/easystock)
- **Stockpost**: dostawcy wysyłają CSV lub XLSX ze stanami, aplikacja dopasowuje SKU i zapisuje stan w lokalizacji dedykowanej danemu dostawcy (tylko stany). — [Shopify App Store: Stockpost](https://apps.shopify.com/stockpost) (dane ze snippetu wyszukiwarki)

### Inferences
- Cena referencyjna "synchronizacji feedu dostawcy" na Shopify to $7–10/mies. Sklepy SMB są przyzwyczajone do bardzo tanich narzędzi, co ogranicza możliwą cenę naszego produktu, jeśli oferuje tylko CSV/XML.
- Skargi na syncX (zły arkusz Excel, złe mapowanie kolumn, ciche błędy) wskazują wartość podglądu i diffu przed publikacją oraz walidacji "czy ten plik wygląda jak poprzedni".

### Gaps
- Treści negatywnych recenzji Matrixify nie były widoczne.
- Nie udało się potwierdzić, jak Syncee obsługuje "private suppliers" (DataFeed Manager).

---

## P7. Nowi gracze AI-native (2025–2026): plik dostawcy, w tym PDF, do sklepu

### Takeaway
W latach 2025–2026 pojawiła się fala małych narzędzi AI robiących dokładnie "PDF/Excel dostawcy → CSV Shopify/Woo" z pamięcią mapowania per dostawca. Najbliżej naszego pomysłu są Sheet2Store (jednorazowe opłaty od $19 za katalog, update/diff za $9) i OhoSync (Norwegia, €19–79/mies., Woo+Shopify, PDF, log zmian, AI tylko do mapowania, "ceny ustalają reguły, nie AI"). Wszystkie są bardzo młode, bez recenzji, i żaden nie obsługuje PrestaShop, Shopware, Shopera, IdoSell ani Allegro.

### Cited Findings
- **Sheet2Store** (AGI Solutions, LLC): przyjmuje PDF (z czytelnymi tabelami; skanów jeszcze nie), XLSX i CSV do 20 MB i wyciąga zdjęcia z PDF. Eksportuje do Shopify, WooCommerce, Amazon, noon, Salla, Zid, Trendyol i Hepsiburada. AI generuje tytuły i opisy tylko z faktów w pliku. **Gdy plik dostawcy wraca, zapisane mapowanie kolumn i reguły cen stosuje się automatycznie.** Narzędzie "price & stock update" porównuje eksport sklepu z nowym cennikiem (po kodzie kreskowym, SKU lub nazwie) i zwraca tylko zmienione wiersze, a nowe produkty w osobnym pliku. Cennik: podgląd 5 produktów za darmo, 1 katalog $19 (do 25 stron PDF, 500 wierszy wariantów), 3 katalogi $49, 10 katalogów $99, update $9, bez subskrypcji, ze zwrotem pieniędzy, jeśli pliku nie da się wygenerować. — [sheet2store.com](https://sheet2store.com/)
- **OhoSync** ("Built in Norway"): WooCommerce i Shopify. Przyjmuje Excel, CSV, Google Sheets, **PDF**, XML, API dostawcy i listy linków. Ma zabezpieczenia: wstrzymuje ceny, które skoczą za mocno lub spadną poniżej minimum, i zatrzymuje cały update, gdy plik nagle traci większość produktów. Pozwala blokować ręcznie edytowane pola. Po każdym update daje listę zmian per produkt z przyczyną. AI jest opcjonalne (podpowiedzi mapowania kolumn, ekstrakcja z opisów, przepisywanie opisów); "Prices and stock are always set by your rules, never by AI". Ceny netto: Starter €0 (30 produktów), Basic €19/mies. (500), Growth €29 (1,000, 3 feedy, co 12 h), Pro €79 (3 sklepy, 10 feedów, 5,000, co 6 h). Płatność przez Freemius, managed setup od 2,900 NOK. Nie udało się potwierdzić, czy mapowanie zapisuje się per dostawca. — [ohosync.com](https://ohosync.com/)
- **Csvio – Bulk Product Importer** (VIVIDIYA LABS LLP, Bengaluru; uruchomiony 12.05.2026): Shopify. Przyjmuje CSV, Excel i PDF, mapuje kolumny przez AI, zapisuje układ pliku ("Save your file layouts so repeat imports skip the mapping step"), automatycznie buduje warianty rozmiar/kolor i ma podgląd przed wypchnięciem. Cennik: Free (30 produktów/mies., 1 PDF), PAYG 2¢ za produkt (bez PDF), Starter $19, Pro $39, Scale $79/mies. 0 recenzji. — [Shopify App Store: Csvio](https://apps.shopify.com/csvio-ai-product-importer). Inne źródło podaje Pro za $29/mies. ($290/rok), więc dane są niespójne, prawdopodobnie przez zmianę cennika w maju 2026. — [pickyourapp: Csvio](https://pickyourapp.com/products/csvio-ai-product-importer). Developer ogłosił aplikację na forum Shopify — [Shopify Community: Csvio offer](https://community.shopify.com/t/offer-csvio-import-supplier-csv-excel-and-pdf-price-lists-as-they-arrive-im-the-developer/705289)
- **MicrocityLabs** (MicroCity Solutions Ltd, UK): przyjmuje PDF, Excel, CSV, **skany i zdjęcia z telefonu**. Eksportuje do Shopify, WooCommerce, Odoo, Xero, QuickBooks, Sage, Zoho i Amazon. "Remembers each vendor". Każda wartość jest śledzona do strony źródłowej. Płatność per plik od £15, darmowy podgląd 2 stron, darmowe konto czyta 10 stron dziennie. Diff nie jest wspomniany. — [microcitylabs.com](https://microcitylabs.com/)
- **Importier** (Product Hunt): bulk import do Shopify z CSV, Excel i faktur PDF z AI (opisy, warianty, podatki). 9 obserwujących, czyli bardzo mała trakcja. — [Product Hunt: Importier](https://www.producthunt.com/products/importier-ai-product-import/makers)
- **Jarlix Importer** (Shopify, 7.04.2026): wiele formatów, backup każdego importu i rollback jednym kliknięciem. — [Shopify App Store: Jarlix Importer](https://apps.shopify.com/jarlix-importer) (dane ze snippetu)
- **SkuParse**: "Supplier catalogs to Shopify-ready CSV". Szczegółów (PDF, AI, ceny) nie udało się potwierdzić. — [skuparse.com](https://skuparse.com/)
- Aktory Apify (dla technicznych użytkowników): parser PDF i XLSX cenników z porównaniem rewizji cennika — [Apify: Supplier Price List Parser](https://apify.com/invincible_nova/supplier-price-list-parser); CatalogFix AI od $4.90 za katalog do 50 stron — [Apify: CatalogFix AI](https://apify.com/w_met/catalogfix-ai); konwerter arkusza dostawcy do CSV Shopify/Woo — [Apify: Supplier Sheet converter](https://apify.com/hanktop/supplier-sheet-three-uses)

### Inferences
- Pomysł "AI + pamięć mapowania per dostawca + diff" nie jest już unikalny globalnie (Sheet2Store, OhoSync, Csvio i MicrocityLabs mają po 2–3 z tych cech). Wszyscy są jednak skupieni na Shopify i WooCommerce oraz rynkach EN, Bliskiego Wschodu i Skandynawii. **Brak kogokolwiek dla PrestaShop, Shopware, Shopera, IdoSell i Allegro oraz dla polskich realiów (netto/brutto z VAT 23/8/5%, przecinek dziesiętny, polskie nazwy kolumn).** To najwyraźniejsza nisza.
- Modele cenowe nowych graczy wyznaczają widełki: per plik ($19 / £15 / $9 za update) albo abonament €19–79/mies. Model "per plik / pakiet kredytów" dobrze pasuje do sklepów, które dostają cennik raz w miesiącu.
- OhoSync jasno komunikuje "AI nie ustala cen". Warto przejąć to jako argument zaufania.

### Gaps
- Żaden z nowych graczy nie ma jeszcze recenzji (0 na Shopify, brak Trustpilot i G2), więc jakości działania nie udało się potwierdzić.
- Nie znaleziono wątków na Indie Hackers o tym segmencie.
- Ceny i funkcje SkuParse nie zostały potwierdzone.

---

## P8. Sąsiednie kategorie enterprise (data onboarding i PIM): tylko kontekst

### Takeaway
Flatfile i OneSchema to embeddable importery dla firm SaaS (nie dla sklepów) z cenami pod sprzedaż, szacowanymi przez konkurencję na setki $ miesięcznie i więcej. Na produkty PIM (Akeneo, Salsify, Pimberly, Catsy) oraz Osmos i Hypotenuse w tej sesji nie zebrano zweryfikowanych danych.

### Cited Findings
- Flatfile ma stronę cennika, ale kwoty nie pojawiły się w wynikach. Blog konkurenta (Dromo) twierdzi, że ceny historycznie zaczynają się od ~$799/mies. plus usage, a roczny koszt często przekracza $9,500. To niezweryfikowane źródło konkurencji. — [Flatfile pricing](https://flatfile.com/pricing); [Dromo blog (konkurent)](https://dromo.io/blog/best-flatfile-alternatives-competitors-2026)
- OneSchema ma cenę "quotation based", bez planu darmowego. — [Capterra UK: OneSchema](https://www.capterra.co.uk/software/1032542/oneschema)
- Shopify ma natywną funkcję "Collective": dostawca tworzy price list i udostępnia ją detalistom, ale to zamknięty system między sklepami Shopify. — [shopify.dev: Collective products](https://shopify.dev/docs/apps/build/collective/products)

### Inferences
- Ta kategoria nie konkuruje o klienta SMB, ale pokazuje, że "AI data onboarding" ma sprawdzony popyt w B2B.

### Gaps
- Akeneo, Salsify, Pimberly, Catsy, Osmos, Hypotenuse: ceny i funkcje w tej sesji nie zostały potwierdzone (pominięte zgodnie z zakresem "tylko krótko").

---

## P9. Synteza: porównanie cech i luki rynkowe

### Takeaway
Żadne zweryfikowane narzędzie nie łączy wszystkich cech: dowolny plik + PDF + AI-mapping + pamięć per dostawca + diff + eksport do wielu platform, w tym PrestaShop, Shopware, Shopera, IdoSell i Allegro. Najbliżej są Parabola (wszystko oprócz celów sklepowych i ceny SMB) oraz Sheet2Store i OhoSync (tylko Shopify, Woo i rynki zagraniczne).

### Cited Findings
Tabela zbiorcza. "?" oznacza "nie udało się potwierdzić", a każde pole wynika ze źródeł w sekcjach P1–P7.

| Narzędzie | Platformy docelowe | Dowolny plik | PDF | AI | Pamięć per dostawca | Diff | Cena |
|---|---|---|---|---|---|---|---|
| [Parabola/Prowork](https://parabola.io/use-cases/vendor-price-list-import) | ERP (NetSuite, Fulfil), API | tak | tak | tak | tak (flow) | tak | free 1k kredytów; ~$400/mies. ([3rd party](https://automationatlas.io/answers/parabola-pricing-explained-2026/)) |
| [Eofferix](https://eofferix.com/docs/mapping-fields) | Ozon, partnerzy | tak | ? | ? | tak (profile) | ? | ? |
| [WP All Import](https://www.wpallimport.com/pricing/) | WooCommerce/WP | tak | nie | nie | szablony | nie (skip unchanged) | $169–299/rok; $1,299 lifetime |
| [WebToffee](https://www.webtoffee.com/product/product-import-export-woocommerce/) | WooCommerce | tak | nie | nie | szablony | ? | $69–249/rok |
| [WP Desk Dropshipping XML](https://wordpress.org/plugins/dropshipping-xml-for-woocommerce/) | WooCommerce | tak (CSV/XML) | nie | nie | ? | ? | free / PRO ? |
| [EmberPrice](https://wordpress.org/plugins/emberprice/) | WooCommerce | tak (XLS/CSV) | nie (planowany) | nie (planowane) | tak | tak (podgląd stara/nowa cena) | free (Pro planowany) |
| [ELEGANTAL Easy Import](https://addons.prestashop.com/de/datentransfer-backup/24523-easy-import-products-from-csv-excel-xml-json-txt.html) | PrestaShop | tak | ? | tylko feedy | tak (reguły) | częściowo (wykrywa niezmieniony plik) | $149.99 |
| [MyPrestaModules](https://addons.prestashop.com/fr/transfert-sauvegarde-donnees/19091-catalogue-de-produits-csv-excel-dimportation.html) | PrestaShop | tak | ? | treści (OpenAI) | tak | test próbki | ? |
| [Kommora Import Export Pro](https://store.shopware.com/en/kommo52751045368m/import-export-pro-csv-xlsx-xml-import-export.html) | Shopware 6 | tak | ? | ? | profile | dry-run | €49.90/mies. |
| [MAVRui](https://opencartforum.com/en/files/file/1479-avtomaticheskoe-obnovlenie-cen-na-sayte-iz-excel-i-xml-praysov-postavschikov-mavrui) | OpenCart | tak | ? | ? | tak | tak (raport zmian) | wycofany |
| [Softhealer Odoo](https://apps.odoo.com/apps/modules/18.0/sh_import_supplier_info/) | Odoo | nie (sztywny szablon) | nie | nie | nie | nie | $21.25 |
| [syncX Stock Sync](https://apps.shopify.com/stock-sync) | Shopify | tak | ? | treści | per feed | ? | $0–10/mies. (+feedy) |
| [Matrixify](https://apps.shopify.com/excel-export-import) | Shopify | tak (własny format) | nie | nie | ? | ? | $20–200/mies. |
| [Sheet2Store](https://sheet2store.com/) | Shopify, Woo, Amazon, noon, Salla, Zid, Trendyol, Hepsiburada | tak | tak (tekstowy) | tak | tak | tak ($9 za update) | $19 za katalog |
| [OhoSync](https://ohosync.com/) | Woo, Shopify | tak | tak | opcjonalnie | ? | log zmian | €0–79/mies. |
| [Csvio](https://apps.shopify.com/csvio-ai-product-importer) | Shopify | tak | tak (limit) | tak | tak | podgląd | $0–79/mies. |
| [MicrocityLabs](https://microcitylabs.com/) | Shopify, Woo, Odoo, księgowość | tak | tak + skany | ? | tak | ? | od £15 za plik |

### Inferences
- Wyróżniki, które w zweryfikowanym materiale nie występują razem u nikogo: (1) eksport do polskich platform (Shoper, IdoSell, Allegro) obok Woo, Presty i Shopware; (2) normalizacja netto/brutto z polskimi stawkami VAT i formatami liczb; (3) czytelny diff "co zmienił dostawca" jako raport biznesowy, a nie tylko log techniczny; (4) PDF z pamięcią układu per dostawca.
- Ryzyko konkurencyjne: Sheet2Store, OhoSync i Csvio pokazują, że ten produkt da się szybko zbudować na LLM. Bariera wejścia jest niska, więc obroną muszą być lokalne integracje i jakość na polskich plikach, a nie sama technologia.
- Cenowo: widełki SMB to ~$7–80/mies. (Shopify/OhoSync) albo ~$15–19 za plik (Sheet2Store/MicrocityLabs). Wtyczki Woo i Presty kosztują ~$70–300/rok jednorazowo lub rocznie.

### Gaps
- Brak danych o udziałach rynkowych i przychodach tych narzędzi.
- Nie zweryfikowano, czy któryś z nowych graczy obsługuje polskie platformy (strony ich nie wymieniają, ale to nie jest dowód braku planów).

# Dowody potrzeby: konwersja plików dostawców (cenniki, katalogi, stany) na pliki importu sklepu

Data researchu: 2026-11-06. Oznaczenia klasyfikacji: **[CYKLICZNY]** = ból powtarzalny (aktualizacje cen/stanów co godzinę/dzień/tydzień/miesiąc), **[JEDNORAZOWY]** = ból jednorazowy (początkowa migracja/założenie katalogu), **[MIESZANY]** = oba. Oznaczenie **(snippet)** = treść znana tylko z fragmentu wyszukiwarki, bo strony nie dało się otworzyć (Reddit blokuje pobieranie). Wszystkie parafrazy, bez cytatów dosłownych (chyba że zaznaczono).

Uwaga metodyczna: w latach 2025–2026 duża część wątków na Reddit/Shopify Community to posty **innych founderów walidujących ten sam pomysł** (np. KlarPatch, hhaa123, Supplier Update Guard). To jednocześnie dowód, że problem istnieje, i sygnał rosnącej konkurencji. Oznaczam to przy każdym takim wpisie.

## 1. Fora i społeczności: gdzie sprzedawcy pytają o automatyczny import/aktualizację cenników dostawców

### Takeaway
Problem jest dobrze udokumentowany i ma głównie charakter **CYKLICZNY**: sprzedawcy dostają od dostawców pliki XLSX/CSV/XML (czasem co 15 min – co dzień) i ręcznie dopasowują SKU, chroniąc własne tytuły/opisy przed nadpisaniem. Najmocniejsze, świeże dowody pochodzą z Shopify Community (2024–2026), forum Shopware (DE, starsze + 2023/2024), PrestaShop PL i Allegro Gadane (2025); polskie fora Shoper/IdoSell i grupy FB praktycznie nie są indeksowane.

### Cited Findings
**Shopify Community (EN)**
- E1 [CYKLICZNY] (2026-10-05, wątek walidacyjny innego foundera „KlarPatch”): merchant hhaa123 (kilka tysięcy SKU od wielu dostawców) wylicza, co poprawia ręcznie: warianty kasowane po imporcie nadpisującym, rozbite wiersze z tym samym Handle (zastosowana tylko ostatnia grupa), wymagany Title nawet przy zmianie samej ceny, puste kolumny opcji czyszczące wartości, utrata formuł Excela przy zapisie do CSV. Pomogło mu porównanie „na sucho” z aktualnym eksportem sklepu, które ujawniło duplikaty i niedopasowane SKU. Inny uczestnik (EverythingDSM) chce aktualizować tylko koszt i stan, bez ruszania tytułów, opisów, zdjęć, tagów, SEO i cen detalicznych, a brakujące, zduplikowane, nowe, wycofane i mocno zmienione wiersze mają być oznaczone do przeglądu. Tom_Wang (dostawca narzędzia) wspomina o dodatkowych kolumnach do przeliczania jednostek (karton/paleta/metr na sztuki) i o utracie historii kosztów przy nadpisywaniu. Uwaga: kilku uczestników to dostawcy aplikacji. — [Shopify Community](https://community.shopify.com/t/what-do-you-still-fix-by-hand-when-updating-supplier-prices-or-stock/692332)
- E2 [CYKLICZNY] (2022-07-27, starszy): dostawcy wysyłają sprzedawczyni cenniki w XLSX. Eksportuje produkty ze Shopify, ręcznie wyszukuje każde SKU w liście dostawcy i przepisuje cenę, co przy wariantach zajmuje godziny. Około 1000 produktów z wariantami wymagało zmiany cen (ponad 10 000 SKU łącznie). Potrzebna była też formuła: cena sugerowana dostawcy idzie do „compare at”, a jej cena to rabat 5–20%. Polecane w odpowiedziach: Matrixify, Stockeo, Ablestar, VLOOKUP. — [Shopify Community](https://community.shopify.com/t/how-can-i-efficiently-update-prices-using-a-csv-file/138448)
- E3 [CYKLICZNY] (2024-06-21): sprzedawca dostaje codziennie CSV z ponad 5000 produktów od partnera dropshippingowego. Chce aktualizować tylko cenę i stan wariantu, ale Shopify wymaga kolumny Title, a on boi się nadpisać własne, zredagowane tytuły. W odpowiedziach polecono syncX Stock Sync i Feeds Bridge. — [Shopify Community](https://community.shopify.com/t/import-csv-updating-variant-price-and-variant-inventory-qty-without-overwriting-title/333334)
- E4 [CYKLICZNY + skarga na konkurencję] (2023-02 do 2023-12): dostawca co kilka godzin wysyła mailem arkusz do aktualizacji stanów dropshippingowych. Ceny zsynchronizowane przez Stock Sync zupełnie nie zgadzały się z arkuszem, a wsparcie odsyłało do artykułów pomocy. Inny użytkownik doładował 50 USD, a import zawiesił się na 65%. Przedstawiciel konkurencyjnej aplikacji przyznał, że 72 USD to „stosunkowo dużo”. — [Shopify Community](https://community.shopify.com/t/what-reliable-app-can-replace-stock-sync-for-dropship-stock-updates/192086)
- E5 [CYKLICZNY] (2022-11, DE, snippet z listy powiązanych wątków): dostawca aktualizuje plik CSV ze stanem co 15 minut, a sprzedawca nie radzi sobie z aktualizacją stanów po SKU. — [Shopify Community (related topics)](https://community.shopify.com/t/update-shopify-stock-levels-via-csv-with-no-handle-only-sku/306346)
- E6 [CYKLICZNY] (2024-03-26, sam tytuł): aktualizacja stanów przez CSV, gdy w pliku jest tylko SKU, a nie ma Handle. — [Shopify Community](https://community.shopify.com/t/update-shopify-stock-levels-via-csv-with-no-handle-only-sku/306346)
- E7 [CYKLICZNY] (2021, starszy, snippet): sprzedawca szuka prostej aplikacji, która codziennie zaimportuje CSV dostawcy dropshippingowego z URL i zaktualizuje stany. — [Shopify Community](https://community.shopify.com/t/app-to-daily-auto-import-inventory-quantity-csv-from-dropship-supplier/37696)

**Forum Shopware (DE)**
- E8 [MIESZANY] (2017-02-15, starszy): CSV od dostawcy ma około 13 800 wierszy i 34 kolumny. Nagłówki nie pasują do pól Shopware, mapowanie w Import/Export się nie udaje, import odrzuca nieznane kategorie i kolory, a struktury rozmiarów, kolorów i płci są inne. Potrzebny jest też cron do cyklicznej aktualizacji dostępności. Sprzedawca ma Community Edition i ograniczony budżet, ale deklaruje, że zapłaci za działające rozwiązanie. — [forum.shopware.com](https://forum.shopware.com/t/lieferanten-artikel-feed-csv-importieren-wer-kann-helfen/43754)
- E9 [CYKLICZNY] (2017-03-15, starszy): czasy dostawy i stany z CSV dostawcy są przepisywane ręcznie. Pliki dostawcy nie zawierają numeru artykułu (ordernumber), którego wymaga import Shopware, więc sprzedawca pyta o dopasowanie po EAN i o import kilka razy dziennie. — [forum.shopware.com](https://forum.shopware.com/t/lieferantendaten-mit-import-export-advanced-importieren/44507)
- E10 [CYKLICZNY] (2023-04-02, odpowiedź z 2024-02-12): przy imporcie cen z CSV trzeba podać zarówno cenę netto, jak i brutto. Sprzedawca liczy netto w Excelu, a po imporcie zrywa się automatyczne powiązanie netto–brutto w ponad 1500 produktach. W 2024 inny użytkownik zgłosił niespójne zachowanie flagi `linked`. — [forum.shopware.com](https://forum.shopware.com/t/korrektes-importieren-von-preisen/99189)
- E11 [CYKLICZNY] (2010, bardzo stary; według podsumowania wyszukiwarki, strony nie otwierałem): pytanie, czy CSV dostawcy można pobierać z FTP i importować co 2 godziny. Odpowiedź: standardowo się nie da, trzeba napisać plugin z cronem. — [forum.shopware.com](https://forum.shopware.com/t/automatischer-import/1112)

**PrestaShop (PL)**
- E12 [CYKLICZNY] (2022-11-12, starszy): CSV z hurtowni zawiera około 70 tys. produktów, a w sklepie jest około 3 tys. od tego dostawcy. Sprzedawca chce aktualizować tylko ilości istniejących produktów. Odpowiedź: Presta przy imporcie utworzy brakujące produkty, więc trzeba napisać skrypt czyszczący plik. Sprzedawca od razu pyta, czy może za taki skrypt zapłacić. — [forum.prestashop.com](https://forum.prestashop.com/topic/1070349-aktualizacja-ilo%C5%9Bci-wybranych-produkt%C3%B3w-csv/)
- E13 [MIESZANY] (data nieznana, snippet): do sklepu dostępne są tylko pliki XML od dostawców, a Presta importuje CSV. — [forum.prestashop.com](https://forum.prestashop.com/topic/339861-import-pliku-xml-baza-produkt%C3%B3w/)
- E14 [JEDNORAZOWY/MIESZANY] (starszy, snippet): import CSV psuje polskie znaki. Obejście polega na przekodowaniu pliku na UTF-8 w Notepad2. — [polskapresta.pl](https://polskapresta.pl/index.php?topic=505.0); dokumentacja platformy Shopgold wymaga UTF-8 bez BOM — [shopgold.pl](https://www.shopgold.pl/podstawowe-dane-do-importu-produktow-z-plikow-csv-n-364.html)

**Allegro Gadane (PL)**
- E15 [CYKLICZNY] (2025-05-20): sprzedawca z około 1300 ofertami szuka prostej aplikacji, która przez API zaktualizuje stany po SKU z pliku CSV/JSON wygenerowanego przez program magazynowy. Aktualizuje 2–4 razy dziennie, zwykle zmienia się mniej niż 100 pozycji. Import CSV w Allegro zawiódł przy ofertach w innej kategorii niż produkt. Wprost odrzuca ciężkie narzędzia typu BaseLinker. Rozwiązaniem okazało się darmowe rozszerzenie Chrome od innego użytkownika. — [spolecznosc.allegro.pl](https://spolecznosc.allegro.pl/t5/pocz%C4%85tkuj%C4%85cy-sprzedawcy/prosta-aplikacja-aktualizacji-stan%C3%B3w-przez-api/td-p/1022471)

**WordPress.org / WooCommerce**
- E16 [CYKLICZNY] (snippet, data nieznana): plik produktowy dostawcy ze zdjęciami, opisami, cenami i stanami jest aktualizowany co 30 minut, a dodatkowo dostawca udostępnia mały plik XLS. — [wordpress.org support](https://wordpress.org/support/topic/product-modification-date-after-import/)
- E17 [CYKLICZNY] (snippet): użytkownik chce aktualizować ceny importem, ale dopasowanie działa tylko po ID lub SKU. — [wordpress.org support](https://wordpress.org/support/topic/update-prices-2/)
- E18 (2020, Stack Overflow): użytkownik aktualizuje ceny przez WP All Import i pyta, jak przyspieszyć taki import. — [Stack Overflow](https://stackoverflow.com/questions/61823825/how-can-you-improve-the-speed-of-the-wpallimport-for-updating-prices)

**Reddit (wyłącznie snippety; nie da się pobrać treści, daty niezweryfikowane)**
- E19 [CYKLICZNY] r/shopify: sprzedawca aktualizuje ceny w Matrixify po SKU lub UPC z cenników, ale kilku dostawców wysyła PDF zamiast CSV. — [Reddit](https://www.reddit.com/r/shopify/comments/1fjiwcb/how_do_you_manage_thousands_of_items_from/)
- E20 [CYKLICZNY] r/shopify: sprzedawca nie chce dodawać wszystkich produktów dostawcy, tylko utrzymywać aktualne stany na podstawie plików Excel. — [Reddit](https://www.reddit.com/r/shopify/comments/1p6ir95/import_products_into_the_shopify_store_or_keep/)
- E21 [CYKLICZNY] r/ShopifyeCommerce: Matrixify kosztuje 50–200 USD miesięcznie za sam import/eksport, co użytkownik uważa za przesadę, ale nie zna lepszej aplikacji. — [Reddit](https://www.reddit.com/r/ShopifyeCommerce/comments/1ll4a0d/alternatives_to_the_matrixify_shopify_app/)
- E22 r/InventoryManagement (pytanie, prawdopodobnie walidacja pomysłu): jak bardzo bałaganiarskie są pliki dostawców (losowe nazwy kolumn, niespójne rozmiary i kolory). — [Reddit](https://www.reddit.com/r/InventoryManagement/comments/1v2b0fx/how_do_you_deal_with_messy_supplier_spreadsheets/); podobnie: jak wygląda aktualizacja sklepu z Excela/CSV od dostawcy — [Reddit](https://www.reddit.com/r/InventoryManagement/comments/1w8fzuh/how_do_you_handle_supplier_spreadsheets_when/)
- E23 r/ShopifyApps (walidacja pomysłu): narzędzie porównujące poprzedni i nowy CSV dostawcy przed importem do Shopify. To niemal ta sama funkcja „diff” co w pomyśle foundera. — [Reddit](https://www.reddit.com/r/ShopifyApps/comments/1x0uuok/would_you_use_a_tool_that_compares_supplier_csv/)
- E24 [CYKLICZNY, rynek sąsiedni B2B] r/supplychain: co tydzień przychodzi kolejny 40-stronicowy PDF albo chaotyczny Excel od producenta z podwyżką o 5–8%. — [Reddit](https://www.reddit.com/r/supplychain/comments/1sbsqil/how_is_everyone_handling_these_constant/); r/estimators: większość dostawców wysyła PDF, formatowanie nie pomaga, praca jest ręczna — [Reddit](https://www.reddit.com/r/estimators/comments/1kqsysg/how_do_you_manage_supplier_price_lists/)
- E25 r/shopify: odpowiedzi często polecają Stock Sync do dziennych CSV/feedów z dopasowaniem po SKU. — [Reddit](https://www.reddit.com/r/shopify/comments/1jtg0nb/product_sync/)

### Inferences
- Dominuje ból **cykliczny**. Jednorazowa migracja katalogu pojawia się głównie w zleceniach freelance (pkt 2), a na forach przeważają pytania o regularną aktualizację cen i stanów bez psucia własnych danych.
- Najczęstszy scenariusz to nie „nie umiem przekonwertować formatu”, tylko „chcę zaktualizować **podzbiór** pól dla **podzbioru** produktów (tych, które mam) i nie zepsuć reszty”. Diff i przegląd zmian przed importem to funkcja, o którą ludzie proszą wprost (E1, E23).
- PDF jako format wejściowy pojawia się rzadziej niż XML/CSV/XLSX w kontekście e-commerce (E19). Częściej występuje w B2B, budowlance i hurcie (E24).

### Gaps
- **forum.shoper.pl**: żadne wyszukiwanie (Google site:, Firecrawl) nie zwróciło wątków. Forum jest słabo indeksowane albo wątków jest mało; należy przeszukać je ręcznie po zalogowaniu.
- **IdoSell community/forum**: nie znalazłem wątków. Są tylko materiały producenta o IAI Downloader ([idosell.com](https://www.idosell.com/en/iai-downloader-automatic-import-offer-updates-and-integration-with-suppliers/iai-downloader-functions-and-possibilites/mass-update-of-product-database/)).
- **Grupy Facebook**: posty praktycznie nie są indeksowane. Znalazłem jeden post z grupy „Forum Sprzedawców” o ręcznym wpisywaniu cen zakupu z faktur do Excela, ale jest to reklama narzędzia i nie dotyczy wprost tematu: [facebook.com](https://www.facebook.com/groups/forum.sprzedawcow/posts/4476311142618497/).
- **wykop, elektroda**: brak trafnych wyników.
- **Reddit**: treści wątków niedostępne (blokada 403), więc korzystałem tylko ze snippetów i nie mam dat.
- **Shopware**: brak świeżych (2024–2026) wątków od sprzedawców o cennikach dostawców. Wyniki zdominowane są przez strony vendorów pluginów (Firebear, Import2Shop).

## 2. Zlecenia freelance: popyt i budżety

### Takeaway
Useme pokazuje stały popyt w PL (2022–2026): podłączenie hurtowni, konwersja XML/CSV, aktualizacje cen ze stałą marżą, 6–58 ofert na zlecenie. Budżety są jednak niemal zawsze „Do negocjacji”. Na Fiverr usługa „supplier/vendor file → Shopify/WooCommerce CSV” jest towarem masowym za 5–100 USD (typowo 10–30 USD), a na Upwork pakiety kosztują około 35–200 USD. Freelancehunt (UA) potwierdza bardzo konkretne potrzeby typu „4 dostawców, każdy Excel inny”.

### Cited Findings
**Useme (PL)**. W każdym z 9 sprawdzonych zleceń budżet to „Do negocjacji”.
- U1 [JEDNORAZOWY] (2022-11-18, 6 ofert): firma ma pliki XML z produktami w różnych konfiguracjach. Chce je ujednolicić, przekonwertować na CSV i wgrać do PrestaShop, Shoper i WooCommerce. Listy mają od kilkudziesięciu do kilkuset pozycji. — [Useme](https://useme.com/pl/jobs/poszukujemy-osoby-do-konwersji-plikow-xml-do-csv-i-pozniejsze-wdrozenie-do-sklep,69230/)
- U2 [CYKLICZNY] (2024-03-20, 18 ofert): sklep z gadżetami reklamowymi na Shoper. Potrzebuje narzędzia do około 15 hurtowni (zwykle pliki XML), które zaktualizuje nazwy, opisy, ceny, stany i zdjęcia. Właściciel chce uniknąć „żmudnych i kosztownych ręcznych aktualizacji” (parafraza). Wymagania: aktualizacja dzienna i doliczanie stałej marży do cen hurtowych. — [Useme](https://useme.com/pl/jobs/api-aplikacja-do-importu-danych-z-15-hurtowni-do-sklepu-shoper,93003/)
- U3 [CYKLICZNY] (2024-07-11, 6 ofert): międzynarodowa sprzedaż opon. Apilo przyjmuje XML w formacie IOF, a według zleceniodawcy prawie wszystkie hurtownie dają API albo CSV na FTP, jedna z nich co godzinę. Potrzebna jest więc konwersja do formatu Apilo. — [Useme](https://useme.com/pl/jobs/podaczenie-zewnetrznych-hurtowni-do-apilo,99669/)
- U4 [CYKLICZNY, sąsiedni: przyjęcia magazynowe] (2025-05-05, 19 ofert): CSV z dostaw są niespójne (raz indeksy z prefiksem i łączną wartością, raz bez prefiksów). System wymaga prefiksu, indeksu, ilości i ceny, więc potrzebne jest automatyczne przekształcanie plików. — [Useme](https://useme.com/pl/jobs/konwertowanie-plikow-csv,115168/)
- U5 [MIESZANY] (2025-07-09, 10 ofert): sklep Shopify z butami piłkarskimi i plik XML z hurtowni. Do zrobienia: rozmiary jako warianty, zdjęcia, opisy, stany, ceny z marżą, automatyczna lub półautomatyczna aktualizacja stanów i cen. Zleceniodawca deklaruje, że jest nietechniczny. — [Useme](https://useme.com/pl/jobs/sklep-na-shopify-integracja-z-hurtownia-plik-xml,118834/)
- U6 [JEDNORAZOWY setup synchronizacji cyklicznej] (2025-11-06, 17 ofert): konfiguracja BaseLinkera z kilkoma hurtowniami dropshippingowymi (XML/API) i Shopify. Wymagana synchronizacja stanów i cen „w czasie rzeczywistym”. — [Useme](https://useme.com/pl/jobs/integracja-baselinker-z-hurtowniami-zewnetrznymi-i-sklepem-shopify,125873/)
- U7 [MIESZANY] (2026-07-30, 58 ofert): sklep B2B z narzędziami ogrodniczymi na WooCommerce. Około 2400 indeksów z XML producenta, mapowanie kategorii, zdjęć i atrybutów oraz **cykliczna aktualizacja cen zakupu z tego pliku**. Zleceniodawca prosi o podanie rocznej ceny licencji gotowego konektora. — [Useme](https://useme.com/pl/jobs/wdrozenie-sklepu-b2b-hurtownia-narzedzi-ogrodniczych-z-indywidualnymi-cennikami,141894/)
- U8 [CYKLICZNY] (2022-10-01, 1 oferta, starszy): IdoSell, 3 hurtownie z linkami XML, aktualizacja stanów i cen co najmniej raz na dobę. — [Useme](https://useme.com/pl/jobs/integracja-hurtowni-ze-sklepem-na-idosell-za-posrednictwem-iai-downloader,67286/)
- Inne zlecenia Useme widoczne tylko w snippetach: integracja Presta z platformą B2B przez XML/CSV z aktualizacją stanów i cen ([Useme](https://useme.com/pl/jobs/integracja-platformy-b2b-z-prestashop,98281/)); integracja z hurtownią przez CSV/WebAPI, w której przy kolejnym imporcie nie wolno nadpisywać opisów i tytułów ([Useme](https://useme.com/pl/jobs/integracja-sklepu-internetowego-z-hurtownia-csv-lub-webapi,25364/)); pilne zmapowanie i powiązanie produktów między dwoma cennikami w Excelu ([Useme, lista](https://useme.com/pl/jobs/category/prace-biurowe,40/wprowadzanie-danych,132/?page=20&order_by=-payment_normalized)).

**Freelancehunt (UA).** Daty i budżety nie są widoczne bez logowania, widać tylko liczbę ofert.
- U9 [CYKLICZNY] (66 ofert; sąsiednie ID z października/listopada 2026): mały sklep z częściami samochodowymi i 4 dostawców. Każdy wysyła Excel o innej strukturze: artykuł raz w 1., raz w 3. kolumnie, ceny raz w USD, raz w UAH. Zleceniodawca chce skryptu w Pythonie, który połączy je w jeden plik. — [Freelancehunt](https://freelancehunt.com/project/skript-na-python-chtobyi-svodit-praysyi/1661107.html)
- U10 [CYKLICZNY] (13 ofert): automatyczne przetwarzanie różnoformatowych cenników dostawców do jednego CSV z 3 kolumnami (id, nazwa, cena detaliczna), który trafia na stronę. — [Freelancehunt](https://freelancehunt.com/project/sdelat-avtomaticheskuyu-obrabotku-raznoobraznyih-praysov/1573246.html)
- U11 (snippet): automatyzacja pracy z cennikami, czyli łączenie cenników dostawców w YML/CSV, synchronizacja kategorii i eksport do YML/Excel. — [Freelancehunt](https://freelancehunt.com/ua/project/avtomatizatsiya-roboti-praysami-ta-skladom/1165615.html); arkusz Google/Excel do aktualizacji stanów na stronie na podstawie tabel dostawców — [Freelancehunt](https://freelancehunt.com/ua/project/fayl-google-tablitsi-excel-dlya-onovlennya/1617737.html); import i aktualizacja produktów dostawcy na Horoshop (4 oferty) — [Freelancehunt](https://freelancehunt.com/ua/project/import-obnovlenie-tovarov-postavschika-yug/1175518.html)

**Fiverr (oferty sprzedających)**
- Na stronie tagu „shopify csv” gigi zaczynają się od 5 USD do 100 USD. Wiele z nich nazywa się „convert any vendor/supplier file into Shopify/WooCommerce CSV” i kosztuje od 10–30 USD. — [Fiverr](https://www.fiverr.com/gigs/shopify-csv)
- Gig za 100 USD: przekształcenie Excela dostawcy w zbiorczy CSV do Shopify. — [Fiverr](https://www.fiverr.com/hossainzabed/reshape-supplier-excel-file-into-bulk-csv-listing-to-upload-any-website)
- Wyspecjalizowane gigi: zamiana cenników dostawców na pliki do Shopify, WooCommerce lub Amazon — [Fiverr](https://www.fiverr.com/tidydatauk/turn-supplier-price-lists-into-shopify-woocommerce-or-amazon-upload-files); cenniki do Shopify/Woo — [Fiverr](https://www.fiverr.com/puhmeister_luka/convert-supplier-price-lists-into-shopify-or-woocommerce-import-csv); listy dostawcy do CSV WooCommerce — [Fiverr](https://www.fiverr.com/smartolomeus/convert-your-supplier-lists-into-a-clean-woocommerce-product-import-csv)

**Upwork (pakiety usług)**
- 95 USD za oczyszczenie jednego cennika dostawcy (do 500 wierszy i 10 kolumn) ze sprawdzeniem SKU i cen. — [Upwork](https://www.upwork.com/services/product/admin-customer-support-a-cleaned-supplier-price-list-with-sku-and-price-checks-2108927896407015122)
- Porównanie starego i nowego cennika dostawcy z oznaczeniem zmian cen oraz nowych i usuniętych pozycji (do 200 wierszy, dostawa w 2 dni). Usługa „diff” sprzedawana ręcznie. — [Upwork](https://www.upwork.com/services/product/admin-customer-support-i-will-compare-old-and-new-supplier-price-lists-and-flag-changes-2108322491870819321)
- Zamiana cennika dostawcy na plik importu Shopify/WooCommerce (reguły cenowe, warianty, filtry stanów). — [Upwork](https://www.upwork.com/services/product/development-it-a-clean-deduplicated-contact-list-ready-for-your-crm-import-2105708447227512870); katalog, cennik lub PDF ze specyfikacją do Excela/CSV — [Upwork](https://www.upwork.com/services/product/admin-customer-support-a-clean-excel-or-csv-spreadsheet-from-your-product-catalog-2099385692546382260); ekstrakcja cennika z PDF — [Upwork](https://www.upwork.com/services/product/admin-customer-support-extract-invoice-product-or-price-list-data-from-pdf-2082383707445335156)
- Pakiet uploadu produktów z CSV/Excel/XML dla Shopify/Woo: od 50 produktów prostych lub 25 wariantowych w wariancie starter do 1000 prostych lub 400 wariantowych w wariancie advanced (według podsumowania wyszukiwarki). — [Upwork](https://www.upwork.com/services/product/product-upload-csv-dropshipping-products-for-shopify-or-woocommerce-store-1330742221159485440)

### Inferences
- W PL zlecenia dotyczą głównie **XML od hurtowni → sklep/BaseLinker/Apilo** i są cykliczne (codzienne lub godzinowe). „Konwersja jednego pliku” jako jednorazowe zlecenie pojawia się rzadziej (U1).
- Na rynku anglojęzycznym konwersja „vendor file → Shopify CSV” jest tanim, masowym towarem (10–30 USD). Jednorazowa konwersja ma więc niską wartość, a wartość leży w powtarzalności: zapamiętane mapowanie i diff.
- Ukraińskie zlecenia (U9, U10) bardzo dokładnie opisują problem z pomysłu: różne kolumny, różne waluty, wielu dostawców, jeden plik wyjściowy.

### Gaps
- **Budżety na Useme są ukryte** („Do negocjacji”) we wszystkich sprawdzonych zleceniach. Nie znalazłem konkretnych kwot w PLN.
- **Zlecenia klientów na Upwork** (job posts) wymagają logowania. Znalazłem tylko oferty freelancerów (pakiety), nie budżety klientów.
- **Oferia, Freelancer.com**: nie przeszukane z powodu limitu czasu i wywołań.
- **Freelancehunt**: brak dat i budżetów bez logowania.

## 3. Recenzje i skargi na konkurencję: niezaspokojone potrzeby

### Takeaway
Główne skargi dotyczą ceny (Matrixify 50–200 USD miesięcznie, pro WP All Import „kilkaset euro”), zbyt ciężkich narzędzi (BaseLinker „kobyła”), błędnych synchronizacji cen i słabego wsparcia (Stock Sync), a w PL także ograniczenia BaseLinkera i Apilo do hurtowni z listy (nietypowy plik wymaga płatnego wdrożenia). Jednocześnie w 2025–2026 pojawiło się wiele małych narzędzi robiących niemal dokładnie to, co pomysł foundera. Największe bezpośrednie zagrożenie to Sheet2Store.

### Cited Findings
- Stock Sync (syncX), ocena 4,8 przy około 936 recenzjach. Recenzje jednogwiazdkowe: bardzo wolne wsparcie, odpowiedzi botów, problemy przy wielu feedach. — [Shopify App Store](https://apps.shopify.com/stock-sync/reviews?page=4&ratings%5B%5D=1); w 2023 zgłaszano ceny zsynchronizowane „zupełnie inne” niż w arkuszu dostawcy — [Shopify Community](https://community.shopify.com/t/what-reliable-app-can-replace-stock-sync-for-dropship-stock-updates/192086)
- Matrixify: recenzent zapłacił za plan Basic (20 USD), a aplikacja kazała mu przejść na plan za około 100 USD. — [Shopify App Store](https://apps.shopify.com/excel-export-import/reviews); 50–200 USD miesięcznie „za sam import/eksport” to według użytkownika przesada (snippet) — [Reddit](https://www.reddit.com/r/ShopifyeCommerce/comments/1ll4a0d/alternatives_to_the_matrixify_shopify_app/)
- WP All Import (1966 recenzji): francuska recenzja mówi, że wersja pro „działa w połowie”, eksport dziesiątek tysięcy wierszy trwa godziny, a cena pro „kilkaset euro” jest nieopłacalna. Pojawia się też polska recenzja pozytywna. — [wordpress.org](https://wordpress.org/plugins/wp-all-import/)
- BaseLinker: sprzedawca na Allegro wprost nie chce „kobył typu BaseLinker” do prostej aktualizacji stanów (E15). — [Allegro Gadane](https://spolecznosc.allegro.pl/t5/pocz%C4%85tkuj%C4%85cy-sprzedawcy/prosta-aplikacja-aktualizacji-stan%C3%B3w-przez-api/td-p/1022471); w innej opinii (według podsumowania wyszukiwarki, nie otwierałem) integracja przebiegła gładko, ale potem pojawiały się błędy, a wsparcie oceniono średnio — [Allegro Gadane](https://spolecznosc.allegro.pl/t5/zaawansowani-sprzedawcy/czy-warto-korzysta%C4%87-z-baselinker/m-p/1171521)
- BaseLinker pozwala integrować wyłącznie hurtownie, które są w systemie. Dla innych dostawców potrzebny jest pośrednik, np. SellPander. — [sellpander.pl](https://www.sellpander.pl/integracja-z-hurtownia/)
- Apilo przyjmuje XML w formacie IOF, więc hurtownie z CSV na FTP wymagają konwersji (U3). — [Useme](https://useme.com/pl/jobs/podaczenie-zewnetrznych-hurtowni-do-apilo,99669/)
- **Bezpośredni konkurenci 2025–2026 (sygnał nasycenia):**
  - Sheet2Store: PDF/XLSX/CSV do Shopify, WooCommerce, Amazon, noon, Trendyol i innych. Zapamiętuje mapowanie i ceny per dostawca, porównuje eksport sklepu z nowym cennikiem i pobiera tylko zmiany, grupuje warianty kolor/rozmiar, wyciąga zdjęcia z PDF, nalicza marżę. Ceny: 19 USD za katalog, 49 USD za 3, 99 USD za 10, **9 USD za aktualizację** cen/stanów. — [sheet2store.com](https://sheet2store.com/)
  - Koalab Sync: Excel/CSV od dostawcy, mapowanie kolumn, reguły marży, podgląd każdej zmiany, cofnięcie całego uploadu. Jest plan darmowy, płatne plany dodają harmonogram i reguły cen. Plugin nie ma jeszcze recenzji. — [wordpress.org](https://wordpress.org/plugins/koalab-sync/)
  - Supplier Update Guard: przegląd cen z CSV dostawcy przed importem do Shopify, 19 USD jednorazowo, brak odpowiedzi merchantów (2026-10-17). — [Shopify Community](https://community.shopify.com/t/review-supplier-csv-prices-before-a-shopify-import-19-once/700040)
  - Inne narzędzia z podsumowań wyszukiwarki (nie weryfikowałem każdego): EmberPrice, CostHarbor (wtyczki WooCommerce z podglądem i rollbackiem), aktor Apify „Supplier Sheet to Shopify, WooCommerce and Weekly Diff”, Csvio (darmowo 3 importy miesięcznie, zapisane układy plików), GrowthLine File Cleaner, StockPatch. — [Apify](https://apify.com/hanktop/supplier-sheet-three-uses), [Apify](https://apify.com/nsk5713/supplier-spreadsheet-shopify-csv), [Shopify Community – StockPatch](https://community.shopify.com/t/free-tool-for-supplier-stock-csv-updates-by-sku-in-shopify-stockpatch/688250/3), [Shopify Community – free tool](https://community.shopify.com/t/free-tool-turn-a-supplier-excel-csv-into-a-shopify-import-file-feedback-wanted/692949)

### Inferences
- Rynek anglojęzyczny (Shopify/Woo) jest zatłoczony małymi narzędziami „supplier file → import + diff”. Wyróżnikami pomysłu mogą być **polskie platformy** (Shoper, IdoSell, Allegro: żaden ze znalezionych konkurentów nie wymienia ich jako celu) oraz **polskie realia**: netto/brutto i VAT, Windows-1250, szt./opak.
- Luka w PL: BaseLinker i Apilo dobrze obsługują hurtownie z listy (XML/API), ale nie pliki ad hoc (Excel/PDF od małego dostawcy) bez płatnego wdrożenia. Właśnie tu narzędzie typu „wgraj plik” ma sens.

### Gaps
- Nie znalazłem niezależnych recenzji Store Commandera ani Parabola dotyczących tego przypadku użycia. Brak też recenzji aplikacji hurtowni z Shoper AppStore (strona VeroSoft nie pokazała ocen).
- Nie sprawdziłem Trustpilot, Capterra ani G2 dla BaseLinkera.

## 4. Konkretne bóle: ranking (częstotliwość × dotkliwość)

### Takeaway
Na szczycie są: różne układy kolumn u każdego dostawcy, dopasowanie wierszy do własnych produktów (SKU/EAN, nadmiar produktów w pliku hurtowni), aktualizacja wybranych pól bez nadpisywania własnych treści oraz marża i reguły cenowe. Warianty/rozmiary i netto/brutto są istotne, ale rzadsze. PDF, jednostki, waluta i kodowanie pojawiają się sporadycznie.

### Cited Findings
1. **Inny układ kolumn i struktura per dostawca** (bardzo częsty, wysoki ból): E8 (34 kolumny, nagłówki niezgodne), U9 (artykuł w różnych kolumnach), U1 (XML w różnych konfiguracjach), U4, E22. — [Shopware](https://forum.shopware.com/t/lieferanten-artikel-feed-csv-importieren-wer-kann-helfen/43754), [Freelancehunt](https://freelancehunt.com/project/skript-na-python-chtobyi-svodit-praysyi/1661107.html), [Useme](https://useme.com/pl/jobs/poszukujemy-osoby-do-konwersji-plikow-xml-do-csv-i-pozniejsze-wdrozenie-do-sklep,69230/)
2. **Dopasowanie do własnych produktów** (SKU dostawcy a własne, brak ordernumber, dopasowanie po EAN, 70 tys. w pliku przy 3 tys. w sklepie, duplikaty i niedopasowane SKU, nowe i wycofane pozycje), bardzo częsty: E9, E12, E1, E2, E17. — [Shopware](https://forum.shopware.com/t/lieferantendaten-mit-import-export-advanced-importieren/44507), [PrestaShop](https://forum.prestashop.com/topic/1070349-aktualizacja-ilo%C5%9Bci-wybranych-produkt%C3%B3w-csv/), [Shopify](https://community.shopify.com/t/what-do-you-still-fix-by-hand-when-updating-supplier-prices-or-stock/692332)
3. **Częściowa aktualizacja bez nadpisywania tytułów i opisów; brak wiersza nie może oznaczać usunięcia ani zera** (częsty, bardzo wysoki ból, bo grozi zepsuciem sklepu): E3, E1, Useme 25364. — [Shopify](https://community.shopify.com/t/import-csv-updating-variant-price-and-variant-inventory-qty-without-overwriting-title/333334), [Useme](https://useme.com/pl/jobs/integracja-sklepu-internetowego-z-hurtownia-csv-lub-webapi,25364/)
4. **Marża i reguły cen** (cena zakupu vs sugerowana, compare-at, stała marża): U2, U5, E2; Apilo liczy cenę jako netto z hurtowni + narzut % + VAT — [Apilo](https://apilo.com/pl/help/podlaczenie-hurtowni-import-xml-csv/); Stock Sync potrafi pobrać RRP zamiast ceny zakupu — [Shopify Community](https://community.shopify.com/t/what-reliable-app-can-replace-stock-sync-for-dropship-stock-updates/192086)
5. **Warianty i rozmiary**: U5 (rozmiary butów), E1 (warianty kasowane przy imporcie), E8 (struktury rozmiar/kolor/płeć); feed hurtowni odzieży Matterhorn podaje stany dla każdego rozmiaru — [matterhorn.pl](https://matterhorn.pl/?str=xmloffer)
6. **Kategorie i atrybuty** (mapowanie): U7, E8 (nieznane kategorie odrzucone przy imporcie), Apilo zaleca osobną kategorię nadrzędną dla produktów z hurtowni — [Apilo](https://apilo.com/pl/help/podlaczenie-hurtowni-import-xml-csv/)
7. **Netto vs brutto i VAT**: E10 (Shopware wymaga obu cen, powiązanie się zrywa). — [Shopware](https://forum.shopware.com/t/korrektes-importieren-von-preisen/99189)
8. **Konwersja formatów XML↔CSV** (platforma przyjmuje inny format niż dostawca): U1, U3, E13.
9. **PDF zamiast Excela**: E19, E24; na Upwork są gigi do ekstrakcji cenników z PDF; Sheet2Store obsługuje PDF z tabelą, ale nie skany. — [sheet2store.com](https://sheet2store.com/)
10. **Waluta**: U9 (USD vs UAH).
11. **Jednostki** (karton/paleta/metr na sztuki): E1 (Tom_Wang).
12. **Kodowanie znaków** (polskie znaki, UTF-8 bez BOM): E14, dowody starsze.
13. **Zdjęcia jako linki**: E8 (pomoc przy zdjęciach podawanych przez URL); feed Matterhorn zawiera linki do zdjęć — [matterhorn.pl](https://matterhorn.pl/?str=xmloffer)
14. **Brakujące lub nieprawidłowe EAN**: słabe dowody. EAN pojawia się tylko jako klucz dopasowania (E9). Nie znalazłem skarg na błędne EAN.

### Inferences
- Do MVP najwięcej daje: (a) zapamiętane mapowanie kolumn per dostawca, (b) dopasowanie po SKU/EAN z raportem niedopasowanych, nowych i wycofanych pozycji, (c) eksport tylko zmienionych pól (cena, stan) z gwarancją nienadpisywania treści, (d) reguły marży i netto/brutto. PDF może poczekać na późniejszą wersję.
- Bezpieczeństwo (podgląd, diff, „nie zeruj brakujących”) jest dla sprzedawców ważniejsze niż sama konwersja formatu (E1).

### Gaps
- Brak twardych danych ilościowych (np. „X% sprzedawców dostaje PDF”). Ranking opiera się na liczbie i jakości znalezionych wzmianek (około 40 źródeł), nie na ankiecie.
- Problem Windows-1250 w plikach od polskich hurtowni nie znalazł świeżego potwierdzenia na forach. Dowody dotyczą ogólnie kodowania (UTF-8, BOM).

## 5. Gotowość do płacenia (WTP)

### Takeaway
Polscy sprzedawcy już płacą za integracje hurtowni: BaseLinker 50 zł netto miesięcznie za każdą hurtownię po pierwszej, Apilo od 599 zł netto jednorazowo za hurtownię spoza listy. Rynek anglojęzyczny ustala kotwice cenowe na poziomie 7–20 USD miesięcznie (Stock Sync, Matrixify Basic), około 9–19 USD za konwersję lub aktualizację (Sheet2Store) i 10–100 USD za jednorazową konwersję u freelancera. Widać przy tym wyraźną wrażliwość na cenę.

### Cited Findings
- BaseLinker (Base.com): pierwsza hurtownia jest w abonamencie, druga i każda kolejna kosztuje **50 zł netto miesięcznie**. — [base.com pomoc](https://base.com/pl-PL/pomoc/wiedza/hurtownie/); potwierdzenie — [devisu.pl](https://devisu.pl/wdrozenie-baselinker/), [ecommerce-manager.pl](https://ecommerce-manager.pl/14-wybor-hurtowni/)
- Według bloga artursmolicki.com sklep z 300 zamówieniami miesięcznie zapłaci za BaseLinkera 576 zł netto miesięcznie. — [artursmolicki.com](https://artursmolicki.com/blog/baselinker-cennik-integracja-ecommerce/)
- Apilo: podłączenie hurtowni spoza listy kosztuje **od 599 zł netto jednorazowo** (analiza 300 zł płatna z góry plus wdrożenie od 299 zł). — [apilo.com](https://apilo.com/pl/help/podlaczenie-hurtowni-import-xml-csv/)
- Shoper AppStore: istnieją płatne aplikacje integracji z hurtowniami, np. ASI VeroSoft w planie rocznym za 1 hurtownię. Ceny nie udało się odczytać. — [shoper.pl](https://www.shoper.pl/aplikacje/integracja-hurtowniami-verosoft), [lista aplikacji „Hurtownie”](https://www.shoper.pl/appstore-aplikacje/hurtownie)
- syncX Stock Sync: od 7 USD miesięcznie (lub 77 USD rocznie), plus 5 USD za każdy dodatkowy feed. Na stronie widnieje też plan 10 USD miesięcznie dla 1–25 feedów (opis cennika na stronie jest niejednoznaczny). — [Shopify App Store](https://apps.shopify.com/stock-sync)
- Matrixify: Basic 20 USD, wyższy plan około 100 USD (z recenzji) — [Shopify App Store](https://apps.shopify.com/excel-export-import/reviews); dla części użytkowników 50–200 USD miesięcznie to za dużo (snippet) — [Reddit](https://www.reddit.com/r/ShopifyeCommerce/comments/1ll4a0d/alternatives_to_the_matrixify_shopify_app/)
- Sheet2Store: 19 USD za katalog (do 25 stron PDF i 500 wierszy wariantów), 9,90 USD za katalog w pakiecie 10 sztuk, 9 USD za aktualizację cen/stanów. — [sheet2store.com](https://sheet2store.com/)
- Supplier Update Guard: 19 USD jednorazowo, bez odzewu merchantów. — [Shopify Community](https://community.shopify.com/t/review-supplier-csv-prices-before-a-shopify-import-19-once/700040)
- Freelancerzy: Fiverr od 5 do 100 USD, typowo 10–30 USD za konwersję pliku dostawcy — [Fiverr](https://www.fiverr.com/gigs/shopify-csv); Upwork 95 USD za oczyszczenie cennika do 500 wierszy — [Upwork](https://www.upwork.com/services/product/admin-customer-support-a-cleaned-supplier-price-list-with-sku-and-price-checks-2108927896407015122); pakiety Upwork z arkuszami cenowymi po 35, 90 i 200 USD — [Upwork](https://www.upwork.com/services/product/admin-customer-support-a-custom-excel-price-list-and-quotation-workbook-that-does-the-maths-2101739933724500800)
- **Sygnały wrażliwości cenowej:** sprzedawca w Shopware z ograniczonym budżetem na Community Edition, choć gotów zapłacić za działające rozwiązanie (2017) — [Shopware](https://forum.shopware.com/t/lieferanten-artikel-feed-csv-importieren-wer-kann-helfen/43754); WP All Import pro za „kilkaset euro” oceniony jako nieopłacalny — [wordpress.org](https://wordpress.org/plugins/wp-all-import/); przedstawiciel aplikacji konkurencyjnej przyznaje, że 72 USD to „stosunkowo dużo” — [Shopify Community](https://community.shopify.com/t/what-reliable-app-can-replace-stock-sync-for-dropship-stock-updates/192086); sprzedawca na Allegro wybrał darmowe rozszerzenie zamiast BaseLinkera — [Allegro Gadane](https://spolecznosc.allegro.pl/t5/pocz%C4%85tkuj%C4%85cy-sprzedawcy/prosta-aplikacja-aktualizacji-stan%C3%B3w-przez-api/td-p/1022471)
- **Sygnały gotowości do zapłaty:** zleceniodawca na Shoperze pisze o „kosztownych ręcznych aktualizacjach” 15 hurtowni (U2); sprzedawca z PrestaShop od razu pyta o płatny skrypt (E12); zleceniodawca B2B pyta o roczną licencję gotowego konektora (U7).

### Inferences
- Naturalna kotwica cenowa w PL to **50 zł netto miesięcznie za dostawcę** (BaseLinker). Narzędzie za około 29–99 zł miesięcznie dla kilku dostawców byłoby tańsze od BaseLinkera przy 2 lub więcej hurtowniach i od jednorazowego wdrożenia w Apilo (599 zł).
- Jednorazowa konwersja to tani towar (10–30 USD u freelancera). Model subskrypcyjny trzeba uzasadnić cyklicznością: zapamiętanym mapowaniem, diffem i harmonogramem.
- Sheet2Store pokazuje, że rozliczanie za użycie (19 USD za katalog, 9 USD za aktualizację) jest w ogóle testowane na rynku. Nie ma jednak danych, czy się sprzedaje.

### Gaps
- Brak publicznych budżetów w PLN na Useme. Brak ceny aplikacji VeroSoft i innych aplikacji hurtowni na Shoperze.
- Brak danych o przychodach, liczbie klientów ani konwersji konkurentów (Sheet2Store, Koalab), więc nie wiadomo, czy ich ceny się sprawdzają.
- Brak ankiet WTP. Wszystkie wnioski o cenach opierają się na cennikach i pojedynczych wypowiedziach.

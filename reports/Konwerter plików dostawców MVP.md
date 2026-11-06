# Konwerter cenników wygra polskimi plikami, nie technologią

*Raport badawczy: rynek, konkurencja i plan MVP. Stan wiedzy: 6 listopada 2026. Każda teza o rynku, cenach i konkurencji ma link. Szacunki i założenia są wyraźnie oznaczone. Miejsca, których nie udało się potwierdzić, są opisane wprost.*

---

## 1. Podsumowanie w 10 zdaniach

Warto budować, ale nie „kolejny konwerter z AI”. Sensowne jest wąskie narzędzie do **cyklicznej aktualizacji cen i stanów z plików od dostawców spoza list integratorów**, które przed importem pokazuje raport zmian.

Problem istnieje i powtarza się regularnie. Sprzedawcy na forach Shopify, Shopware, PrestaShop i Allegro opisują ręczne dopasowywanie SKU i strach przed nadpisaniem własnych opisów ([Shopify Community](https://community.shopify.com/t/what-do-you-still-fix-by-hand-when-updating-supplier-prices-or-stock/692332), [Allegro](https://spolecznosc.allegro.pl/t5/pocz%C4%85tkuj%C4%85cy-sprzedawcy/prosta-aplikacja-aktualizacji-stan%C3%B3w-przez-api/td-p/1022471)). Zlecenia typu „podłącz hurtownię i aktualizuj ceny z XML” na Useme zbierają od 6 do 58 ofert ([Useme](https://useme.com/pl/jobs/wdrozenie-sklepu-b2b-hurtownia-narzedzi-ogrodniczych-z-indywidualnymi-cennikami,141894/)).

Założenie, że „nikt tego nie robi”, jest nieprawdziwe. **Witly** w Shoper App Store (od 99 zł netto/mies.) importuje dowolne pliki XLS/CSV/XML i zapamiętuje scenariusz dla kolejnych plików ([Witly](https://witly.ai/news/import-produktow)). Za granicą Sheet2Store, OhoSync, Csvio i EmberPrice mają pamięć mapowania i podgląd zmian ([Sheet2Store](https://sheet2store.com/), [OhoSync](https://ohosync.com/), [EmberPrice](https://wordpress.org/plugins/emberprice/)).

Wolne miejsce wciąż jest. W przejrzanych źródłach żadne narzędzie na polskim rynku nie łączy polskich realiów z **czytelnym raportem zmian u dostawcy** i bezpiecznym importem samych zmienionych pól. Polskie realia to netto/brutto przy VAT 23/8/5%, przecinek dziesiętny, polskie nagłówki kolumn i PDF-y od lokalnych dystrybutorów.

Integratorzy (BaseLinker, Apilo, Sky-Shop) dobrze obsługują setki hurtowni ze swoich list. Dostawca spoza listy kosztuje jednak w Base 50 zł/mies. i wymaga planu Business za 279 zł. W Apilo trzeba zapłacić za wdrożenie od 599 zł. Base nie przyjmuje XLS i nie tworzy wariantów przy imporcie z pliku ([Base cennik](https://base.com/pl-PL/cennik/), [Base pomoc](https://base.com/pl-PL/pomoc/wiedza/import-produktow/), [Apilo](https://apilo.com/pl/help/podlaczenie-hurtowni-import-xml-csv/)).

Polska ma ok. **75–143 tys. sklepów** ([D&B przez ewp.pl](https://ewp.pl/liczba-sklepow-internetowych-w-polsce-rosnie-mimo-presji-globalnych-platform/), [ShopRank](https://shoprank.com/countries/poland)). Nie istnieje żadne badanie, które mówi, jaka ich część kupuje od zewnętrznych dostawców. Szacunek 40–70 tys. potencjalnych klientów to więc założenie do sprawdzenia.

Na start polecam **WooCommerce**. Ma największą pulę sklepów w Polsce (51–72 tys.) i publiczny schemat CSV z wariantami ([AfterShip](https://www.aftership.com/ecommerce/statistics/regions/pl), [WooCommerce docs](https://woocommerce.com/document/product-csv-importer-exporter/)). Grupa docelowa to sklepy odsprzedające towar z branż technicznych, które dostają Excel lub PDF od 2–10 dostawców. Drugi wybór to IdoSell, bo sam pobiera plik z adresu URL ([pomoc IdoSell](https://pomoc.idosell.com/towary/webowy-import-aktualizacja-i-przywracanie-towarow/import-i-aktualizacja-towarow-za-pomoca-narzedzia-webowego)).

Proponowana cena to **49 i 99 zł netto/mies.**, czyli mniej niż wejście do Witly i mniej niż BaseLinker przy dwóch lub więcej dostawcach spoza listy. To jednak więcej niż wtyczka WP Desk za 329 zł/rok ([WP Desk](https://www.wpdesk.pl/sklep/dropshipping-xml-woocommerce/)), więc wartość musi wynikać z obsługi XLS/PDF, raportu zmian i braku konfiguracji serwera.

Przed budową trzeba w tydzień przeprowadzić 10 rozmów i sprawdzić Witly oraz Sheet2Store na prawdziwych plikach. Budować warto dopiero wtedy, gdy co najmniej 5 rozmówców przyśle swoje pliki, a co najmniej 3 zgodzą się zapłacić z góry.

Niemcy to rynek większy i lepiej płacący, ale działają tam już REPMOD i Import2Shop. Import2Shop ma polską stronę i kosztuje 69 €/mies. ([REPMOD](https://repmod.de/), [Import2Shop](https://import2shop.com/de/preise/)). Niemcy mają więc sens dopiero jako drugi krok, z przewagą w obsłudze PDF i nieuporządkowanych Exceli oraz z obsługą JTL-Ameise, BMEcat i GPSR.

---

## 2. Tabela konkurencji

Kolumna „Dowolny dostawca” oznacza, że użytkownik może sam zmapować plik dowolnego dostawcy, bez wdrożenia przez producenta narzędzia. Ceny są netto, jeśli nie zaznaczono inaczej. „Brak danych” znaczy, że w badaniu nie udało się tego potwierdzić.

### 2.1 Najbliżsi konkurenci (nowe narzędzia do plików dostawców)

| Nazwa | Platformy docelowe | Dowolny dostawca | Cena | Mocne strony | Słabe strony | Link |
|---|---|---|---|---|---|---|
| **Witly** (PL) | Shoper, WooCommerce, PrestaShop | **Tak** (XLS, XLSX, CSV, XML, JSON) | od 99 zł/mies. z 10 000 kredytów, +100 zł za każde kolejne 10 000; 30 dni testu bez karty | Jest w Shoper App Store. Agent AI pyta o warianty i mapowanie. Ten sam scenariusz stosuje do kolejnych plików i ostrzega o zmianie formatu. | Nie znaleziono informacji o PDF, eksporcie do IdoSell i Allegro ani o raporcie zmian dla sprzedawcy. Nie wiadomo, ile kredytów zużywa jeden import. To szeroki „ekosystem 20 agentów”, a nie narzędzie do jednego zadania. Brak opinii. | [witly.ai/news](https://witly.ai/news/import-produktow), [cennik](https://witly.ai/cennik), [App Store](https://www.shoper.pl/aplikacje/witly) |
| **Sheet2Store** | Shopify, Woo, Amazon, noon, Salla, Zid, Trendyol, Hepsiburada | **Tak** (PDF z tekstem, XLSX, CSV do 20 MB) | $19 za katalog, $49 za 3, $99 za 10, $9 za aktualizację; bez abonamentu | Czyta PDF i wyciąga z niego zdjęcia. Pamięta mapowanie i reguły cen. Aktualizacja zwraca tylko zmienione wiersze. | Nie czyta skanów. Nie obsługuje polskich platform. Brak recenzji. | [sheet2store.com](https://sheet2store.com/) |
| **REPMOD** (DE) | JTL-Ameise, Shopware 6, Woo, Shopify, Plentymarkets, CSV | **Tak** (BMEcat, Datanorm, CSV) | od 89 € za pakiet 5 000 artykułów, bez abonamentu, 250 artykułów gratis | Profile per dostawca, porównanie asortymentu (wycofane artykuły), GPSR, sprawdzanie GS1, warianty | Strona nie wspomina o AI ani o swobodnych plikach PDF/Excel. Nastawiony na Niemcy. | [repmod.de](https://repmod.de/) |
| **Import2Shop** (DE, ma stronę PL) | Shopify, Woo, Shopware, Gambio, PrestaShop, eBay, Amazon, Kaufland | **Tak** (CSV, XML, JSON, API, EDI, FTP) | 69 €/mies. za 1 hurtownię i 1 kanał | Ciągła synchronizacja, reguły cen, przekazywanie zamówień, brak limitu artykułów | Synchronizuje feedy, a nie „dowolny Excel/PDF”. Nie wymienia Shopera, IdoSell ani Allegro. | [import2shop.com](https://import2shop.com/de/preise/) |
| **EmberPrice** | WooCommerce | **Tak** (XLSX, XLS, CSV) | darmowy, wersja Pro planowana | Mapowanie potwierdzane raz dla dostawcy. Podgląd starej i nowej ceny ze zmianą w %. Próg minimalnej ceny i możliwość wycofania zmian. | Mniej niż 10 instalacji. Brak PDF i AI. Stany i harmonogram dopiero w planach. | [wordpress.org](https://wordpress.org/plugins/emberprice/) |
| **OhoSync** (NO) | WooCommerce, Shopify | **Tak** (Excel, CSV, Sheets, **PDF**, XML, API) | €0 / €19 / €29 / €79 miesięcznie | Blokuje zbyt duże skoki cen i update, w którym znika większość produktów. Daje listę zmian. „Ceny ustalają reguły, nie AI”. | Brak recenzji. Nie potwierdzono, czy mapowanie zapisuje się per dostawca. Brak polskich platform. | [ohosync.com](https://ohosync.com/) |
| **Csvio** | Shopify | **Tak** (CSV, Excel, PDF) | darmowy plan; 2¢ za produkt; $19 / $39 / $79 miesięcznie (dane w źródłach niespójne) | AI mapuje kolumny, zapisuje układ pliku, sam buduje warianty, pokazuje podgląd | Tylko Shopify. 0 recenzji. | [Shopify App Store](https://apps.shopify.com/csvio-ai-product-importer) |
| **Upsellr** | PrestaShop, Shopify, Akeneo, CSV/Excel, Amazon, ManoMano, Carrefour | **Tak** (arkusze, PDF) | od 79 €/mies. | Agenci AI. Dane z PDF mają zapisane źródło. | Brak Shopera, IdoSell i Woo. To PIM, czyli narzędzie szersze i droższe. | [upsellr.io](https://www.upsellr.io/pl) |
| **Parabola / Prowork** | ERP (NetSuite, Fulfil), API | **Tak** | 1 000 kredytów za darmo; plan Collaborator ok. $400/mies. (źródło zewnętrzne, niepotwierdzone na stronie Paraboli) | Gotowy szablon: e-mail, AI czyta CSV/Excel/PDF, dopasowanie SKU, **porównanie z poprzednim cennikiem**, kolejka do przeglądu | Zbudowane dla działów zakupów i ERP, nie dla sklepów. Klienci skarżą się na nieprzewidywalny koszt kredytów. | [use case](https://parabola.io/use-cases/vendor-price-list-import), [ceny wg Automation Atlas](https://automationatlas.io/answers/parabola-pricing-explained-2026/), [forum](https://community.parabola.io/t/parabola-pricing-update/1660) |
| **Koalab Sync** | WooCommerce | Tak (Excel, CSV) | plan darmowy i płatne (kwot nie potwierdzono) | Podgląd każdej zmiany, wycofanie całego uploadu | Brak recenzji | [wordpress.org](https://wordpress.org/plugins/koalab-sync/) |
| **MicrocityLabs** (UK) | Shopify, Woo, Odoo, Xero, QuickBooks, Sage, Zoho, Amazon | Tak (PDF, Excel, CSV, **skany i zdjęcia z telefonu**) | od £15 za plik | Pamięta każdego dostawcę. Każdą wartość da się prześledzić do strony źródłowej. | Raport zmian nie jest wspomniany. Brak polskich platform. | [microcitylabs.com](https://microcitylabs.com/) |
| **Supplier Update Guard** | Shopify | CSV | $19 jednorazowo | Przegląd cen przed importem | Brak reakcji sprzedawców na ofertę | [Shopify Community](https://community.shopify.com/t/review-supplier-csv-prices-before-a-shopify-import-19-once/700040) |
| **SellStar** (PL, PIM) | wiele, w tym Shoper i IdoSell | Tak (PIM) | 159 / 299 / 599 zł mies. | AI mapuje kategorie, raport pominiętych pozycji | Obsługi XLS i PDF nie zweryfikowano. PIM to więcej niż konwerter. | [cennik](https://sellstar.pl/cennik/) |

### 2.2 Integratorzy i platformy w Polsce

| Nazwa | Platformy | Dowolny dostawca | Cena | Mocne strony | Słabe strony | Link |
|---|---|---|---|---|---|---|
| **BaseLinker / Base.com** | marketplace'y; sklep tylko pośrednio | **Częściowo**: hurtownie z listy (ponad 400), dowolny CSV, XML tylko w znanej strukturze (np. Ceneo) | 0 zł do 100 zamówień; 279 zł + 0,99 zł za zamówienie; każda hurtownia spoza Base Connect po pierwszej: 50 zł/mies. (tylko w planie Business) | Ponad 400 hurtowni, Base Connect, mnożniki cen, ponad 30 tys. klientów | Nie przyjmuje XLS. Import z pliku nie tworzy wariantów. „Nie ma możliwości” zintegrowania hurtowni ze sklepem. Fala skarg na podwyżki (wzrosty o 300–1100%). | [cennik](https://base.com/pl-PL/cennik/), [hurtownie](https://base.com/pl-PL/pomoc/wiedza/hurtownie/), [import](https://base.com/pl-PL/pomoc/wiedza/import-produktow/), [Allegro](https://spolecznosc.allegro.pl/t5/zaawansowani-sprzedawcy/alternatywa-dla-baselinker-podwy%C5%BCka-od-stycznia-i-enterprise-od/td-p/882117) |
| **Apilo** (grupa Shoper) | Shoper, Allegro, PrestaShop (przez CSV) i inne | **Nie**: hurtownia spoza listy wymaga wdrożenia od 599 zł; ogólne pliki Ceneo i IOF działają bez wdrożenia | Starter 39 zł; w Shoperze 99 zł/mies. za 3 hurtownie albo 649 zł/rok za 1; każda kolejna 45–59 zł/mies. | Ok. 400 hurtowni, filtry, narzut, oficjalna ścieżka Shopera | Dane z hurtowni pobierane 3 razy dziennie. Brak typu „wariant”. Produkty trafiają do sklepu przez CSV lub formularz. Wdrożeniowiec opisał ciche błędy: import ze statusem OK i zerem produktów. | [pomoc](https://apilo.com/pl/help/podlaczenie-hurtowni-import-xml-csv/), [porównanie aplikacji](https://apilo.com/pl/help/aplikacja-integracje-z-hurtowniami-czy-dropshipping-modul-apilo-co-wybrac/), [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/) |
| **Sellasist** | sklepy, marketplace'y | brak danych | 59–899 zł/mies.; hurtownie wyceniane osobno | Ponad 200 hurtowni, tańszy od Base przy dużym wolumenie | Mało intuicyjny panel | [EcomFlowLab](https://ecomflowlab.pl/baselinker-podrozal-migracja-apilo-sellasist/) |
| **Sky-Shop** | tylko Sky-Shop | **Nie** (lista ok. 580 hurtowni) | moduł hurtowni 49–319 zł/mies. | Najwięcej gotowych integracji, wysyłka zamówień do hurtowni | Działa tylko na własnej platformie. Brak informacji o podpięciu dowolnego pliku. | [sky-shop.pl](https://sky-shop.pl/cennik-modul-integracji-z-hurtowniami/) |
| **IdoSell (IAI) Downloader** | tylko IdoSell | **Tak** (CSV, XML, IOF; nietypowy XML wymaga sterownika XSLT) | brak danych | Narzędzie wbudowane, pobiera z URL i FTP, IdoSell jest autorem standardu IOF | XLS trzeba najpierw przerobić na CSV/XML. Nietypowy XML wymaga XSLT. Wokół narzędzia działa rynek usług (mhajok, PrePIM). | [pomoc](https://pomoc.idosell.com/towary/iai-downloader/integracja-z-hurtownia), [mhajok](https://mhajok.pl/import-produktow-idosell) |
| **Sellpander** | nakładka na BaseLinkera | Tak (XML/CSV z linku) | brak danych | Dowolna hurtownia w Base | Strona z 2021 r., ostatnia zmiana 04.2024 | [sellpander.pl](https://www.sellpander.pl/integracja-z-hurtownia/) |

### 2.3 Wtyczki i moduły dla platform

| Nazwa | Platformy | Dowolny dostawca | Cena | Mocne strony | Słabe strony | Link |
|---|---|---|---|---|---|---|
| **WP All Import** | WooCommerce, WordPress | **Tak** (XML, CSV, XLS/XLSX, Sheets, ZIP) | $169–299/rok; licencja dożywotnia $1 299 | Ponad 100 tys. instalacji, ocena 4,7/5 z 1 966 recenzji | Brak PDF, AI i porównania zmian. Skargi na paywall („import do Woo jest płatny”) i na UX. | [wordpress.org](https://wordpress.org/plugins/wp-all-import/), [ceny](https://www.wpallimport.com/pricing/) |
| **WebToffee Product Import Export** | WooCommerce | Tak (w wersji Premium: CSV, XML, Excel, Sheets) | $69 / $129 / $249 rocznie | Szablon mapowania, FTP, cron, 80 tys. instalacji | Darmowa wersja obsługuje tylko CSV, bez wariantów. Skargi „bez płacenia bezużyteczna”. | [webtoffee.com](https://www.webtoffee.com/product/product-import-export-woocommerce/), [opinie](https://wordpress.org/support/plugin/product-import-export-for-woo/reviews/?filter=1) |
| **WP Desk Dropshipping Import** (PL) | WooCommerce | **Tak** (XML, CSV) | 329 zł/rok (PRO, 1 strona) | Polska firma. Mapowanie przeciągnij-i-upuść, warianty, marża, harmonogram, decyzja co zrobić z produktami, które zniknęły z pliku. | Nie obsługuje XLS ani PDF. Wymaga hostingu i crona. Ocena 4,3 z 11 recenzji. | [wpdesk.pl](https://www.wpdesk.pl/sklep/dropshipping-xml-woocommerce/), [wordpress.org](https://wordpress.org/plugins/dropshipping-xml-for-woocommerce/) |
| **PrestaShow Importer** (PL) | PrestaShop | **Tak** (XML, CSV, API) | 650,41 / 1 300,81 zł jednorazowo | Kombinacje, CRON, 82 recenzje | Konfiguracja techniczna. Brak informacji o XLS i PDF. | [prestashow.pl](https://prestashow.pl/pl/moduly-prestashop/5-prestashop-importer-integracja-z-hurtowniami-xml-csv-api.html) |
| **x13 Import hurtowni** (PL) | PrestaShop | **Nie**: „Integracja nie jest uniwersalna” | 399 zł (licencja roczna) | AI do opisów, kombinacje | Przygotowywany pod konkretny plik | [x13.pl](https://x13.pl/integracje-prestashop/import-xml-do-prestashop.html) |
| **ELEGANTAL Easy Import** | PrestaShop | **Tak** (CSV, XLS, XLSX, XML, JSON, ODS…) | $149,99 | Ocena 4,9 z 110. Zapisane reguły, formuły cen, wykrywa i pomija niezmieniony plik. | Brak PDF. Nie porównuje cen produkt po produkcie. | [Addons](https://addons.prestashop.com/de/datentransfer-backup/24523-easy-import-products-from-csv-excel-xml-json-txt.html) |
| **MyPrestaModules Catalog Import** | PrestaShop | Tak (CSV, XLSX, XML) | nie odczytano | Ocena 4,6 z 180, testowy import próbki | Brak PDF | [Addons](https://addons.prestashop.com/fr/transfert-sauvegarde-donnees/19091-catalogue-de-produits-csv-excel-dimportation.html) |
| **Store Commander** | PrestaShop (wersja Shopify od $29,99) | konfigurowalny import CSV | 9,99 / 39,99 / 79,99 mies. | Masowa edycja back-office | To nie jest konwerter cenników. Nie wiadomo, które plany mają import. | [licencje](https://my.storecommander.com/fr/content/45-licences-store-commander) |
| **Shopware 6 Import/Export** (wbudowany) | Shopware | Tylko CSV według profili | w cenie platformy | Profile mapowania | Brak XLS, XML i PDF. Warianty wymagają UUID-ów. | [docs.shopware.com](https://docs.shopware.com/en/shopware-en/settings/importexport) |
| **Shopware Import/Export (SW5)** | Shopware 5.7 | Tylko CSV | darmowy | — | Ocena 2,8/5, wsparcie 0,2/5, brak następcy | [Shopware Store](https://store.shopware.com/en/swagef36a3f0ee25/shopware-import-export.html) |
| **Kommora Import Export Pro** | Shopware 6 | Tak (CSV, XLSX, XML) | €49,90/mies. lub €499/rok | Próbny import z raportem błędów, harmonogram | Mniej niż 10 pobrań, nic o dostawcach | [Shopware Store](https://store.shopware.com/en/kommo52751045368m/import-export-pro-csv-xlsx-xml-import-export.html) |
| **Firebear Improved Import** | Shopware | Tak (CSV, XML, XLSX, Sheets) | 75 €/mies. lub 675 €/rok | Zapisane mapowanie dostawcy, harmonogram, FTP | Ocena 4,33 z 26. Recenzja: „Bekommen wir nicht zum Laufen” („nie możemy tego uruchomić”). | [Shopware Store](https://store.shopware.com/en/fireb81914862032m/improved-import-export-mass-actions.html) |
| **Synesty** (DE, iPaaS) | Shopware, JTL, PlentyONE, marketplace'y | Tak (narzędzie no-code) | od 99 €/mies. | Elastyczny | Narzędzie ogólne, trzeba je skonfigurować | [synesty.com](https://synesty.com/de/pricing/) |
| **excodata** (AT/DE) | sklep lub ERP | Tak, jako usługa (Excel, CSV, PDF, BMEcat) | 290 € lub 490 € jednorazowo; 99 €/mies. | Usługa obejmuje PDF | To usługa, nie samoobsługowe narzędzie | [excodata.com](https://www.excodata.com/en/) |
| **syncX: Stock Sync** | Shopify | **Tak** (CSV, XLSX, XML, JSON) | $0 / $7 / $10 mies., dodatkowy feed $5–7 | Ocena 4,8 z 940, bardzo tani | Brak PDF. Skargi: czytał zły arkusz Excela, mapował złe kolumny, słabe wsparcie. | [App Store](https://apps.shopify.com/stock-sync), [opinie 1–2★](https://apps.shopify.com/stock-sync/reviews?ratings%5B%5D=1&ratings%5B%5D=2) |
| **Matrixify** | Shopify | własny format | $20 / $50 / $200 mies. | Ocena 4,9 z 1 872 | Trudny do opanowania. Dla części użytkowników za drogi. | [App Store](https://apps.shopify.com/excel-export-import) |
| **Syncee** | Shopify | marketplace dostawców | $39,99–99,99 mies. | — | To nie jest konwerter plików | [App Store](https://apps.shopify.com/syncee-1) |
| **Odoo, Softhealer** | Odoo | **Nie** (sztywny szablon kolumn) | $21,25 | Tani, cron, logi | Kolumn nie wolno przestawiać | [Odoo Apps](https://apps.odoo.com/apps/modules/18.0/sh_import_supplier_info/) |
| **MAVRui** | OpenCart | Tak | $37, **wycofany ze sprzedaży** (ostatnia wersja 10.2023) | Raport nowych produktów, zmian cen i stanów | Już niedostępny | [OpenCartForum](https://opencartforum.com/en/files/file/1479-avtomaticheskoe-obnovlenie-cen-na-sayte-iz-excel-i-xml-praysov-postavschikov-mavrui) |
| **usergio „Suppliers”** | OpenCart | Tak (XML, CSV, XLS) | 1 776 UAH | Ocena 4,9 z 628, czyli duży popyt | Rynek UA/RU, w Polsce nisza | [OpenCartForum](https://opencartforum.com/en/files/file/811-avtomatychna-obrobka-prais-lystiv/) |
| **Eofferix** | Ozon, partnerzy | Tak (CSV, XLS/XLSX, XML, zapisane profile) | **nie udało się potwierdzić** (strona zwracała błąd 503) | Profile przetwarzania, harmonogram | Skupiony na Ozonie. PDF, AI i porównanie zmian niepotwierdzone. | [docs](https://eofferix.com/docs/mapping-fields), [Ozon](https://eofferix.com/price-list-to-ozon) |

**Wniosek z tabeli.** Rynek dzieli się na trzy grupy. Pierwsza to integratorzy z listą hurtowni: dostawca spoza listy oznacza u nich wdrożenie albo pisanie kodu. Druga to wtyczki per platforma: są elastyczne i tanie, ale wymagają wiedzy technicznej i nie czytają PDF. Trzecia to nowa fala narzędzi AI, z których prawie wszystkie celują w Shopify i Woo po angielsku. Raport „co zmienił dostawca”, przygotowany pod polskie realia, w przejrzanych źródłach nie występuje u nikogo w Polsce. Najbliżej są EmberPrice (WooCommerce, bez AI i PDF) oraz Parabola (ERP, ok. $400/mies.) ([EmberPrice](https://wordpress.org/plugins/emberprice/), [Parabola](https://parabola.io/use-cases/vendor-price-list-import)). **Największe zagrożenie w Polsce to Witly**: ten sam kanał sprzedaży, ta sama cena i ta sama obietnica zapamiętania scenariusza. To, czego u Witly nie znaleziono (PDF, IdoSell, Allegro, raport zmian), trzeba sprawdzić na darmowym okresie testowym, zanim zacznie się budować.

---

## 3. Dowody potrzeby

Oznaczenia: **[CYKLICZNY]** to ból powtarzalny (ceny i stany co godzinę, dzień, tydzień lub miesiąc). **[JEDNORAZOWY]** to migracja albo założenie katalogu. **[MIESZANY]** to oba naraz. Wszystkie opisy są parafrazami. Wątków z Reddita nie dało się otworzyć (blokada 403), więc opisy pochodzą z fragmentów w wyszukiwarce i nie mają dat.

### 3.1 Fora i społeczności

- **[CYKLICZNY]** Shopify Community, 10.2026. Sprzedawca z kilkoma tysiącami SKU od wielu dostawców wylicza, co poprawia ręcznie: warianty kasowane przy imporcie, utracone formuły Excela, wymaganą kolumnę Title nawet przy zmianie samej ceny. Inny uczestnik chce aktualizować tylko koszt i stan, a brakujące, nowe i mocno zmienione wiersze oznaczać do przeglądu. Wątek założył inny founder, który sprawdzał podobny pomysł. To dowód problemu, ale też sygnał, że rośnie konkurencja. [link](https://community.shopify.com/t/what-do-you-still-fix-by-hand-when-updating-supplier-prices-or-stock/692332)
- **[CYKLICZNY]** Shopify Community, 06.2024. Sprzedawca codziennie dostaje CSV z ponad 5 000 produktów i boi się, że import cen nadpisze jego własne tytuły. [link](https://community.shopify.com/t/import-csv-updating-variant-price-and-variant-inventory-qty-without-overwriting-title/333334)
- **[CYKLICZNY]** Shopify Community, 2022. Cenniki XLSX od dostawców. Ręczne wyszukiwanie każdego SKU przy ponad 10 000 SKU zajmuje godziny. [link](https://community.shopify.com/t/how-can-i-efficiently-update-prices-using-a-csv-file/138448)
- **[CYKLICZNY + skarga na konkurencję]** Shopify Community, 2023. Dostawca co kilka godzin przysyła arkusz, a ceny zsynchronizowane przez Stock Sync nie zgadzają się z tym arkuszem. [link](https://community.shopify.com/t/what-reliable-app-can-replace-stock-sync-for-dropship-stock-updates/192086)
- **[CYKLICZNY]** Shopify Community, 2024. Aktualizacja stanów, gdy plik ma tylko SKU, bez identyfikatora Handle. Jeden z podlinkowanych wątków (DE, 2022) opisuje dostawcę, który aktualizuje plik co 15 minut. [link](https://community.shopify.com/t/update-shopify-stock-levels-via-csv-with-no-handle-only-sku/306346)
- **[CYKLICZNY]** Allegro, społeczność, 05.2025. Sprzedawca z ok. 1 300 ofertami aktualizuje stany 2–4 razy dziennie z pliku CSV. Wprost odrzuca „kobyły typu BaseLinker”, a rozwiązaniem okazuje się darmowe rozszerzenie do przeglądarki. [link](https://spolecznosc.allegro.pl/t5/pocz%C4%85tkuj%C4%85cy-sprzedawcy/prosta-aplikacja-aktualizacji-stan%C3%B3w-przez-api/td-p/1022471)
- **[CYKLICZNY]** Forum PrestaShop (PL), 2022. Hurtownia ma 70 tys. pozycji, a sklep sprzedaje 3 tys. z nich. Sprzedawca chce aktualizować tylko ilości i od razu pyta, czy może zapłacić za skrypt. [link](https://forum.prestashop.com/topic/1070349-aktualizacja-ilo%C5%9Bci-wybranych-produkt%C3%B3w-csv/)
- **[MIESZANY]** Forum PrestaShop (data nieznana). Dostawcy dają tylko XML, a Presta importuje CSV. [link](https://forum.prestashop.com/topic/339861-import-pliku-xml-baza-produkt%C3%B3w/)
- **[CYKLICZNY]** Forum Shopware, 2023/2024. Import cen wymaga podania i netto, i brutto, a po imporcie w ponad 1 500 produktach zrywa się automatyczne powiązanie netto–brutto. [link](https://forum.shopware.com/t/korrektes-importieren-von-preisen/99189)
- **[MIESZANY]** Forum Shopware, 2017. Plik dostawcy ma 13 800 wierszy i 34 kolumny o nazwach niepasujących do pól sklepu. Sprzedawca ma mały budżet, ale deklaruje, że zapłaci za rozwiązanie, które działa. [link](https://forum.shopware.com/t/lieferanten-artikel-feed-csv-importieren-wer-kann-helfen/43754)
- **[CYKLICZNY]** Forum Shopware, 2017. Pliki dostawcy nie mają numeru artykułu, więc trzeba dopasowywać po EAN, kilka razy dziennie. [link](https://forum.shopware.com/t/lieferantendaten-mit-import-export-advanced-importieren/44507)
- **[CYKLICZNY]** Forum Shopware, 2022. Excel od producenta trzeba łączyć z danymi sklepu po EAN. Odpowiedź: „robimy to dość często”, przez VLOOKUP. [link](https://forum.shopware.com/t/import-von-produktdaten-in-shopware-abgleich-und-vereinen-zweier-excel-dateien-mit-uebereinstimmenden-zeilen-auf-basis-ean/95391)
- **[CYKLICZNY]** Forum JTL, 06.2026. Sprzedawca z 10 tys. artykułów chce co godzinę przeliczać ceny według dostawców. Obchodzi problem skryptem w Pythonie i importem przez JTL-Ameise. Inny użytkownik radzi importować tylko różnice, czyli dokładnie to, co robiłby raport zmian. [link](https://forum.jtl-software.de/threads/arbeiten-mit-lieferanten-eks-workflows-und-sql.247773/)
- **[CYKLICZNY]** Reddit r/shopify. Część dostawców przysyła PDF zamiast CSV. [link](https://www.reddit.com/r/shopify/comments/1fjiwcb/how_do_you_manage_thousands_of_items_from/)
- **[CYKLICZNY]** Reddit r/ShopifyeCommerce. Matrixify za 50–200 USD/mies. „za sam import” to według użytkownika przesada. [link](https://www.reddit.com/r/ShopifyeCommerce/comments/1ll4a0d/alternatives_to_the_matrixify_shopify_app/)
- **[CYKLICZNY, rynek sąsiedni B2B]** Reddit r/supplychain. Co tydzień przychodzi 40-stronicowy PDF albo nieuporządkowany Excel z podwyżką 5–8%. [link](https://www.reddit.com/r/supplychain/comments/1sbsqil/how_is_everyone_handling_these_constant/)
- **Inni founderzy sprawdzający podobny pomysł:** Reddit r/ShopifyApps pyta o narzędzie porównujące stary i nowy CSV dostawcy ([link](https://www.reddit.com/r/ShopifyApps/comments/1x0uuok/would_you_use_a_tool_that_compares_supplier_csv/)). Podobnie r/InventoryManagement ([link](https://www.reddit.com/r/InventoryManagement/comments/1v2b0fx/how_do_you_deal_with_messy_supplier_spreadsheets/)).

**Luka w danych:** forum.shoper.pl, społeczność IdoSell, grupy na Facebooku, wykop i elektroda nie zwróciły trafnych wyników. Te miejsca są słabo indeksowane, więc trzeba je przejrzeć ręcznie.

### 3.2 Zlecenia freelancerskie

- **[CYKLICZNY]** Useme, 03.2024, 18 ofert. Sklep na Shoperze z ok. 15 hurtowniami potrzebuje codziennej aktualizacji nazw, cen, stanów i zdjęć ze stałą marżą. Właściciel chce uniknąć „żmudnych i kosztownych” ręcznych aktualizacji. [link](https://useme.com/pl/jobs/api-aplikacja-do-importu-danych-z-15-hurtowni-do-sklepu-shoper,93003/)
- **[MIESZANY]** Useme, 07.2026, **58 ofert**. Sklep B2B na WooCommerce z narzędziami ogrodniczymi. Ok. 2 400 indeksów z XML producenta i **cykliczna aktualizacja cen zakupu**. Zleceniodawca pyta o roczną licencję gotowego konektora. [link](https://useme.com/pl/jobs/wdrozenie-sklepu-b2b-hurtownia-narzedzi-ogrodniczych-z-indywidualnymi-cennikami,141894/)
- **[MIESZANY]** Useme, 07.2025, 10 ofert. Sklep Shopify z butami: XML z hurtowni, rozmiary jako warianty, marża, aktualizacja stanów. Zleceniodawca deklaruje, że nie zna się na technice. [link](https://useme.com/pl/jobs/sklep-na-shopify-integracja-z-hurtownia-plik-xml,118834/)
- **[CYKLICZNY]** Useme, 07.2024, 6 ofert. Opony. Apilo przyjmuje IOF, a hurtownie dają CSV na FTP, więc potrzebna jest konwersja. [link](https://useme.com/pl/jobs/podaczenie-zewnetrznych-hurtowni-do-apilo,99669/)
- **[CYKLICZNY]** Useme, 05.2025, 19 ofert. Niespójne pliki CSV z dostaw trzeba automatycznie przekształcać. [link](https://useme.com/pl/jobs/konwertowanie-plikow-csv,115168/)
- **[JEDNORAZOWE ustawienie cyklicznej synchronizacji]** Useme, 11.2025, 17 ofert. BaseLinker połączony z kilkoma hurtowniami i Shopify. [link](https://useme.com/pl/jobs/integracja-baselinker-z-hurtowniami-zewnetrznymi-i-sklepem-shopify,125873/)
- **[JEDNORAZOWY]** Useme, 11.2022, 6 ofert. Ujednolicenie XML-i i konwersja do CSV dla PrestaShop, Shopera i WooCommerce. [link](https://useme.com/pl/jobs/poszukujemy-osoby-do-konwersji-plikow-xml-do-csv-i-pozniejsze-wdrozenie-do-sklep,69230/)
- **[CYKLICZNY]** Useme, 2022. IdoSell, 3 hurtownie, aktualizacja co dobę. [link](https://useme.com/pl/jobs/integracja-hurtowni-ze-sklepem-na-idosell-za-posrednictwem-iai-downloader,67286/)
- **[CYKLICZNY]** Useme (data nieznana). Integracja z hurtownią, w której kolejny import **nie może nadpisywać opisów i tytułów**. [link](https://useme.com/pl/jobs/integracja-sklepu-internetowego-z-hurtownia-csv-lub-webapi,25364/)
- **[CYKLICZNY]** Freelancehunt (UA), 66 ofert. Sklep z częściami samochodowymi ma 4 dostawców i każdy przysyła inny Excel: artykuł w innej kolumnie, ceny raz w USD, raz w UAH. [link](https://freelancehunt.com/project/skript-na-python-chtobyi-svodit-praysyi/1661107.html)
- **[CYKLICZNY]** Freelancehunt, 13 ofert. Cenniki w różnych formatach trzeba sprowadzić do jednego CSV. [link](https://freelancehunt.com/project/sdelat-avtomaticheskuyu-obrabotku-raznoobraznyih-praysov/1573246.html)
- **[JEDNORAZOWY]** Fiverr. Gigi „convert any supplier file into Shopify/WooCommerce CSV” kosztują od 5 do 100 USD, zwykle 10–30 USD. [link](https://www.fiverr.com/gigs/shopify-csv), [przykład za 100 USD](https://www.fiverr.com/hossainzabed/reshape-supplier-excel-file-into-bulk-csv-listing-to-upload-any-website)
- **[CYKLICZNY, usługa ręczna]** Upwork. Za 95 USD freelancer czyści cennik do 500 wierszy ([link](https://www.upwork.com/services/product/admin-customer-support-a-cleaned-supplier-price-list-with-sku-and-price-checks-2108927896407015122)). Inny pakiet to **ręczne porównanie starego i nowego cennika** z oznaczeniem zmian cen oraz nowych i usuniętych pozycji ([link](https://www.upwork.com/services/product/admin-customer-support-i-will-compare-old-and-new-supplier-price-lists-and-flag-changes-2108322491870819321)). Ludzie płacą więc za ręczne wykonanie dokładnie tej funkcji, którą chcesz zautomatyzować.

**Luka w danych:** budżety we wszystkich 9 sprawdzonych zleceniach Useme są ukryte („Do negocjacji”). Budżety klientów na Upwork wymagają logowania.

### 3.3 Opinie o konkurencji

- **[CYKLICZNY]** BaseLinker. Wątek na Społeczności Allegro (10.2024–12.2025) opisuje wzrost kosztów o 300–1100% po zmianie cennika i system „przeładowany funkcjami” ([link](https://spolecznosc.allegro.pl/t5/zaawansowani-sprzedawcy/alternatywa-dla-baselinker-podwy%C5%BCka-od-stycznia-i-enterprise-od/td-p/882117)). W Capterrze minusy to wysoki koszt dla małych firm i słaby import wariantów ([link](https://www.capterra.com/p/245981/Base/)).
- **[CYKLICZNY]** Apilo. Wdrożeniowiec opisuje import ze statusem OK i zerem produktów, brak logów, brak typu „wariant” oraz 17 tys. produktów bez zdjęć bez żadnego komunikatu o błędzie ([link](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/)). Po przejściu z Base najczęstsza skarga brzmi: „i tak trzeba dokupić synchronizację” ([link](https://ecomflowlab.pl/baselinker-podrozal-migracja-apilo-sellasist/)).
- **[CYKLICZNY]** WP All Import. Recenzje jednogwiazdkowe mówią, że darmowa wersja jest bezużyteczna, że import do Woo jest płatny i że wersja Pro dobrze działa tylko na świeżych danych, a gorzej przy aktualizacjach ([link](https://wordpress.org/support/plugin/wp-all-import/reviews/?filter=1)).
- **[CYKLICZNY]** syncX Stock Sync. Aplikacja czytała zły arkusz Excela, przez co ceny na żywo były błędne. Kolumny mapowały się na złe dane, a błędy synchronizacji prowadziły do sprzedaży towaru, którego nie było ([link](https://apps.shopify.com/stock-sync/reviews?ratings%5B%5D=1&ratings%5B%5D=2)).
- **[MIESZANY]** WebToffee. Skargi: „bezużyteczna bez płacenia”, brak wariantów w darmowej wersji, wtyczka zepsuła stronę ([link](https://wordpress.org/support/plugin/product-import-export-for-woo/reviews/?filter=1)).
- **[CYKLICZNY]** Matrixify. Użytkownik zapłacił za plan za $20, a aplikacja wymusiła przejście na plan za ok. $100 ([link](https://apps.shopify.com/excel-export-import/reviews)).
- **[CYKLICZNY]** Parabola. Klienci obawiają się, że model kredytów będzie „nieprzewidywalny i drogi przy wzroście” ([link](https://community.parabola.io/t/parabola-pricing-update/1660)).

**Co z tego wynika.** Przeważa ból **cykliczny**. Jednorazowe konwersje pojawiają się głównie jako tanie gigi na Fiverr. Ludzie rzadko piszą „nie umiem przekonwertować formatu”. Częściej piszą: „chcę zaktualizować **część pól** dla **części produktów**, nie psując reszty”. Bezpieczeństwo, czyli podgląd, raport zmian i zasada „nie zeruj tego, czego brak w pliku”, jest dla sprzedawców ważniejsze niż sama konwersja.

---

### 3A. Wielkość rynku: TAM i SAM z jawnymi założeniami

**Polska.** Liczba sklepów zależy od tego, co się liczy. Firm zarejestrowanych jako e-sklep jest **prawie 75 tys.** Netto przybyło ich ok. 2,4 tys. w 2025 r. (dane D&B) ([ewp.pl](https://ewp.pl/liczba-sklepow-internetowych-w-polsce-rosnie-mimo-presji-globalnych-platform/), [pro.rp.pl](https://pro.rp.pl/raporty-ekonomiczne/art43687641-polacy-radza-sobie-z-chinczykami-codziennie-powstaje-szesc-nowych-e-sklepow)). Narzędzia skanujące technologię stron widzą **ok. 143,6 tys.** domen sklepowych z dostawą fizyczną ([ShopRank, XI 2026](https://shoprank.com/countries/poland)).

Podział według platform ze skanów:

- **WooCommerce: 51,1–72,1 tys.**
- **PrestaShop: 16,5–17,4 tys.**
- **Shoper: 13,6–15,4 tys.** Spółka podaje, że obsługuje „ponad 20 tys. e-sklepów”.
- **Shopify: 9,2–14,5 tys.**
- **IdoSell: 3–4 tys.** Spółka podaje, że ma „blisko 8 tys.” sklepów.
- **Sky-Shop: ok. 2,2 tys.**

Źródła: [ShopRank](https://shoprank.com/countries/poland), [AfterShip](https://www.aftership.com/ecommerce/statistics/regions/pl), [Shoper IR](https://investors.shoper.pl/en/press-office/wyniki-finansowe-q4-2025---komunikat), [IAI](https://www.iai-sa.com/pl/o-iai/). Różnice między skanami a danymi spółek najpewniej wynikają z tego, że spółki liczą całe grupy, rozwiązania white-label i sklepy bez własnej domeny. To wniosek, nie fakt.

Obok sklepów działa **ok. 160 tys. sprzedawców na Allegro** ([xyz.pl](https://xyz.pl/pko-bp-i-allegro-zmieniaja-zasady-gry-milion-nowych-klientow-i-15-mld-zl-finansowania-dla-sprzedawcow/), [EuroEcom](https://euroecom.com/blog/allegro-explained-why-over-150000-merchants-trust-this-fast-growing-marketplace/)) i **ponad 30 tys. klientów Base.com** ([xyz.pl](https://xyz.pl/base-sebastiana-kulczyka-kupil-firme-szefa-pko-bp-uwolni-miedzynarodowy-potencjal-polskich-sprzedawcow/)). Te grupy w dużej części pokrywają się ze sklepami, więc nie należy ich sumować.

**Jaki odsetek sklepów kupuje od zewnętrznych dostawców? Nie udało się tego potwierdzić.** Nie znaleziono żadnego badania ani dla Polski, ani dla Niemiec. Jedyna liczba to globalne 27% sklepów, dla których dropshipping jest głównym modelem. Podaje ją agregator dostawcy dropshippingu, bez opisanej metodologii ([SaleHoo](https://www.salehoo.com/learn/dropshipping-market-size)).

Pośrednie przesłanki istnieją. Większość firm z PKD 47.91 z definicji odsprzedaje towar. Base ma integracje z ponad 400 hurtowniami ([base.com](https://base.com/pl-PL/pomoc/wiedza/czym-jest-base-com/)), a Sky-Shop z ok. 580 ([sky-shop.pl](https://sky-shop.pl/cennik-modul-integracji-z-hurtowniami/)). To dowodzi, że przypadek jest masowy, ale nie daje twardej liczby.

| Poziom | Obliczenie | Wynik | Status |
|---|---|---|---|
| Sklepy w PL | 75 tys. (firmy) do 143 tys. (domeny); wartość środkowa 100 tys. | ok. 100 tys. | źródła powyżej, wartość środkowa to **założenie** |
| Odsetek sklepów pracujących na plikach dostawców | 40–70% | — | **założenie, niepotwierdzone** |
| **TAM PL (liczba sklepów)** | 100 tys. × 40–70% | **40–70 tys. sklepów** | obliczenie |
| **TAM PL (wartość)** | 40–70 tys. × 720–1 200 zł/rok (60–100 zł/mies.) | **ok. 29–84 mln zł/rok** | obliczenie; przychód na klienta to **założenie** oparte na cenach Witly, Apilo i BaseLinkera |
| SAM: WooCommerce PL | 51–72 tys. × 40–70% | ok. 20–50 tys. | obliczenie |
| SAM po zawężeniu | × 20–40% (sklepy z ponad 300 SKU i co najmniej jednym dostawcą spoza list integratorów) | **ok. 4–20 tys. sklepów** | **założenie** |
| **SAM (wartość)** | 4–20 tys. × 720–1 200 zł | **ok. 2,9–24 mln zł/rok** | obliczenie |
| Cel na 12 miesięcy dla jednej osoby | 100–300 płacących × ok. 60 zł/mies. | **ok. 72–216 tys. zł przychodu rocznego (ARR)** | **cel, nie prognoza** |
| Alternatywny SAM: platformy SaaS w PL | Shoper + IdoSell + Sky-Shop + ShopGold | 25–35 tys. sklepów | obliczenie z danych skanów |

**Jak to czytać.** Rynek wystarczy dla jednoosobowego biznesu na poziomie dziesiątek lub setek tysięcy złotych rocznie. Nie jest to jednak „wielki rynek”. Rozrzut szacunków jest szeroki, bo kluczowego założenia (40–70%) nikt dotąd nie zmierzył. Pierwsze rozmowy z klientami powinny je zweryfikować.

**Niemcy (skrót, szczegóły w 3F).** Skany pokazują **ok. 412 tys.** witryn sklepowych. WooCommerce ma ok. 111 tys., Shopify ok. 110 tys., Shopware 20–25 tys., a JTL-Shop i Gambio razem ok. 12,4 tys. ([AfterShip DE](https://www.aftership.com/ecommerce/statistics/regions/de), [Store Leads](https://storeleads.app/reports/shopware)). W bazie Listflix jest **62 734** firm sklasyfikowanych jako sklepy internetowe ([Listflix](https://listflix.de/statistik/online-shops/)). Na Amazon.de ma działać ok. 240 tys. sprzedawców, ale to źródło wtórne bez ustalonego pochodzenia ([mediasprout](https://www.mediasprout.de/amazon-statistiken/)).

### 3B. Bolączki: ranking (częstotliwość razy dotkliwość)

Ranking opiera się na liczbie i jakości ok. 40 znalezionych wzmianek, a nie na ankiecie.

| # | Bolączka | Częstotliwość | Dotkliwość | Typ | Dowody |
|---|---|---|---|---|---|
| 1 | **Częściowa aktualizacja bez nadpisywania własnych treści.** Brak wiersza w pliku nie może oznaczać usunięcia produktu ani zerowego stanu. | częsta | **bardzo wysoka**, bo grozi zepsuciem sklepu | cykliczny | [Shopify](https://community.shopify.com/t/import-csv-updating-variant-price-and-variant-inventory-qty-without-overwriting-title/333334), [Useme](https://useme.com/pl/jobs/integracja-sklepu-internetowego-z-hurtownia-csv-lub-webapi,25364/) |
| 2 | **Dopasowanie do własnych produktów** (SKU dostawcy a własne, EAN, 70 tys. pozycji w pliku przy 3 tys. w sklepie, nowe i wycofane pozycje) | bardzo częsta | wysoka | cykliczny | [PrestaShop](https://forum.prestashop.com/topic/1070349-aktualizacja-ilo%C5%9Bci-wybranych-produkt%C3%B3w-csv/), [Shopware](https://forum.shopware.com/t/lieferantendaten-mit-import-export-advanced-importieren/44507) |
| 3 | **Inny układ kolumn u każdego dostawcy** | bardzo częsta | wysoka | cykliczny | [Freelancehunt](https://freelancehunt.com/project/skript-na-python-chtobyi-svodit-praysyi/1661107.html), [Shopware](https://forum.shopware.com/t/lieferanten-artikel-feed-csv-importieren-wer-kann-helfen/43754) |
| 4 | **Ciche błędy i zmiany układu pliku** (import z OK i zerem produktów, zły arkusz Excela, nowy plik od hurtowni, który wymaga nowego konektora) | częsta | **bardzo wysoka**, bo błąd wychodzi dopiero u klienta | cykliczny | [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/), [syncX](https://apps.shopify.com/stock-sync/reviews?ratings%5B%5D=1&ratings%5B%5D=2), [Shoper App Store („nowy plik” i „stary plik”)](https://www.shoper.pl/aplikacje/integracje-z-hurtowniami) |
| 5 | **Marża i reguły cen** (cena zakupu, sugerowana albo detaliczna, stała marża, zaokrąglenia do X,90) | częsta | wysoka | cykliczny | [Useme](https://useme.com/pl/jobs/api-aplikacja-do-importu-danych-z-15-hurtowni-do-sklepu-shoper,93003/), [JTL](https://forum.jtl-software.de/threads/arbeiten-mit-lieferanten-eks-workflows-und-sql.247773/) |
| 6 | **Netto czy brutto, VAT, cennik detaliczny zamiast zakupowego.** Tylko 1 z 5 dostawców oznaczył to wprost, a pomyłka przesuwa ceny o 23%. | średnia | **bardzo wysoka**, bo bezpośrednio uderza w marżę | cykliczny | [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/), [Shopware](https://forum.shopware.com/t/korrektes-importieren-von-preisen/99189) |
| 7 | **Warianty i rozmiary** (rozmiar zapisany w nazwie, „ROZM. 43”; 4 667 pozycji złożonych w 1 069 kart produktów) | średnia, wysoka w odzieży i obuwiu | wysoka | mieszany | [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/), [Useme](https://useme.com/pl/jobs/sklep-na-shopify-integracja-z-hurtownia-plik-xml,118834/) |
| 8 | **Jakość danych** (60 zdublowanych EAN, 165 pustych, przesunięte kolumny, stan „TAK” czytany jako 1 sztuka) | średnia | średnia do wysokiej | cykliczny | [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/) |
| 9 | Kategorie i atrybuty | średnia | średnia | głównie jednorazowy | [Useme](https://useme.com/pl/jobs/wdrozenie-sklepu-b2b-hurtownia-narzedzi-ogrodniczych-z-indywidualnymi-cennikami,141894/) |
| 10 | Konwersja XML na CSV i odwrotnie | średnia | średnia | mieszany | [Useme](https://useme.com/pl/jobs/podaczenie-zewnetrznych-hurtowni-do-apilo,99669/) |
| 11 | **PDF zamiast Excela** | rzadsza w e-commerce, częstsza w B2B | wysoka, gdy występuje | cykliczny | [Reddit](https://www.reddit.com/r/shopify/comments/1fjiwcb/how_do_you_manage_thousands_of_items_from/), [Reddit B2B](https://www.reddit.com/r/supplychain/comments/1sbsqil/how_is_everyone_handling_these_constant/) |
| 12 | Waluta, jednostki (karton, paleta, metr na sztuki), kodowanie znaków | sporadyczna | średnia | mieszany | [Freelancehunt](https://freelancehunt.com/project/skript-na-python-chtobyi-svodit-praysyi/1661107.html), [Shopify](https://community.shopify.com/t/what-do-you-still-fix-by-hand-when-updating-supplier-prices-or-stock/692332), [polskapresta](https://polskapresta.pl/index.php?topic=505.0) |
| 13 | Zdjęcia (za małe dla Allegro; w jednym pliku tylko 46% pozycji ma zdjęcia) | średnia | średnia | mieszany | [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/) |

**Najbardziej bolesne są punkty 1, 4 i 6.** Nie chodzi w nich o wygodę, tylko o ryzyko realnej straty: zły import, nieświadoma utrata marży albo błąd, który wychodzi dopiero u klienta. Dlatego sednem produktu powinien być **raport zmian z bezpiecznikami**, a nie sama „konwersja formatu”. Problem kodowania Windows-1250 w plikach polskich hurtowni nie znalazł świeżego potwierdzenia.

### 3C. Ceny i gotowość do zapłaty

Polscy sprzedawcy już płacą za podłączenie dostawców:

- **BaseLinker:** 50 zł/mies. za każdą hurtownię spoza Base Connect po pierwszej, przy planie Business za 279 zł + 0,99 zł za zamówienie ([Base](https://base.com/pl-PL/cennik/)).
- **Apilo:** 99 zł/mies. za 3 hurtownie w Shoperze albo 649 zł/rok za 1. Wdrożenie hurtowni spoza listy kosztuje **od 599 zł jednorazowo** ([Apilo](https://apilo.com/pl/help/podlaczenie-hurtowni-import-xml-csv/), [Shoper App Store](https://www.shoper.pl/aplikacje/integracje-z-hurtowniami)).
- **Aplikacja dla jednej hurtowni (Incom):** 189 zł/mies. ([Shoper](https://www.shoper.pl/aplikacje/integracja-z-incom)).
- **Sky-Shop:** 49–319 zł/mies. za moduł hurtowni ([Sky-Shop](https://sky-shop.pl/cennik-modul-integracji-z-hurtowniami/)).
- **Witly:** od 99 zł/mies. ([Witly](https://witly.ai/cennik)).
- **SellStar:** od 159 zł/mies. ([SellStar](https://sellstar.pl/cennik/)).

Po drugiej stronie są tanie wtyczki: **WP Desk za 329 zł/rok** ([WP Desk](https://www.wpdesk.pl/sklep/dropshipping-xml-woocommerce/)), **WebToffee za $69/rok** ([WebToffee](https://www.webtoffee.com/product/product-import-export-woocommerce/)) i moduły PrestaShop za **399–1 300 zł jednorazowo** ([x13](https://x13.pl/integracje-prestashop/import-xml-do-prestashop.html), [PrestaShow](https://prestashow.pl/pl/moduly-prestashop/5-prestashop-importer-integracja-z-hurtowniami-xml-csv-api.html)).

Na Zachodzie widełki są podobne. Stock Sync kosztuje **$7–10/mies.** ([App Store](https://apps.shopify.com/stock-sync)), OhoSync **€19–79** ([OhoSync](https://ohosync.com/)), Sheet2Store **$19 za katalog i $9 za aktualizację** ([Sheet2Store](https://sheet2store.com/)). Freelancerzy biorą **10–30 USD** za jednorazową konwersję na Fiverr ([Fiverr](https://www.fiverr.com/gigs/shopify-csv)) i **95 USD** za oczyszczenie cennika na Upwork ([Upwork](https://www.upwork.com/services/product/admin-customer-support-a-cleaned-supplier-price-list-with-sku-and-price-checks-2108927896407015122)).

Widać też wrażliwość na cenę. Sprzedawca na Allegro wybrał darmowe rozszerzenie zamiast BaseLinkera ([Allegro](https://spolecznosc.allegro.pl/t5/pocz%C4%85tkuj%C4%85cy-sprzedawcy/prosta-aplikacja-aktualizacji-stan%C3%B3w-przez-api/td-p/1022471)). Wersję Pro WP All Import za „kilkaset euro” recenzent uznał za nieopłacalną ([wordpress.org](https://wordpress.org/plugins/wp-all-import/)).

**Jaki model zadziała.** Jednorazowa konwersja to tani towar, więc abonament broni się tylko wtedy, gdy praca się powtarza: mapowanie jest zapamiętane, raport zmian pokazuje różnice, później dochodzi harmonogram. Naturalną polską kotwicą jest „**50 zł za dostawcę miesięcznie**” z BaseLinkera. Abonament 49–99 zł za kilku dostawców jest od niej wyraźnie tańszy, a jednocześnie mieści się w zakresie, za który sprzedawcy SaaS już płacą.

Rozliczanie za użycie, jak w Sheet2Store, warto dodać jako opcję jednorazową, bo część bólu ma charakter jednorazowy. **Nie wiadomo, czy ceny Sheet2Store i Witly się sprawdzają.** Brak danych o ich przychodach, a ankiet gotowości do zapłaty nie znaleziono. Budżety na Useme są ukryte.

### 3D. Technika: formaty importu według platform

| Platforma | Format importu | Warianty | Klucz dopasowania | Kodowanie i separator | Zdjęcia | Netto czy brutto | API i limity | Czy wystarczy sam plik? |
|---|---|---|---|---|---|---|---|---|
| **WooCommerce** | CSV, wbudowany importer; publiczny schemat kolumn | `Type=variable` i `variation` z kolumną `Parent`; od wersji 11.1 jeden plik, jeśli rodzic stoi przed wariantami | ID lub SKU; od 11.2 także GTIN/EAN | UTF-8, przecinek; kategorie oddzielone `>` | URL pobierane do biblioteki mediów | dokumentacja milczy; zależy to od ustawień sklepu (niepotwierdzone) | REST API; limitów partii nie potwierdzono | **Tak**, pełny katalog i aktualizacje |
| **PrestaShop 8/9** | CSV, XLS, XLSX, ODS | **osobny plik kombinacji** | „Use product reference as key” | UTF-8 (lub ISO-8859-1), średnik | absolutne URL | kolumna ceny bez podatku lub z podatkiem (do sprawdzenia na instancji) | Webservice; limitów nie potwierdzono | **Tak**, ale potrzebne są dwa pliki |
| **Shoper** | CSV według „profili” („Aktualizacja”, „Aktualizacja, dodawanie”) | **CSV nie obejmuje wariantów** (źródło nieoficjalne); stanami wariantów zarządza się osobną aplikacją | `product_code` (jest też profil z kodem kreskowym) | UTF-8, średnik lub tabulator | `images 1…n` jako URL | nie udało się potwierdzić | REST: kubełek 10 operacji, 2 operacje/s, bulk do 25 | **Częściowo**: proste produkty i ceny tak, warianty praktycznie przez API |
| **IdoSell** | **IOF 3.0 XML** (full, light) i CSV; narzędzie webowe | IOF obsługuje rozmiary (szczegółów elementów nie potwierdzono) | kod zewnętrzny, kod producenta, ID | brak danych | nadpisywanie lub dogrywanie | brak danych | Admin API; limitów nie potwierdzono | **Tak**: **pobiera plik z URL cyklicznie**, więc prawie jak integracja bez API |
| **Allegro** | „Importuj i wystaw” (CSV lub link, do 50 MB) i „Wystaw z pliku” (do 10 000 ofert, 5 MB); **tylko konta firmowe** | przez Katalog Allegro | GTIN/EAN, MPN | CSV | `IMAGES` z separatorem `\|` lub `IMAGE1–16` | **`PRICE` brutto** | REST API: nowy regulamin od 23.09.2025, kara 50 000 zł za udostępnienie kluczy, 20 tys. nowych produktów w katalogu miesięcznie | **Tak**, także masowa edycja cen i ilości |
| **Shopware 6** | CSV według profili (UTF-8, średnik) | wymaga UUID-ów (`parent_id`, `optionIds`) | `productNumber` (niepotwierdzone dla profilu domyślnego) | UTF-8, średnik; przecinek dziesiętny psuje import | rozszerzenie profilu | trzeba podać i netto, i brutto | Admin API; limitów nie potwierdzono | **Warunkowo**: ceny i stany tak, warianty trudne |
| **Base.com** (jako cel pośredni) | dowolny CSV; XML tylko w znanej strukturze | **import nie tworzy wariantów** | — | — | — | — | API | Tak, dla produktów prostych |

Źródła: [WooCommerce](https://woocommerce.com/document/product-csv-importer-exporter/), [PrestaShop 8](https://docs.prestashop-project.org/v.8-documentation/user-guide/configuring-shop/advanced-parameters/import), [Shoper, Vinson Agency](https://vinson.agency/blog/import-produktow-do-shopera-z-pliku-csv-instrukcja-krok-po-kroku), [Shoper Learn: warianty](https://www.shoper.pl/learn/artykul/zarzadzanie-plikami-csv-grupowe-dodawanie-producenta), [Shoper API](https://developers.shoper.pl/docs/), [IdoSell import](https://pomoc.idosell.com/towary/webowy-import-aktualizacja-i-przywracanie-towarow/import-i-aktualizacja-towarow-za-pomoca-narzedzia-webowego), [IOF](https://www.idosell.com/pl/developers/otwarte-standardy-i-api-do-integracji/internet-offer-format-iof-/dokumentacja-internet-offer-format-iof/), [Allegro pomoc](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku), [Allegro regulamin API](https://developer.allegro.pl/rules), [Allegro, limit katalogu](https://github.com/allegro/allegro-api/issues/11793), [Shopware](https://docs.shopware.com/en/shopware-en/settings/importexport), [Firebear](https://firebearstudio.com/blog/ultimate-guide-to-shopware-6-import.html), [Base](https://base.com/pl-PL/pomoc/wiedza/import-produktow/).

**Czy można zacząć od samego pliku wyjściowego? Tak, i to jest właściwa decyzja.** WooCommerce, PrestaShop, IdoSell i Allegro dają się w pełni obsłużyć plikiem. Shopware tylko przy prostych aktualizacjach. Shoper jest najsłabszy przy wariantach, a jego API przy 2 operacjach na sekundę nie jest „darmowym” kanałem: 5 000 aktualizacji pojedynczo zajmie ok. 40 minut (obliczenie z limitu w [dokumentacji](https://developers.shoper.pl/docs/)).

API Allegro niesie dodatkowo ryzyko regulaminowe. Dostęp do części funkcji wymaga programu partnerskiego albo co najmniej 100 użytkowników aplikacji ([regulamin](https://developer.allegro.pl/rules)). Codzienną aktualizację najlepiej później rozwiązać **plikiem pod stałym URL**. IdoSell pobiera go natywnie, a Allegro przyjmuje link.

**Koszty przetwarzania.**

- **Mapowanie przez model językowy** (nagłówki i ok. 20 wierszy, ok. 5 tys. tokenów wejścia i 1 tys. wyjścia): ok. **$0,001** na Haiku 5.5 i **$0,02** na Sonnet 5.5. To obliczenie z cennika Claude według notatek badawczych (stan 10.2026) ([Claude pricing](https://platform.claude.com/docs/en/about-claude/pricing)).
- **PDF:** Docling wypada najlepiej w benchmarkach tabel (F1 0,85–0,94, wobec 0,19–0,38 dla pdfplumber) ([arXiv 2511.16134](https://arxiv.org/html/2511.16134v2)) i działa lokalnie, więc praktycznie nic nie kosztuje. Mistral OCR kosztuje **$4 za 1 000 stron, w trybie wsadowym $2** ([Mistral](https://mistral.ai/news/ocr-4/)). 20-stronicowy cennik to ok. $0,08 (wsadowo $0,04). Azure Layout kosztuje $10 za 1 000 stron ([Azure](https://azure.microsoft.com/en-us/pricing/details/document-intelligence/)), a Textract Tables $15 ([AWS](https://aws.amazon.com/textract/pricing/)).
- **Uwaga:** nie znaleziono żadnego benchmarku dla polskich cenników hurtowych (polskie znaki, scalone komórki, tabele na wielu stronach).

### 3E. Prawo

**Zdjęcia i opisy.** Profesjonalne zdjęcia i twórcze opisy producenta są zwykle utworami. Zakup towaru w hurcie **nie daje licencji** na ich publikację ([Kancelaria Lech](https://znakitowarowe-blog.pl/zdjecia-i-opisy-produktow-od-producenta/)). Prosty packshot może nie być utworem ([Lege Artis, 2019](https://czasopismo.legeartis.org/2019/11/prawa-autorskie-zdjec-produktow-fotografia-packshot-utwor-wyrok/)). Katalog dostawcy może dodatkowo podlegać ochronie baz danych na mocy dyrektywy 96/9/WE ([EUR-Lex](https://eur-lex.europa.eu/eli/dir/1996/9/oj)). Zakresu tej ochrony w badaniu nie analizowano.

Wniosek dla produktu: regulamin powinien przenosić odpowiedzialność za prawa do treści na użytkownika. Narzędzie powinno **przekazywać linki URL do zdjęć zamiast kopiować je na własne serwery**. Nie znaleziono orzecznictwa o odpowiedzialności dostawcy SaaS, który tylko konwertuje pliki.

**RODO.** Cenniki co do zasady nie zawierają danych osobowych. Mogą się w nich jednak pojawić dane kontaktowe handlowców albo jednoosobowej firmy wskazanej jako producent w polach GPSR ([wytyczne KE dot. GPSR](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=OJ:C_202506233)). Minimum na start to regulamin, polityka prywatności, wzór umowy powierzenia (art. 28 [RODO](https://eur-lex.europa.eu/eli/reg/2016/679/oj)), hosting w UE i dostawcy LLM/OCR wpisani jako dalsi podmioty przetwarzające. Nie potwierdzono, czy Claude, Mistral i Gemini przetwarzają dane w regionie UE. Ta dziedzina spełnia warunek foundera „bez wrażliwych danych osobowych”.

**GPSR.** Rozporządzenie stosuje się od 13.12.2024. Każda oferta online musi podawać producenta, osobę odpowiedzialną w UE (gdy producent jest spoza UE), identyfikator produktu i ostrzeżenia ([EUR-Lex C/2025/6233](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=OJ:C_202506233), [Händlerbund](https://www.haendlerbund.de/de/ratgeber/recht/produktsicherheitsverordnung)). Allegro ma na to osobne pola w API i w narzędziu plikowym ([GitHub allegro-api](https://github.com/allegro/allegro-api/issues/11793), [Allegro pomoc](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku)). W Niemczech pierwsze upomnienia za brak tych danych pojawiły się w maju 2025 ([xictron](https://www.xictron.com/de/blog/gpsr-produktsicherheitsverordnung-online-shop-2026/)). **Dane GPSR zapamiętane per producent w profilu dostawcy** to prawnie uzasadniona funkcja dodatkowa.

**Omnibus.** Przy każdej informacji o obniżce sklep musi pokazać najniższą cenę z 30 dni ([UOKiK](https://uokik.gov.pl/storage/archiwum/e6e552a1.pdf)). UOKiK aktywnie stawia zarzuty, w 2026 r. m.in. Zalando i Temu ([UOKiK](https://uokik.gov.pl/tag/dyrektywa-omnibus)). Snapshoty cen w narzędziu dają naturalnie historię cen. Narzędzie powinno ostrzegać, gdy użytkownik ustawia „cenę promocyjną” z pola dostawcy.

**Regulaminy platform.** API Allegro: kara 50 000 zł za udostępnienie kluczy, zakaz scrapingu, utrata dostępu po 90 dniach bez używania aplikacji ([regulamin](https://developer.allegro.pl/rules)). To kolejny argument, żeby zacząć od pliku. Warunków API i App Store dla Shopera i IdoSell nie udało się potwierdzić.

### 3F. Rynek niemiecki

**Problem w Niemczech jest ten sam i lepiej udokumentowany.** Fora Shopware i JTL opisują ręczny VLOOKUP po EAN, skrypty w Pythonie podawane do JTL-Ameise i potrzebę importu samych różnic ([JTL 2026](https://forum.jtl-software.de/threads/arbeiten-mit-lieferanten-eks-workflows-und-sql.247773/), [Shopware 2022](https://forum.shopware.com/t/import-von-produktdaten-in-shopware-abgleich-und-vereinen-zweier-excel-dateien-mit-uebereinstimmenden-zeilen-auf-basis-ean/95391)). Gotowość do zapłaty jest wyższa: Firebear kosztuje **56–75 €/mies.**, Import2Shop **69 €/mies.**, Synesty **od 99 €**, a usługi excodata **290–490 € jednorazowo** ([Firebear](https://store.shopware.com/en/fireb81914862032m/improved-import-export-mass-actions.html), [Import2Shop](https://import2shop.com/de/preise/), [Synesty](https://synesty.com/de/pricing/), [excodata](https://www.excodata.com/en/)).

**Konkurencja jest jednak znacznie silniejsza.** REPMOD to niemal dokładnie ten sam pomysł: profile per dostawca, porównanie asortymentu, GPSR, cele JTL, Shopware, Woo i Shopify, od 89 € za 5 tys. artykułów ([REPMOD](https://repmod.de/)). Import2Shop ma **polską wersję strony**, więc konkuruje już na rynku startowym ([Import2Shop](https://import2shop.com/de/preise/)).

Wejście do Niemiec wymaga lokalnych elementów:

- parserów BMEcat i Datanorm ([onveda](https://www.onveda.de/en/blog/bmecat), [REPMOD Datanorm](https://repmod.de/datanorm-in-csv-umwandeln)),
- eksportu do **JTL-Ameise**, bo średnie firmy często importują do systemu magazynowego, a nie do sklepu ([JTL-Guide](https://guide.jtl-software.com/jtl-wawi/jtl-ameise/artikeldaten-importieren/)),
- ceny jednostkowej według PAngV ([gesetze-im-internet](https://www.gesetze-im-internet.de/pangv_2022/BJNR492110021.html)),
- pól GPSR,
- obsługi klienta po niemiecku.

Na niemieckim Reddicie i platformach freelance nie znaleziono dowodów popytu. To luka w badaniu, a nie dowód braku popytu.

**Werdykt:** Niemcy tak, ale jako drugi krok, najwcześniej po 6–12 miesiącach. Warunek: produkt w Polsce musi wypracować przewagę, której REPMOD i Import2Shop nie mają, czyli dobre działanie na PDF i nieuporządkowanych Excelach oraz raport zmian z akceptacją. Kolejność wejścia: Shopware lub JTL-Ameise i pakiet „GPSR + Grundpreis”. Amazon.de odłożyć, bo szablonów flat file nie zweryfikowano.

---

## 4. Wybór niszy startowej

### Rekomendacja: **WooCommerce + sklep odsprzedający towar z branży technicznej z 2–10 dostawcami spoza list integratorów**

Profil klienta: sklep na WooCommerce (B2C lub B2B) z **300–10 000 SKU** w branżach takich jak narzędzia, ogród, instalacje i budowlanka, motoryzacja, BHP i chemia, artykuły biurowe. Dostaje od producentów i dystrybutorów **Excel, CSV albo PDF mailem**, raz w tygodniu lub w miesiącu, i ręcznie przenosi zmiany cen i stanów. Główny przypadek użycia to **cykliczna aktualizacja cen i stanów istniejących produktów plus dodawanie nowych produktów prostych**.

| Kryterium | WooCommerce | IdoSell | Shoper | Allegro | PrestaShop |
|---|---|---|---|---|---|
| Liczba sklepów w PL | **51–72 tys.** | 3–8 tys. | 14–20 tys. | ok. 160 tys. sprzedawców | 16,5–17,4 tys. |
| Najbliższa konkurencja | Wtyczki techniczne bez PDF i raportu zmian; EmberPrice bez trakcji; Witly, Sheet2Store i OhoSync bez polskich realiów | **Nie znaleziono konkurenta AI**; wbudowany Downloader | **Witly w tym samym App Store za 99 zł**; oficjalnie Apilo | BaseLinker, Apilo (lista hurtowni) | Wiele modułów po 400–1 300 zł jednorazowo |
| Łatwość eksportu z samego pliku | **Najwyższa** (publiczny schemat, warianty, GTIN) | Wysoka, ale IOF i CSV niepotwierdzone szczegółowo | Niska przy wariantach; API 2 operacje/s | Średnia (parametry kategorii, EAN) | Średnia (dwa pliki) |
| Czy da się postawić sklep testowy za darmo i od razu? | **Tak** (open source) | Wymaga konta lub okresu testowego | Wymaga konta lub okresu testowego | Wymaga konta firmowego | Tak |
| Wartość raportu zmian, PDF i netto/brutto | Wysoka | Wysoka | Wysoka | Wysoka; GPSR najważniejszy | Wysoka |

**Uzasadnienie.**

Po pierwsze, **najprościej to zbudować**. Schemat CSV WooCommerce jest publiczny i kompletny: warianty przez `Parent`, dopasowanie po SKU, a od wersji 11.2 także po GTIN ([WooCommerce docs](https://woocommerce.com/document/product-csv-importer-exporter/)). Sklep testowy postawisz w godzinę, a jedna osoba bez dostępu do platform SaaS przetestuje poprawność na prawdziwych importach.

Po drugie, **pula sklepów jest największa**, 51–72 tys. ([ShopRank](https://shoprank.com/countries/poland), [AfterShip](https://www.aftership.com/ecommerce/statistics/regions/pl)). Właśnie z tej grupy pochodzi zlecenie z największą liczbą ofert w badaniu (58 ofert, narzędzia ogrodnicze, cykliczne ceny zakupu) ([Useme](https://useme.com/pl/jobs/wdrozenie-sklepu-b2b-hurtownia-narzedzi-ogrodniczych-z-indywidualnymi-cennikami,141894/)).

Po trzecie, **konkurencja na Woo jest liczna, ale żadna nie odpowiada polskiemu klientowi**. WP Desk nie czyta XLS ani PDF i wymaga crona ([WP Desk](https://www.wpdesk.pl/sklep/dropshipping-xml-woocommerce/)). WP All Import i WebToffee nie mają PDF ani raportu zmian. Sheet2Store i OhoSync nie znają polskiego VAT ani polskich nagłówków. Witly obsługuje Woo, ale nie znaleziono u niego raportu zmian ani PDF.

Po czwarte, **branże techniczne to świadome cięcie zakresu**. Mają mało wariantów (inaczej niż odzież i obuwie, gdzie 4 667 pozycji składa się w 1 069 kart produktów ([EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/))). Częściej dostają PDF i Excele od producentów niż feedy XML od dużych hurtowni dropshippingowych. Takie hurtownie są już obsłużone przez ponad 400 integracji w Base i ok. 580 w Sky-Shop.

Po piąte, **przewaga polegająca na „polskich platformach” przesuwa się na „polskie pliki”**. Wejście, czyli polski Excel, PDF i netto/brutto, jest trudne i unikalne. Wyjście to tylko „writer”, który można później dodać dla IdoSell, Allegro i Shopera.

**Dlaczego nie Shoper na start?** To najmocniejszy kontrargument: sprzedawcy Shopera są nietechniczni, nie mogą instalować wtyczek, płacą za aplikacje, a App Store to gotowy kanał sprzedaży. Mimo to Shoper jest dziś **najbardziej zajętym** miejscem. Witly działa tam za 99 zł z zapamiętanym scenariuszem ([App Store](https://www.shoper.pl/aplikacje/witly)), a Apilo jest oficjalną ścieżką. Do tego CSV Shopera według jedynego znalezionego źródła nie obsługuje wariantów ([Vinson](https://vinson.agency/blog/import-produktow-do-shopera-z-pliku-csv-instrukcja-krok-po-kroku)), a pełnej specyfikacji kolumn nie ma publicznie. Shoper warto rozważyć w wersji 2, jeśli test Witly pokaże wyraźne luki.

**Dlaczego nie Allegro na start?** Pula jest ogromna, a import z pliku jest oficjalny i ma pola GPSR. Jednak produkty bez EAN wymagają kompletnych parametrów kategorii, a dziedzinę dobrze obsługują BaseLinker i Apilo. Allegro to idealny **drugi format wyjściowy**, bo tam GPSR i ceny brutto (`PRICE`) mają największe znaczenie ([Allegro pomoc](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku)).

### Drugi wybór: **IdoSell + plik pod stałym URL**

IdoSell sam cyklicznie pobiera plik CSV lub IOF z adresu URL ([pomoc IdoSell](https://pomoc.idosell.com/towary/webowy-import-aktualizacja-i-przywracanie-towarow/import-i-aktualizacja-towarow-za-pomoca-narzedzia-webowego)). Można więc dać doświadczenie „podłącz i zapomnij” bez API i bez certyfikacji aplikacji. Na tej platformie nie znaleziono konkurenta AI.

Klienci IdoSell to średnie i duże sklepy ([MCI](https://mci.pl/mci-sprzedaje-grupe-iai-globalnemu-funduszowi-montagu-private-equity)), które prawdopodobnie zapłacą więcej. Wokół Downloadera działa rynek płatnych usług ([mhajok](https://mhajok.pl/import-produktow-idosell), [PrePIM](https://prepim.eu/integracje/hurtownie/idosell/)). Minusy: pula jest mała (3–8 tys.), szczegółów IOF i CSV nie udało się potwierdzić, a sklep testowy wymaga konta.

**Kiedy zamienić kolejność:** jeśli w walidacji co najmniej 3 z 10 rozmówców będą na IdoSell, a sprzedawcy z WooCommerce okażą się zadowoleni z WP All Import lub WP Desk.

---

## 5. Plan MVP

### 5.1 Zakres

**Główna funkcja, w jednym zdaniu:** „Wgraj nowy plik od dostawcy, a dostaniesz raport, co się zmieniło, i gotowy plik CSV do WooCommerce, który zmienia tylko to, co ma się zmienić.”

**W MVP:**

- Wejście: XLSX, XLS, CSV (wykrywanie kodowania UTF-8, Windows-1250 i ISO-8859-2, separatora i przecinka dziesiętnego) oraz XML o płaskiej strukturze. **PDF z warstwą tekstową jako beta**, z limitem stron.
- Wykrywanie wiersza nagłówka i arkusza w Excelu. Zła zakładka to znany błąd syncX ([opinie](https://apps.shopify.com/stock-sync/reviews?ratings%5B%5D=1&ratings%5B%5D=2)).
- Propozycja mapowania kolumn od modelu językowego, z poziomem pewności dla każdego pola, i ekran potwierdzenia.
- **Profil dostawcy**: mapowanie, reguły cen (netto/brutto, VAT, narzut, zaokrąglenie), mapa stanów tekstowych („TAK”, „>10”), przelicznik jednostek, z wersjonowaniem.
- Dopasowanie do sklepu: użytkownik wgrywa eksport produktów z WooCommerce (wbudowany eksporter). Dopasowanie po SKU, potem EAN, potem aliasach zapamiętanych ręcznie.
- **Raport zmian**: nowe produkty, zniknięte produkty, zmiany cen w zł i %, zmiany stanów, flagi ryzyka. Akceptacja lub odrzucenie zbiorcze i pojedyncze.
- **Bezpieczniki**: zatrzymanie, gdy liczba wierszy spadnie o ponad 30%, zmiana ceny przekroczy próg, cena wyjdzie poniżej ceny zakupu albo pojawi się duplikat EAN.
- Eksport w dwóch trybach: **(a) „Aktualizacja”** — tylko kolumny ID/SKU, ceny i stanu; **(b) „Nowe produkty”** — pełne wiersze produktów prostych, zdjęcia jako URL. Do sprawdzenia testem na instancji: czy importer WooCommerce przy aktualizacji naprawdę nie zmienia pól, których nie ma w pliku. Dokumentacja tego wprost nie mówi.
- Historia importów i snapshoty, czyli przy okazji archiwum cen pomocne przy Omnibusie.

**Świadomie poza MVP:**

- integracje API (Woo REST, Shoper, Allegro),
- harmonogram i pobieranie pliku z URL lub maila (wersja 1.1),
- eksport do IdoSell, Allegro, Shopera, PrestaShop i Shopware,
- grupowanie wariantów (rozmiar i kolor) poza prostym przypadkiem,
- OCR skanów,
- generowanie opisów przez AI,
- pobieranie i hostowanie zdjęć,
- pola GPSR (wersja 2, razem z Allegro),
- przekazywanie zamówień do dostawcy,
- wielu użytkowników na koncie,
- rynek niemiecki.

### 5.2 Przepływ użytkownika krok po kroku

1. **Rejestracja** (e-mail lub Google) i wybór platformy (na start tylko WooCommerce) oraz trybu cen w sklepie: „ceny wpisuję z VAT” albo „bez VAT”.
2. **Wgranie eksportu produktów ze sklepu** (CSV z wbudowanego eksportera WooCommerce). Narzędzie zapamiętuje SKU, EAN, ceny i stany jako stan wyjściowy.
3. **Dodanie dostawcy** („Hurtownia X”) i wgranie jego pliku.
4. **Analiza pliku**: wykrycie formatu, kodowania, arkusza i wiersza nagłówka. Podgląd pierwszych 20 wierszy.
5. **Propozycja mapowania**: każda kolumna ma zielony, żółty lub czerwony znacznik pewności. Narzędzie wykrywa podpowiedzi, np. „kolumna C ≈ kolumna B × 1,23, więc B to netto, a C to brutto”. Użytkownik potwierdza albo poprawia pola żółte i czerwone.
6. **Reguły cen**: którą cenę brać (zakupu czy sugerowaną), narzut %, zaokrąglenie (np. do ,99), stawka VAT (z kolumny albo stała), minimalna marża. Podgląd przeliczenia na 5 produktach.
7. **Dopasowanie**: X dopasowanych, Y nowych, Z niedopasowanych, z kolejką do ręcznego przypisania. Przypisanie zapisuje się jako alias.
8. **Raport zmian**: zakładki „Ceny ↑ / ↓”, „Stany”, „Nowe”, „Zniknęły” i „Flagi”. Domyślne zachowanie dla produktów, które zniknęły z pliku: stan 0 albo bez zmian, do wyboru per dostawca.
9. **Pobranie plików** `aktualizacja.csv` i `nowe.csv` z krótką instrukcją importu w WooCommerce (Produkty → Import → zaznacz „Aktualizuj istniejące”).
10. **Przy następnym pliku od tego dostawcy** narzędzie porównuje odcisk nagłówków. Jeśli się zgadza, kroki 4–7 dzieją się automatycznie i od razu widać raport zmian. Jeśli się nie zgadza, narzędzie pokazuje, co się zmieniło w układzie, i proponuje poprawione mapowanie jako nową wersję profilu.

### 5.3 Stack do vibecodingu i obsługa plików z modelem językowym

Poniższy stack to rekomendacja inżynierska. Konkretne biblioteki pochodzą z ogólnej wiedzy i nie były weryfikowane źródłami w tym badaniu.

- **Frontend i aplikacja:** Next.js (TypeScript) z gotowymi komponentami (np. shadcn/ui). Dobrze generuje się w narzędziach do vibecodingu.
- **Backend danych:** Supabase w regionie UE (Postgres, logowanie, magazyn plików).
- **Worker do plików:** Python z FastAPI na hostingu w UE.
  - pandas z openpyxl (XLSX) i xlrd (stary XLS),
  - lxml (XML),
  - charset-normalizer (kodowanie; dla polskich plików dodatkowa heurystyka rozróżniająca Windows-1250 i ISO-8859-2 po częstości „ą, ś, ź”),
  - Docling do PDF.
- **Płatności:** Stripe albo polska bramka i system faktur.

**Zasada podziału pracy: model językowy proponuje, kod przelicza.**

1. **Deterministyczny parser** zawsze działa przed modelem językowym. Zamienia plik w tabelę i wylicza „podpis” każdej kolumny: typ, odsetek wartości liczbowych, odsetek wartości wyglądających jak EAN (z sumą kontrolną), przykładowe wartości.
2. **Model językowy dostaje** nagłówki, podpisy kolumn, 15–20 wierszy próbki i listę pól docelowych. Zwraca JSON zgodny ze schematem (structured outputs: `output_config.format` lub `strict: true`, [Claude docs](https://platform.claude.com/docs/en/build-with-claude/structured-outputs)): `target_field → source_column`, transformację, pewność i uzasadnienie. Literatura z 2025 r. pokazuje, że metody oparte na modelach językowych przewyższają podobieństwo wektorowe w dopasowywaniu schematów ([LLMatch](https://arxiv.org/html/2507.10897v1)). Pomaga podawanie próbek wartości i agregowanie kilku odpowiedzi ([ACM 2025](https://dl.acm.org/doi/full/10.1145/3737412.3743490)).
3. **Transformacja jest w 100% w kodzie**: przeliczenia netto i brutto, narzuty, zaokrąglenia, jednostki, mapy stanów. Model językowy nigdy nie liczy cen. To ten sam argument zaufania, którego używa OhoSync: „ceny ustalają reguły, nie AI” ([OhoSync](https://ohosync.com/)).
4. **PDF:** najpierw Docling lokalnie dla PDF z tekstem. Jeśli ekstrakcja się nie uda, Mistral OCR ($2–4 za 1 000 stron, [Mistral](https://mistral.ai/news/ocr-4/)). Po każdej ekstrakcji walidacja liczby wierszy, typów i wartości ujemnych, a wiersze o niskiej pewności idą do przeglądu.

**Koszt zmienny na klienta** (obliczenia z notatek): pierwsze mapowanie kosztuje ok. $0,001–0,02. Kolejne pliki z tym samym odciskiem nagłówków nie wymagają modelu językowego. PDF kosztuje ok. $0,002–0,004 za stronę, gdy potrzebny jest OCR. Nawet przy 50 stronach PDF miesięcznie koszt zmienny wynosi ułamek złotówki przy cenie 49 zł, więc marża brutto jest bardzo wysoka.

### 5.4 Model danych zapamiętanego mapowania

```sql
-- Konto i dostawcy
suppliers (
  id uuid pk, account_id uuid, name text,
  default_currency text default 'PLN',
  missing_rows_policy text check (in ('keep','zero_stock','flag')),  -- co zrobić z wierszami, których brak w nowym pliku
  gpsr_defaults jsonb,            -- wersja 2: producent, adres, osoba odpowiedzialna
  created_at timestamptz
)

-- Wersjonowany profil mapowania
mapping_profiles (
  id uuid pk, supplier_id uuid fk, version int,
  status text check (in ('draft','active','archived')),
  parent_version_id uuid null,    -- z której wersji powstał
  source_format text,             -- xlsx|xls|csv|xml|pdf
  sheet_name text, header_row int, data_start_row int,
  encoding text, delimiter text, decimal_sep text, thousands_sep text,
  header_fingerprint text,        -- sha256(znormalizowane nagłówki w kolejności)
  layout_signature jsonb,         -- [{col, norm_header, dtype, pct_numeric, pct_ean, samples[]}]
  created_by text check (in ('llm','user','llm+user')),
  llm_model text, created_at timestamptz,
  unique (supplier_id, version)
)

field_mappings (
  id uuid pk, profile_id uuid fk,
  target_field text,              -- sku|ean|name|price_purchase|price_retail|vat_rate|stock|unit|pack_qty|image_urls|category|brand|description
  source_column text, source_index int,
  transform text,                 -- direct|regex_extract|split|concat|lookup|constant
  params jsonb,                   -- np. {"regex":"ROZM\\.\\s*(\\d+)"}
  confidence numeric,             -- 0..1 (model językowy + kontrole deterministyczne)
  confirmed_by_user boolean
)

transform_rules (
  profile_id uuid pk fk,
  rules jsonb                     -- schemat poniżej
)

sku_aliases (                     -- ręczne przypisania zapamiętane na stałe
  supplier_id uuid, supplier_key text, shop_sku text,
  source text check (in ('manual','auto_ean','auto_sku')),
  primary key (supplier_id, supplier_key)
)

-- Przebiegi i historia
import_runs (
  id uuid pk, supplier_id uuid, profile_id uuid, profile_version int,
  file_name text, file_sha256 text, uploaded_at timestamptz,
  fingerprint_match text check (in ('exact','compatible','changed')),
  status text,                    -- parsed|mapped|reviewed|exported|failed
  row_count int, stats jsonb, warnings jsonb
)

product_snapshots (               -- znormalizowany stan każdego wiersza dostawcy w danym przebiegu
  run_id uuid fk, supplier_key text,  -- SKU dostawcy lub EAN
  shop_sku text null, ean text, name text,
  price_net numeric(12,2), price_gross numeric(12,2), vat_rate numeric(4,2),
  sell_price_gross numeric(12,2), stock int, unit text,
  image_urls text[], attrs jsonb, row_hash text,
  primary key (run_id, supplier_key)
)

change_sets (
  id uuid pk, run_id uuid fk, prev_run_id uuid null,
  counts jsonb                    -- {"new":12,"removed":3,"price_up":140,"price_down":8,"stock":510,"flagged":6}
)

change_items (
  change_set_id uuid fk, supplier_key text,
  change_type text,               -- new|removed|price_up|price_down|stock|attr|unmatched
  old jsonb, new jsonb, delta_abs numeric, delta_pct numeric,
  flags text[],                   -- price_jump|below_cost|dup_ean|invalid_ean|zero_price
  decision text check (in ('pending','accepted','rejected'))
)

exports (
  id uuid pk, run_id uuid, target text,  -- woocommerce (później idosell_iof|allegro|shoper|prestashop)
  mode text,                      -- update|new
  file_path text, rows int, created_at timestamptz
)
```

**Przykład `transform_rules.rules`:**

```json
{
  "price": {
    "input_column_basis": "net",
    "price_type": "purchase",
    "vat": { "source": "constant", "rate": 23 },
    "markup": { "type": "percent", "value": 35,
                "tiers": [ { "max_cost": 20, "value": 60 }, { "max_cost": 200, "value": 35 } ] },
    "rounding": { "mode": "end_with", "value": 0.99 },
    "min_margin_pct": 15,
    "currency": { "from": "PLN", "fixed_rate": null },
    "output_basis": "gross"
  },
  "stock": {
    "text_map": { "TAK": 5, "NIE": 0, ">10": 10, "brak": 0 },
    "safety_buffer": { "if_lte": 2, "set": 0 }
  },
  "units": { "pack_qty_column": "Ilość w opak.", "sell_unit": "szt.", "price_per": "pack" },
  "sizes": { "extract_from": "name", "regex": "ROZM\\.?\\s*(\\d{2})", "normalize": "upper" },
  "variants": { "enabled": false, "group_by": [], "option_columns": [] },
  "guards": { "max_row_drop_pct": 30, "max_price_change_pct": 25, "block_below_cost": true }
}
```

**Odcisk nagłówków.** Nagłówki normalizujemy: małe litery, bez polskich znaków, bez nadmiarowych spacji i znaków interpunkcyjnych. Z listy w kolejności liczymy `sha256`.

- **Zgodny (`exact`)**: odcisk identyczny. Profil stosuje się automatycznie.
- **Kompatybilny (`compatible`)**: podobieństwo zbiorów nagłówków (Jaccard) co najmniej 0,8, wszystkie zmapowane kolumny obecne, a podpisy typów zgodne. Profil stosuje się automatycznie z komunikatem.
- **Zmieniony (`changed`)**: model językowy dostaje stary profil i nowy plik, proponuje poprawki, użytkownik zatwierdza i powstaje `version + 1`.

### 5.5 Jak mierzyć poprawność mapowania i jak użytkownik ją poprawia

**Zestaw wzorcowy (golden files).** Przed premierą trzeba zebrać **30–50 prawdziwych plików** od rozmówców, w tym co najmniej 5 PDF i 5 par „stary i nowy plik” od tego samego dostawcy. Do każdego ręcznie przygotowujemy oczekiwany profil i oczekiwany plik WooCommerce. Testy regresji uruchamiamy przy każdej zmianie promptu, modelu albo kodu.

**Metryki:**

1. **Dokładność mapowania pól krytycznych** (SKU lub EAN, cena, podstawa netto/brutto, stan): cel ≥ 98%, liczona osobno, z wagą wyższą niż dla pól opisowych.
2. **Dokładność mapowania wszystkich pól** (precision i recall): cel ≥ 90%.
3. **Zgodność wierszy wyjściowych z wzorcem** (cena co do grosza, stan dokładnie): cel ≥ 99% na plikach z tekstem i ≥ 95% na PDF.
4. **Odsetek mapowań zaakceptowanych bez poprawki.**
5. **Odsetek kolejnych plików przetworzonych bez dotykania** (zgodny odcisk i zero ręcznych zmian): to najważniejsza metryka wartości produktu.
6. **Liczba poprawek użytkownika na import** i **czas od wgrania pliku do pobrania CSV.**
7. **Błędy zgłoszone po imporcie** przez użytkownika lub przez importer WooCommerce: cel bliski zeru.

**Reguły walidacji:**

- cena > 0,
- cena sprzedaży ≥ cena zakupu × (1 + minimalna marża),
- VAT należy do zbioru {23, 8, 5, 0},
- suma kontrolna EAN-13 jest poprawna,
- brak duplikatów EAN i SKU,
- stan jest liczbą całkowitą ≥ 0 po zastosowaniu mapy tekstowej,
- znaki nowej linii w opisach zamienione,
- kodowanie wyjścia UTF-8,
- liczba wierszy względem poprzedniego pliku w granicach progu,
- zmiana ceny względem poprzedniego pliku w granicach progu,
- wykrycie pary netto/brutto (kolumna B ≈ kolumna A × 1,23, 1,08 lub 1,05),
- ostrzeżenie, gdy wszystkie ceny dostawcy wzrosły dokładnie o ok. 23%, bo to sygnał zmiany podstawy na brutto.

**Pewność (confidence).** Pewność podawana przez model językowy łączymy z kontrolami deterministycznymi. Jeśli kolumna zmapowana jako EAN ma ponad 95% poprawnych sum kontrolnych, pewność rośnie. Jeśli kolumna ceny ma mniej niż 90% wartości liczbowych, pewność spada. Dla pól krytycznych robimy **dwa niezależne wywołania** modelu, z innym ziarnem albo innym modelem. Jeśli się nie zgadzają, pole staje się żółte i wymaga potwierdzenia, zgodnie z wnioskiem o agregacji odpowiedzi z [ACM 2025](https://dl.acm.org/doi/full/10.1145/3737412.3743490).

**Człowiek w pętli.** Użytkownik nigdy nie dostaje pliku bez ekranu podglądu. Pola żółte i czerwone wymagają kliknięcia. Podgląd pokazuje 20 wierszy „przed i po” oraz pełny raport zmian z flagami. Każda poprawka zapisuje się w profilu jako nowa wersja i jako przypadek testowy. Poprawki w kolejce dopasowań zapisują się jako aliasy SKU.

**Zmiana układu pliku.** Odcisk nagłówków w stanie `changed` blokuje automatyczny eksport. Narzędzie pokazuje różnicę nagłówków: dodane, usunięte i przemianowane kolumny. To dokładnie ten scenariusz, w którym integratorzy dziś zawodzą po cichu ([EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/)).

### 5.6 Cennik startowy

| Plan | Cena netto | Zawartość |
|---|---|---|
| **Test** | 0 zł | 1 dostawca, pliki do 300 wierszy, pełny raport zmian i eksport (żeby klient zobaczył wartość na własnym pliku) |
| **Start** | **49 zł/mies.** (490 zł/rok) | do 3 dostawców, do 10 000 wierszy w pliku, bez limitu przebiegów, PDF do 50 stron miesięcznie |
| **Pro** | **99 zł/mies.** (990 zł/rok) | do 10 dostawców, do 50 000 wierszy, PDF do 300 stron miesięcznie; w wersji 1.1 plik pod URL i harmonogram |
| **Jednorazowo** | 59 zł za plik | jednorazowa konwersja z raportem; kwota zaliczana na poczet abonamentu |

**Uzasadnienie względem konkurencji:**

- **BaseLinker:** trzech dostawców spoza Base Connect to plan Business (279 zł + 0,99 zł za zamówienie) plus 2 × 50 zł ([Base](https://base.com/pl-PL/cennik/)). Start za 49 zł jest kilka razy tańszy dla sklepu, który potrzebuje tylko zasilania produktów.
- **Apilo:** 99 zł/mies. za 3 hurtownie, ale wyłącznie z listy. Dostawca spoza listy to 599 zł wdrożenia ([Apilo](https://apilo.com/pl/help/podlaczenie-hurtowni-import-xml-csv/)). U nas dowolny dostawca jest w cenie.
- **Witly:** od 99 zł/mies. z kredytami ([Witly](https://witly.ai/cennik)). Start jest o połowę tańszy przy węższym, ale głębszym zakresie (raport zmian, PDF, bezpieczniki). Pro jest w tej samej cenie.
- **Sheet2Store:** $19 za katalog i $9 za każdą aktualizację ([Sheet2Store](https://sheet2store.com/)). Przy 3 dostawcach aktualizowanych co miesiąc to ok. $27 miesięcznie bez polskich realiów. Opcja jednorazowa 59 zł odpowiada na ten sam jednorazowy ból.
- **Freelancerzy:** 10–30 USD za każdą konwersję na Fiverr, 95 USD za oczyszczenie cennika na Upwork ([Fiverr](https://www.fiverr.com/gigs/shopify-csv), [Upwork](https://www.upwork.com/services/product/admin-customer-support-a-cleaned-supplier-price-list-with-sku-and-price-checks-2108927896407015122)). Abonament zwraca się po jednej lub dwóch aktualizacjach w miesiącu.
- **Słaby punkt:** WP Desk kosztuje 329 zł/rok, czyli ok. 27 zł/mies. ([WP Desk](https://www.wpdesk.pl/sklep/dropshipping-xml-woocommerce/)), a WebToffee $69/rok. Start jest od nich droższy, więc komunikacja musi mówić wprost: „bez hostingu i crona, Excel i PDF, raport zmian przed importem, ochrona przed złą ceną”. Jeśli rozmowy pokażą, że klient porównuje nas tylko z wtyczkami, warto przetestować Start za 29 zł.

---

## 6. Plan walidacji przed budową

### Gdzie znaleźć pierwszych 10 rozmówców

1. **Useme:** autorzy zleceń o hurtowniach i plikach XML/CSV. Profil pokazują zlecenia z 2024–2026 ([przykład z 58 ofertami](https://useme.com/pl/jobs/wdrozenie-sklepu-b2b-hurtownia-narzedzi-ogrodniczych-z-indywidualnymi-cennikami,141894/), [Shoper z 15 hurtowniami](https://useme.com/pl/jobs/api-aplikacja-do-importu-danych-z-15-hurtowni-do-sklepu-shoper,93003/)). Złóż ofertę „bezpłatna konwersja pierwszego pliku w zamian za 30 minut rozmowy”.
2. **Społeczność Allegro:** uczestnicy wątków o podwyżce BaseLinkera i o prostej aktualizacji stanów ([wątek 1](https://spolecznosc.allegro.pl/t5/zaawansowani-sprzedawcy/alternatywa-dla-baselinker-podwy%C5%BCka-od-stycznia-i-enterprise-od/td-p/882117), [wątek 2](https://spolecznosc.allegro.pl/t5/pocz%C4%85tkuj%C4%85cy-sprzedawcy/prosta-aplikacja-aktualizacji-stan%C3%B3w-przez-api/td-p/1022471)).
3. **Grupy na Facebooku:** „BaseLinker Expert” ([grupa](https://www.facebook.com/groups/baselinkerexpert/posts/4330824827189409/)), „Forum Sprzedawców” ([grupa](https://www.facebook.com/groups/forum.sprzedawcow/posts/4476311142618497/)) oraz grupy WooCommerce i WordPress PL. Wpis nie powinien reklamować produktu, tylko pytać: „szukam 10 osób, które co miesiąc przerabiają cennik od dostawcy”.
4. **Forum PrestaShop PL i forum.shoper.pl:** ręczne przejrzenie, bo te fora słabo się indeksują.
5. **Pośrednicy:** wdrożeniowcy i agencje, którzy opisują ten problem (np. [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/), [Vinson](https://vinson.agency/blog/integracja-shopera-z-hurtownia-import-xml-i-automatyczna-aktualizacja-stanow), [mhajok](https://mhajok.pl/import-produktow-idosell)). Mogą przedstawić klientów albo sami stać się kanałem sprzedaży.
6. **Bezpośrednio:** sklepy WooCommerce z narzędziami, ogrodem i motoryzacją znalezione przez wyszukiwarkę i porównywarki. Krótki mail do właściciela.

Cel: **10 rozmów w 7 dni**, w tym co najmniej 6 z WooCommerce i 2–3 z IdoSell lub Shopera dla porównania.

### Pytania w stylu Mom Test (o przeszłe zachowanie, nie o opinię o pomyśle)

1. Opowiedz o **ostatnim razie**, kiedy dostałeś nowy cennik albo plik od dostawcy. Co dokładnie zrobiłeś, krok po kroku?
2. Ilu masz dostawców? W jakim formacie przysyła każdy z nich (Excel, CSV, XML, PDF, link) i jak często?
3. Ile czasu zajęła ostatnia taka aktualizacja i kto ją wykonał?
4. Kiedy ostatnio **coś poszło nie tak** po imporcie (zła cena, wyzerowane stany, nadpisane opisy, netto zamiast brutto)? Jak się o tym dowiedziałeś i ile to kosztowało?
5. Skąd dziś wiesz, **co zmieniło się** u dostawcy (nowe i wycofane produkty, podwyżki)?
6. Jakich narzędzi, wtyczek lub integratorów próbowałeś? Co z nich zostało, a co porzuciłeś i dlaczego?
7. Czy **płaciłeś komuś** (freelancerowi, agencji, za wdrożenie w Apilo lub BaseLinkerze) za podłączenie dostawcy albo przerobienie pliku? Ile?
8. Jak liczysz cenę sprzedaży z ceny dostawcy: netto czy brutto, jaka marża, jakie zaokrąglenia, czy różnie dla różnych dostawców?
9. Co robisz z plikami PDF od dostawców?
10. Czy możesz mi wysłać **dwa ostatnie pliki od tego samego dostawcy** i eksport produktów ze sklepu? To test zaangażowania, ważniejszy niż wszystkie odpowiedzi.

### Test konkurencji (równolegle, dni 2–5)

Przetestuj **Witly** (30 dni bez karty, [cennik](https://witly.ai/cennik)) na 3 prawdziwych plikach od rozmówców, w tym 1 PDF i 1 parze „stary i nowy plik”. Sprawdź:

- czy przyjmuje PDF,
- czy pokazuje raport zmian przed importem,
- jak traktuje netto i brutto,
- ile kredytów zużywa jeden import,
- czy eksportuje do WooCommerce lub IdoSell,
- co się dzieje przy zmienionym układzie pliku.

Te same pliki przepuść przez **Sheet2Store** (darmowy podgląd 5 produktów, [sheet2store.com](https://sheet2store.com/)), a jeśli wystarczy czasu, także przez **EmberPrice** na testowym WooCommerce ([wordpress.org](https://wordpress.org/plugins/emberprice/)). Wynikiem testu jest tabela luk. Jeśli Witly robi wszystko z listy dobrze, różnicowanie spada do ceny, a to za mało.

### Sygnały „budować” i „porzucić”

**Budować**, jeśli spełnione są co najmniej 4 z 5 warunków:

- co najmniej 6 z 10 rozmówców aktualizuje pliki dostawców przynajmniej raz w miesiącu,
- co najmniej 5 z 10 przyśle prawdziwe pliki,
- co najmniej 3 z 10 opisze konkretną stratę po złym imporcie albo zapłacił już freelancerowi lub za wdrożenie,
- co najmniej 3 zgodzi się na przedpłatę (np. 3 miesiące planu Start z góry) albo podpisze list intencyjny,
- test Witly i Sheet2Store pokaże co najmniej 2 istotne luki (np. brak raportu zmian, słabe netto/brutto, brak PDF).

**Porzucić albo zmienić kierunek**, jeśli:

- większość rozmówców ma wszystkich dostawców w gotowych integracjach i jest z nich zadowolona,
- ból okazuje się jednorazowy (migracja), a nie cykliczny,
- nikt nie chce wysłać plików,
- Witly już dobrze robi raport zmian i PDF w cenie ok. 99 zł,
- rozmówcy porównują cenę tylko do wtyczek za ok. 300 zł/rok i nie widzą wartości w bezpieczeństwie.

**Zmienić niszę**, a nie porzucać pomysłu, jeśli ból jest silny, ale dotyczy IdoSell, Allegro albo hurtu B2B z PDF-ami.

---

## 7. Plan na pierwsze 30 dni

**Tydzień 1 (dni 1–7): walidacja i dane.**

- 10 rozmów według sekcji 6.
- Zebranie co najmniej 20 prawdziwych plików i co najmniej 5 eksportów sklepów.
- Testy Witly, Sheet2Store i EmberPrice.
- Postawienie testowego WooCommerce lokalnie.
- Prosta strona docelowa z listą oczekujących i ceną 49/99 zł, żeby zmierzyć zapisy.
- **Dzień 7–8: decyzja** według sygnałów z sekcji 6.

**Tydzień 2 (dni 8–14): rdzeń.**

- Wgrywanie plików.
- Parser XLSX, XLS, CSV i XML z wykrywaniem kodowania, separatora, arkusza i nagłówka.
- Podpisy kolumn.
- Wywołanie modelu językowego ze structured output.
- Ekran potwierdzenia mapowania.
- Zapis profilu dostawcy w wersji 1.
- Eksport „Nowe produkty” do CSV WooCommerce.
- Pierwsze 10 plików wzorcowych w testach automatycznych.

**Tydzień 3 (dni 15–21): to, co odróżnia produkt.**

- Wgrywanie eksportu sklepu i dopasowanie po SKU, EAN i aliasach.
- Reguły cen: netto/brutto, VAT, narzut z progami, zaokrąglenia, minimalna marża.
- Snapshoty i **raport zmian** z flagami i bezpiecznikami.
- Eksport „Aktualizacja”, przetestowany na instancji: czy nie nadpisuje pól.
- Odcisk nagłówków i wersjonowanie.
- PDF w wersji beta (Docling).
- Płatności.

**Tydzień 4 (dni 22–30): pilotaż i cena.**

- 5–8 pilotażowych użytkowników z rozmów. Pierwsze importy robisz razem z nimi na wideorozmowie, ręcznie wspierając proces.
- Pomiar metryk z sekcji 5.5 i poprawki.
- Rozszerzenie zestawu wzorcowego do 30 plików.
- Prośba o płatność po pierwszym udanym imporcie.
- Spisanie trzech najczęstszych próśb.
- Decyzja o drugim formacie wyjściowym: plik pod URL dla IdoSell albo Allegro (z GPSR), zależnie od tego, kto płaci.

**Cel na koniec 30 dni:** co najmniej 3 płacących klientów, co najmniej 70% kolejnych plików przetworzonych bez ręcznych poprawek i zero błędnych cen, które trafiły do sklepu.

---

## 8. Największe ryzyka i jak je ograniczyć

| Ryzyko | Prawdopodobieństwo | Wpływ | Jak ograniczyć |
|---|---|---|---|
| **Witly, Import2Shop albo Apilo dodadzą raport zmian i PDF.** Witly już ma zapamiętany scenariusz i alert zmiany formatu ([Witly](https://witly.ai/news/import-produktow)), Import2Shop ma stronę PL ([Import2Shop](https://import2shop.com/de/preise/)). | wysokie | wysoki | Wąska specjalizacja: polskie pliki, branże techniczne, bezpieczniki cen. Szybkie wejście do kolejnych formatów (IdoSell, Allegro). Bliskość klienta i obsługa po polsku. |
| **Niska bariera wejścia.** Sheet2Store, OhoSync, Csvio i EmberPrice powstały w 2025–2026 ([Sheet2Store](https://sheet2store.com/), [OhoSync](https://ohosync.com/), [Csvio](https://apps.shopify.com/csvio-ai-product-importer)). | wysokie | średni | Przewagą nie jest technologia, tylko zestaw wzorcowy polskich plików, biblioteka profili popularnych dostawców i jakość dopasowania. Każdy nowy klient wzbogaca bazę. |
| **Kotwica cenowa wtyczek** (WP Desk 329 zł/rok, WebToffee $69/rok) ogranicza cenę na WooCommerce. | średnie | średni | Komunikować „bez serwera, Excel i PDF, raport zmian, ochrona marży”. Przetestować 29 zł. Jeśli kotwica okaże się zbyt silna, przejść na IdoSell lub Allegro. |
| **Błędna cena w sklepie przez złe mapowanie** = utrata zaufania. | średnie | **bardzo wysoki** | Model językowy nie liczy cen. Zawsze podgląd przed eksportem. Bezpieczniki (cena poniżej zakupu, skok o ponad X%, spadek liczby wierszy). Dwa niezależne wywołania dla pól krytycznych. Zestaw wzorcowy w testach. |
| **Jakość PDF** (scalone komórki, skany) i brak benchmarku dla polskich cenników | wysokie | średni | PDF jako beta z limitem. Najpierw Docling, potem OCR. Wiersze o niskiej pewności idą do przeglądu. Uczciwy komunikat „skany jeszcze nie”. |
| **Niepotwierdzone specyfikacje platform**: czy aktualizacja WooCommerce nadpisuje pola, czy CSV Shopera obsługuje warianty, szczegóły IOF | średnie | średni | Każdy format testowany na prawdziwej instancji przed obietnicą w marketingu. Shoper odłożony. |
| **Założenie rynkowe 40–70% jest niezweryfikowane** | średnie | wysoki | Pytanie 2 w każdej rozmowie. Krótka ankieta na grupach. Decyzja po tygodniu 1. |
| **Platformy rozbudują własne importy** (Shoper jest właścicielem Apilo, Base rozwija Base Connect) | średnie | wysoki | Celować w dostawców spoza list. Być narzędziem między dowolnym plikiem a platformą, a nie integratorem jednej platformy. |
| **Prawo**: zdjęcia producenta, umowa powierzenia, Omnibus | niskie | średni | Linki URL zamiast kopiowania zdjęć. Regulamin przenosi odpowiedzialność za treści. Gotowy wzór umowy powierzenia. Hosting w UE. Ostrzeżenie przy cenach promocyjnych. |
| **Wsparcie klientów przytłoczy jedną osobę** (tak jest u konkurentów: skargi na wsparcie syncX i Firebear) | średnie | średni | Limit pilotażu do 10 klientów. Prowadzenie przy pierwszym imporcie. Biblioteka gotowych profili. Czytelne komunikaty błędów zamiast zgłoszeń do wsparcia. |
| **Koszty i dostępność modeli językowych** | niskie | niski | Model językowy potrzebny jest tylko przy pierwszym mapowaniu i przy zmianie układu. Koszt rzędu centów. Abstrakcja pozwalająca zmienić dostawcę modelu. |

---

## 9. Lista źródeł

### Wielkość rynku (PL i DE)
- [ewp.pl: liczba sklepów (D&B)](https://ewp.pl/liczba-sklepow-internetowych-w-polsce-rosnie-mimo-presji-globalnych-platform/)
- [pro.rp.pl: niemal 75 tys. sklepów](https://pro.rp.pl/raporty-ekonomiczne/art43687641-polacy-radza-sobie-z-chinczykami-codziennie-powstaje-szesc-nowych-e-sklepow)
- [dlahandlu.pl](https://www.dlahandlu.pl/e-commerce/polska-odporna-na-presje-temu-i-shein-codziennie-powstaje-6-nowych-e-sklepow,165980.html)
- [D&B: liczba sklepów (2021)](https://www.dnb.com/pl-pl/blog/dane/liczba-sklepow-internetowych.html)
- [ShopRank: Polska](https://shoprank.com/countries/poland)
- [AfterShip: Polska](https://www.aftership.com/ecommerce/statistics/regions/pl)
- [AfterShip: Niemcy](https://www.aftership.com/ecommerce/statistics/regions/de)
- [Store Leads: Shoper](https://storeleads.app/reports/shoper)
- [Store Leads: Shopware](https://storeleads.app/reports/shopware)
- [Shoper IR: wyniki Q4 2025](https://investors.shoper.pl/en/press-office/wyniki-finansowe-q4-2025---komunikat)
- [IAI: o firmie](https://www.iai-sa.com/pl/o-iai/)
- [Montagu: przejęcie IAI](https://montagu.com/montagu-to-acquire-iai-group-polands-leading-digital-retail-solutions-provider/)
- [MCI: sprzedaż IAI](https://mci.pl/mci-sprzedaje-grupe-iai-globalnemu-funduszowi-montagu-private-equity)
- [xyz.pl: 160 tys. sprzedawców Allegro](https://xyz.pl/pko-bp-i-allegro-zmieniaja-zasady-gry-milion-nowych-klientow-i-15-mld-zl-finansowania-dla-sprzedawcow/)
- [EuroEcom: Allegro](https://euroecom.com/blog/allegro-explained-why-over-150000-merchants-trust-this-fast-growing-marketplace/)
- [xyz.pl: Base ponad 30 tys. klientów](https://xyz.pl/base-sebastiana-kulczyka-kupil-firme-szefa-pko-bp-uwolni-miedzynarodowy-potencjal-polskich-sprzedawcow/)
- [Base.com: czym jest Base](https://base.com/pl-PL/pomoc/wiedza/czym-jest-base-com/)
- [SaleHoo: udział dropshippingu (niska wiarygodność)](https://www.salehoo.com/learn/dropshipping-market-size)
- [Listflix: Online-Shops DE](https://listflix.de/statistik/online-shops/)
- [mediasprout: Amazon.de](https://www.mediasprout.de/amazon-statistiken/)
- [HDE Online Monitor 2025](https://einzelhandel.de/images/Konjunktur/Online_Monitor_2025_HDE.pdf)
- [Shopware: EHI 2025](https://www.shopware.com/en/press/press-releases/for-the-fourth-year-in-a-row-shopware-remains-germanys-market-leader-among/)

### Konkurencja w Polsce
- [Base.com: cennik](https://base.com/pl-PL/cennik/)
- [Base.com: hurtownie](https://base.com/pl-PL/pomoc/wiedza/hurtownie/)
- [Base.com: import produktów](https://base.com/pl-PL/pomoc/wiedza/import-produktow/)
- [Capterra: Base](https://www.capterra.com/p/245981/Base/)
- [jakwybrachosting.pl: recenzja Base](https://jakwybrachosting.pl/recenzja-baselinker/)
- [EcomFlowLab: integracja z hurtownią](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/)
- [EcomFlowLab: Base, Apilo, Sellasist](https://ecomflowlab.pl/baselinker-podrozal-migracja-apilo-sellasist/)
- [Apilo: podłączenie hurtowni](https://apilo.com/pl/help/podlaczenie-hurtowni-import-xml-csv/)
- [Apilo: porównanie aplikacji](https://apilo.com/pl/help/aplikacja-integracje-z-hurtowniami-czy-dropshipping-modul-apilo-co-wybrac/)
- [Shoper App Store: Pakiet 3 Hurtownie](https://www.shoper.pl/aplikacje/integracje-z-hurtowniami)
- [Shoper App Store: Dropshipping Apilo](https://www.shoper.pl/aplikacje/dropshipping-modul-apilo)
- [Shoper App Store: Incom](https://www.shoper.pl/aplikacje/integracja-z-incom)
- [Shoper App Store: Witly](https://www.shoper.pl/aplikacje/witly)
- [Shoper App Store: VeroSoft](https://www.shoper.pl/aplikacje/integracja-hurtowniami-verosoft)
- [Witly: import produktów](https://witly.ai/news/import-produktow)
- [Witly: cennik](https://witly.ai/cennik)
- [Sellasist](https://sellasist.pl/rozwiazania/integracje-z-hurtowniami-i-dropshipping-2-0/)
- [Sky-Shop: cennik modułu](https://sky-shop.pl/cennik-modul-integracji-z-hurtowniami/)
- [IdoSell: integracja z hurtownią](https://pomoc.idosell.com/towary/iai-downloader/integracja-z-hurtownia)
- [mhajok](https://mhajok.pl/import-produktow-idosell)
- [PrePIM](https://prepim.eu/integracje/hurtownie/idosell/)
- [SellStar: cennik](https://sellstar.pl/cennik/)
- [Sellpander](https://www.sellpander.pl/integracja-z-hurtownia/)
- [WP Desk](https://www.wpdesk.pl/sklep/dropshipping-xml-woocommerce/)
- [PrestaShow](https://prestashow.pl/pl/moduly-prestashop/5-prestashop-importer-integracja-z-hurtowniami-xml-csv-api.html)
- [x13](https://x13.pl/integracje-prestashop/import-xml-do-prestashop.html)
- [Upsellr](https://www.upsellr.io/pl)
- [Społeczność Allegro: alternatywa dla BaseLinkera](https://spolecznosc.allegro.pl/t5/zaawansowani-sprzedawcy/alternatywa-dla-baselinker-podwy%C5%BCka-od-stycznia-i-enterprise-od/td-p/882117)

### Konkurencja międzynarodowa
- [Parabola: vendor price list import](https://parabola.io/use-cases/vendor-price-list-import)
- [Parabola: cennik](https://parabola.io/pricing)
- [Automation Atlas: ceny Paraboli](https://automationatlas.io/answers/parabola-pricing-explained-2026/)
- [Parabola Community: zmiana cennika](https://community.parabola.io/t/parabola-pricing-update/1660)
- [Eofferix: mapowanie](https://eofferix.com/docs/mapping-fields)
- [Eofferix: CSV/XLSX](https://eofferix.com/docs/import-csv-xlsx-price-list)
- [Eofferix: Ozon](https://eofferix.com/price-list-to-ozon)
- [WP All Import](https://wordpress.org/plugins/wp-all-import/)
- [WP All Import: cennik](https://www.wpallimport.com/pricing/)
- [WP All Import: recenzje 1★](https://wordpress.org/support/plugin/wp-all-import/reviews/?filter=1)
- [WebToffee](https://www.webtoffee.com/product/product-import-export-woocommerce/)
- [WebToffee: recenzje 1★](https://wordpress.org/support/plugin/product-import-export-for-woo/reviews/?filter=1)
- [WP Desk na wordpress.org](https://wordpress.org/plugins/dropshipping-xml-for-woocommerce/)
- [EmberPrice](https://wordpress.org/plugins/emberprice/)
- [Koalab Sync](https://wordpress.org/plugins/koalab-sync/)
- [ELEGANTAL](https://addons.prestashop.com/de/datentransfer-backup/24523-easy-import-products-from-csv-excel-xml-json-txt.html)
- [MyPrestaModules](https://addons.prestashop.com/fr/transfert-sauvegarde-donnees/19091-catalogue-de-produits-csv-excel-dimportation.html)
- [OBS Solutions](https://addons.prestashop.com/en/data-transfer-backup/21973-bulk-import-update-products-via-csv-xml-or-json.html)
- [Store Commander: licencje](https://my.storecommander.com/fr/content/45-licences-store-commander)
- [Shopware Import/Export (SW5)](https://store.shopware.com/en/swagef36a3f0ee25/shopware-import-export.html)
- [Kommora](https://store.shopware.com/en/kommo52751045368m/import-export-pro-csv-xlsx-xml-import-export.html)
- [Firebear (Shopware Store)](https://store.shopware.com/en/fireb81914862032m/improved-import-export-mass-actions.html)
- [Pickware](https://help.pickware.com/en/articles/659853-how-do-i-create-and-edit-suppliers)
- [MAVRui](https://opencartforum.com/en/files/file/1479-avtomaticheskoe-obnovlenie-cen-na-sayte-iz-excel-i-xml-praysov-postavschikov-mavrui)
- [usergio Suppliers](https://opencartforum.com/en/files/file/811-avtomatychna-obrobka-prais-lystiv/)
- [Odoo Softhealer](https://apps.odoo.com/apps/modules/18.0/sh_import_supplier_info/)
- [syncX Stock Sync](https://apps.shopify.com/stock-sync)
- [syncX: recenzje 1–2★](https://apps.shopify.com/stock-sync/reviews?ratings%5B%5D=1&ratings%5B%5D=2)
- [Matrixify](https://apps.shopify.com/excel-export-import)
- [Syncee](https://apps.shopify.com/syncee-1)
- [Sheet2Store](https://sheet2store.com/)
- [OhoSync](https://ohosync.com/)
- [Csvio](https://apps.shopify.com/csvio-ai-product-importer)
- [MicrocityLabs](https://microcitylabs.com/)
- [Supplier Update Guard](https://community.shopify.com/t/review-supplier-csv-prices-before-a-shopify-import-19-once/700040)
- [REPMOD](https://repmod.de/)
- [Import2Shop: ceny](https://import2shop.com/de/preise/)
- [Synesty: ceny](https://synesty.com/de/pricing/)
- [excodata](https://www.excodata.com/en/)
- [nexoma](https://www.nexoma.de/produkte/features/shopware-anbinden/)

### Dowody potrzeby
- Fora: [Shopify: ręczne poprawki](https://community.shopify.com/t/what-do-you-still-fix-by-hand-when-updating-supplier-prices-or-stock/692332), [Shopify: tytuły](https://community.shopify.com/t/import-csv-updating-variant-price-and-variant-inventory-qty-without-overwriting-title/333334), [Shopify: ceny CSV](https://community.shopify.com/t/how-can-i-efficiently-update-prices-using-a-csv-file/138448), [Shopify: Stock Sync](https://community.shopify.com/t/what-reliable-app-can-replace-stock-sync-for-dropship-stock-updates/192086), [Shopify: SKU bez Handle](https://community.shopify.com/t/update-shopify-stock-levels-via-csv-with-no-handle-only-sku/306346), [Allegro: aktualizacja stanów](https://spolecznosc.allegro.pl/t5/pocz%C4%85tkuj%C4%85cy-sprzedawcy/prosta-aplikacja-aktualizacji-stan%C3%B3w-przez-api/td-p/1022471), [PrestaShop: ilości](https://forum.prestashop.com/topic/1070349-aktualizacja-ilo%C5%9Bci-wybranych-produkt%C3%B3w-csv/), [PrestaShop: XML](https://forum.prestashop.com/topic/339861-import-pliku-xml-baza-produkt%C3%B3w/), [polskapresta: kodowanie](https://polskapresta.pl/index.php?topic=505.0), [Shopware: ceny](https://forum.shopware.com/t/korrektes-importieren-von-preisen/99189), [Shopware: feed dostawcy](https://forum.shopware.com/t/lieferanten-artikel-feed-csv-importieren-wer-kann-helfen/43754), [Shopware: EAN](https://forum.shopware.com/t/lieferantendaten-mit-import-export-advanced-importieren/44507), [Shopware 2022](https://forum.shopware.com/t/import-von-produktdaten-in-shopware-abgleich-und-vereinen-zweier-excel-dateien-mit-uebereinstimmenden-zeilen-auf-basis-ean/95391), [JTL 2026](https://forum.jtl-software.de/threads/arbeiten-mit-lieferanten-eks-workflows-und-sql.247773/)
- Reddit: [r/shopify: PDF](https://www.reddit.com/r/shopify/comments/1fjiwcb/how_do_you_manage_thousands_of_items_from/), [r/ShopifyeCommerce: Matrixify](https://www.reddit.com/r/ShopifyeCommerce/comments/1ll4a0d/alternatives_to_the_matrixify_shopify_app/), [r/supplychain](https://www.reddit.com/r/supplychain/comments/1sbsqil/how_is_everyone_handling_these_constant/), [r/ShopifyApps](https://www.reddit.com/r/ShopifyApps/comments/1x0uuok/would_you_use_a_tool_that_compares_supplier_csv/), [r/InventoryManagement](https://www.reddit.com/r/InventoryManagement/comments/1v2b0fx/how_do_you_deal_with_messy_supplier_spreadsheets/)
- Freelance: [Useme 141894](https://useme.com/pl/jobs/wdrozenie-sklepu-b2b-hurtownia-narzedzi-ogrodniczych-z-indywidualnymi-cennikami,141894/), [Useme 93003](https://useme.com/pl/jobs/api-aplikacja-do-importu-danych-z-15-hurtowni-do-sklepu-shoper,93003/), [Useme 118834](https://useme.com/pl/jobs/sklep-na-shopify-integracja-z-hurtownia-plik-xml,118834/), [Useme 99669](https://useme.com/pl/jobs/podaczenie-zewnetrznych-hurtowni-do-apilo,99669/), [Useme 115168](https://useme.com/pl/jobs/konwertowanie-plikow-csv,115168/), [Useme 125873](https://useme.com/pl/jobs/integracja-baselinker-z-hurtowniami-zewnetrznymi-i-sklepem-shopify,125873/), [Useme 69230](https://useme.com/pl/jobs/poszukujemy-osoby-do-konwersji-plikow-xml-do-csv-i-pozniejsze-wdrozenie-do-sklep,69230/), [Useme 67286](https://useme.com/pl/jobs/integracja-hurtowni-ze-sklepem-na-idosell-za-posrednictwem-iai-downloader,67286/), [Useme 25364](https://useme.com/pl/jobs/integracja-sklepu-internetowego-z-hurtownia-csv-lub-webapi,25364/), [Freelancehunt 1661107](https://freelancehunt.com/project/skript-na-python-chtobyi-svodit-praysyi/1661107.html), [Freelancehunt 1573246](https://freelancehunt.com/project/sdelat-avtomaticheskuyu-obrabotku-raznoobraznyih-praysov/1573246.html), [Fiverr: shopify csv](https://www.fiverr.com/gigs/shopify-csv), [Fiverr: gig za 100 USD](https://www.fiverr.com/hossainzabed/reshape-supplier-excel-file-into-bulk-csv-listing-to-upload-any-website), [Upwork: czyszczenie cennika](https://www.upwork.com/services/product/admin-customer-support-a-cleaned-supplier-price-list-with-sku-and-price-checks-2108927896407015122), [Upwork: porównanie cenników](https://www.upwork.com/services/product/admin-customer-support-i-will-compare-old-and-new-supplier-price-lists-and-flag-changes-2108322491870819321)

### Technika
- [WooCommerce: CSV importer](https://woocommerce.com/document/product-csv-importer-exporter/)
- [PrestaShop 8: import](https://docs.prestashop-project.org/v.8-documentation/user-guide/configuring-shop/advanced-parameters/import)
- [PrestaShop: specyfikacja 1.7](https://build.prestashop-project.org/prestashop-specs/1.7/back-office/advanced-parameters/import/configure-import.html)
- [Shoper Learn: profile CSV](https://www.shoper.pl/learn/artykul/zarzadzanie-plikami-csv-ogolne-zasady-ustawienia-profilow)
- [Shoper Learn: warianty](https://www.shoper.pl/learn/artykul/zarzadzanie-plikami-csv-grupowe-dodawanie-producenta)
- [Vinson: import CSV do Shopera](https://vinson.agency/blog/import-produktow-do-shopera-z-pliku-csv-instrukcja-krok-po-kroku)
- [Shoper Developer Docs](https://developers.shoper.pl/docs/)
- [Apilo: CSV do Shopera](https://apilo.com/pl/help/eksport-produktow-do-shoper-plik-csv/)
- [IdoSell: import webowy](https://pomoc.idosell.com/towary/webowy-import-aktualizacja-i-przywracanie-towarow/import-i-aktualizacja-towarow-za-pomoca-narzedzia-webowego)
- [IdoSell: dokumentacja IOF](https://www.idosell.com/pl/developers/otwarte-standardy-i-api-do-integracji/internet-offer-format-iof-/dokumentacja-internet-offer-format-iof/)
- [IdoSell: aktualizacja towarów](https://pomoc.idosell.com/towary/iai-downloader/aktualizacja-towarow)
- [Allegro: wystawianie z pliku](https://help.allegro.com/pl/sell/c/jak-wystawiac-oferty-z-pliku)
- [Allegro Developer Portal](https://developer.allegro.pl/documentation)
- [Allegro: regulamin API](https://developer.allegro.pl/rules)
- [GitHub allegro-api #11793](https://github.com/allegro/allegro-api/issues/11793)
- [Shopware: Import/Export](https://docs.shopware.com/en/shopware-en/settings/importexport)
- [Firebear: Shopware 6 import](https://firebearstudio.com/blog/ultimate-guide-to-shopware-6-import.html)
- [arXiv 2511.16134: ekstrakcja tabel z PDF](https://arxiv.org/html/2511.16134v2)
- [Procycons: benchmark PDF](https://procycons.com/en/blogs/pdf-data-extraction-benchmark/)
- [Mistral OCR 4](https://mistral.ai/news/ocr-4/)
- [Mistral: cennik](https://docs.mistral.ai/inference/pricing)
- [Azure Document Intelligence](https://azure.microsoft.com/en-us/pricing/details/document-intelligence/)
- [AWS Textract](https://aws.amazon.com/textract/pricing/)
- [LlamaParse: cennik](https://developers.llamaindex.ai/llamaparse/general/pricing/)
- [Claude: cennik](https://platform.claude.com/docs/en/about-claude/pricing)
- [Claude: structured outputs](https://platform.claude.com/docs/en/build-with-claude/structured-outputs)
- [Claude: obsługa PDF](https://platform.claude.com/docs/en/build-with-claude/pdf-support)
- [LLMatch](https://arxiv.org/html/2507.10897v1)
- [Magneto (VLDB)](https://www.vldb.org/pvldb/vol18/p2681-freire.pdf)
- [ACM 2025: schema mapping](https://dl.acm.org/doi/full/10.1145/3737412.3743490)

### Prawo
- [Kancelaria Lech: zdjęcia i opisy od producenta](https://znakitowarowe-blog.pl/zdjecia-i-opisy-produktow-od-producenta/)
- [Lege Artis: packshot](https://czasopismo.legeartis.org/2019/11/prawa-autorskie-zdjec-produktow-fotografia-packshot-utwor-wyrok/)
- [Trusted Shops (2018)](https://business.trustedshops.pl/blog/zdjecia-opisy-produktow-prawa-autorskie/)
- [Dyrektywa 96/9/WE](https://eur-lex.europa.eu/eli/dir/1996/9/oj)
- [RODO](https://eur-lex.europa.eu/eli/reg/2016/679/oj)
- [Wytyczne KE GPSR, C/2025/6233](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=OJ:C_202506233)
- [Händlerbund: GPSR](https://www.haendlerbund.de/de/ratgeber/recht/produktsicherheitsverordnung)
- [IT-Recht Kanzlei: GPSR](https://www.it-recht-kanzlei.de/eu-produktsicherheitsverordnung-gpsr-haendler-informationspflichten.html)
- [xictron: upomnienia GPSR](https://www.xictron.com/de/blog/gpsr-produktsicherheitsverordnung-online-shop-2026/)
- [UOKiK: wyjaśnienia Omnibus](https://uokik.gov.pl/storage/archiwum/e6e552a1.pdf)
- [UOKiK: Omnibus](https://uokik.gov.pl/tag/dyrektywa-omnibus)
- [xSale: regulamin API Allegro 2025](https://xsale.ai/zmiany-w-regulaminie-allegro-rest-api-2025-co-musi-wiedziec-kazdy-wlasciciel-e-commerce/)
- [PAngV](https://www.gesetze-im-internet.de/pangv_2022/BJNR492110021.html)
- [eRecht24: PAngV](https://www.e-recht24.de/ecommerce/13092-preisangabenverordnung.html)

### Rynek niemiecki
- [JTL-Forum 2026](https://forum.jtl-software.de/threads/arbeiten-mit-lieferanten-eks-workflows-und-sql.247773/)
- [JTL-Guide: Ameise](https://guide.jtl-software.com/jtl-wawi/jtl-ameise/artikeldaten-importieren/)
- [Mader Systemtechnik](https://mader-systemtechnik.de/warenwirtschaft-jtl-wawi/jtl-ameise/)
- [knowmates](https://www.knowmates.de/jtl-wawi-automatischer-import-von-lieferantenbestaenden/)
- [REPMOD: Datanorm](https://repmod.de/datanorm-in-csv-umwandeln)
- [REPMOD: dane dostawców](https://repmod.de/lieferantendaten-konvertieren)
- [Import2Shop: Shopware](https://import2shop.com/en/shopware-connectors/)
- [onveda: BMEcat](https://www.onveda.de/en/blog/bmecat)
- [entitys.io: katalogi elektroniczne](https://entitys.io/magazin/elektronische-kataloge)
- [PlentyONE: ceny](https://www.plentyone.com/de/preise-und-tarife)
- [Webiprog](https://www.webiprog.de/en/bmecat-xlsx-and-csv-import-tool-for-shopware/)
- [wnm.de: e-commerce 2026](https://wnm.de/e-commerce-zahlen-2026-kennzahlen-trends-und-was-sie-fuer-ihren-shop-bedeuten)
- [waredock](https://www.waredock.com/magazine/ecommerce-market-in-germany/)
- [Statista: dostawcy oprogramowania e-commerce w DE](https://www.statista.com/statistics/685489/e-commerce-software-provider-market-share-in-germany/)
- [ecommercegermany.com: platformy DACH](https://ecommercegermany.com/blog/top-20-e-commerce-platforms-in-the-dach-region/)

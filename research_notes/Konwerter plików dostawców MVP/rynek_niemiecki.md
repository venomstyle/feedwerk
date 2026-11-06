# Rynek niemiecki (DE) dla konwertera plików dostawców → pliki importu do sklepu

Data researchu: 2026-11-06. Źródła starsze niż 2025 są oznaczone rokiem. Tam, gdzie czegoś nie dało się zweryfikować, jest dopisek „nie udało się potwierdzić”.

## 1. Dowody popytu w języku niemieckim (fora, Reddit, freelance)

### Takeaway
Problem występuje w Niemczech i jest dobrze udokumentowany na forach Shopware i JTL, i to od ponad 10 lat. Jedyny wątek z lat 2025–2026, który znalazłem, pochodzi z forum JTL. Sprzedawcy obchodzą problem przez Excel (SVERWEIS/VLOOKUP), szablony JTL-Ameise albo własne skrypty Pythona. Na niemieckim Reddicie i platformach freelance nie znalazłem żadnych dowodów (luka, a nie dowód na brak popytu).

### Cited Findings
- **Forum JTL, czerwiec 2026** (scraper odczytał datę jako „3. Juni 2026”, częściowo niejednoznacznie): sprzedawca z ~10 000 artykułów, który planuje 100 000+, ma kilku dostawców na artykuł. Chce co godzinę aktualizować ceny według dostawcy podstawowego i zaokrąglać do XX,90 €, czego wbudowana kalkulacja JTL-Wawi nie umie. Obejście: „Python sammelt und bewertet die Lieferantendaten, erzeugt daraus eine CSV … diese wird dann über die Ameise … zurück in JTL gespielt”. Jeden z odpowiadających pisze, że Ameise potrzebuje ~30 min na aktualizację 18 000 artykułów od jednego dostawcy, i radzi importować tylko deltę (porównać stan obecny z nowym). To bezpośrednio potwierdza wartość funkcji „diff vs poprzedni plik” — [JTL-Forum: Arbeiten mit Lieferanten EKs](https://forum.jtl-software.de/threads/arbeiten-mit-lieferanten-eks-workflows-und-sql.247773/)
- **Forum Shopware, lipiec 2022 (starsze)**: sprzedawca dostaje od producentów pliki Excel do importu z kluczem EAN, ale bez własnych numerów artykułów z ERP. Musi łączyć dwa arkusze po EAN, przy czym część EAN występuje tylko w jednym z nich. Pisze: „Ich bin sicher, dass wir nicht das einzige Unternehmen mit dieser Problematik sind”. Inny użytkownik odpowiada, że przy aktualizacji cenników robią to „ziemlich oft”, eksportem z Shopware i formułą VLOOKUP. Wątek ma 558 wyświetleń — [forum.shopware.com, 2022](https://forum.shopware.com/t/import-von-produktdaten-in-shopware-abgleich-und-vereinen-zweier-excel-dateien-mit-uebereinstimmenden-zeilen-auf-basis-ean/95391)
- **Forum Shopware, 2013 (stare)**: wątek „Tool um automatisch CSV, XLS, TXT, DBF, etc. zu laden”, 10 odpowiedzi, ~2,2 tys. wyświetleń. Dostawca narzędzia do synchronizacji danych dostawców z WaWi („unilukas”) rozważał wersję dla Shopware. Na tej samej stronie są powiązane wątki: „Import über EAN abgleichen” (2021), „Import Lagerbestand ohne ordernumber” (2018), „Import/Export Advanced: EAN importieren” (2018) — [forum.shopware.com, 2013](https://forum.shopware.com/t/tool-um-automatisch-csv-xls-txt-dbf-etc-zu-laden/11754); lista powiązanych wątków [tutaj](https://forum.shopware.com/t/import-von-produktdaten-in-shopware-abgleich-und-vereinen-zweier-excel-dateien-mit-uebereinstimmenden-zeilen-auf-basis-ean/95391)
- **Forum JTL**: osobny wątek „Preise lassen sich nicht importieren über Ameise” (data nieznana) pokazuje problemy z importem cen przez Ameise — [JTL-Forum](https://forum.jtl-software.de/threads/preise-lassen-sich-nicht-importieren-ueber-ameise.244936/). Tag „ek-preise”: użytkownik importuje prawie wszystko przez Ameise — [JTL-Forum tag ek-preise](https://forum.jtl-software.de/tags/ek-preise/)
- **Agencje i blogi JTL** opisują codzienny import stanów magazynowych dostawców z CSV przez JTL-Ameise z „wiederverwendbaren Vorlagen”. To pokazuje, że rynek usług wdrożeniowych wokół tego problemu istnieje — [Mader Systemtechnik](https://mader-systemtechnik.de/warenwirtschaft-jtl-wawi/jtl-ameise/); [knowmates: JTL-Wawi Automatischer Import von Lieferantenbeständen](https://www.knowmates.de/jtl-wawi-automatischer-import-von-lieferantenbestaenden/) (daty nie udało się potwierdzić)
- **Reddit**: trafiły się tylko wątki anglojęzyczne, czasem z automatycznym tłumaczeniem na niemiecki („?tl=de”). Przykład: r/excel, dopasowywanie numerów części z cennika dostawcy do własnej listy — [Reddit r/excel](https://www.reddit.com/r/excel/comments/zaw5k5/matching_prices_from_vendor_price_list_to_our/?tl=de). r/InventoryManagement: „messy supplier spreadsheets”, przy imporcie CSV/Excel wymieniane są Matrixify i Stock Sync — [Reddit](https://www.reddit.com/r/InventoryManagement/comments/1v2b0fx/how_do_you_deal_with_messy_supplier_spreadsheets/?tl=de). To nie są niemieckie źródła, więc nie dowodzą popytu w DE.

### Inferences
- Ten sam schemat bólu co w PL: pliki Excel/CSV od dostawców, dopasowanie po EAN, ręczne VLOOKUP, powtarzane przy każdym nowym cenniku. Większy sprzedawca w DE zwykle ma ERP lub WaWi (JTL-Wawi, PlentyONE), więc docelowym plikiem jest często **import do WaWi (JTL-Ameise)**, a nie bezpośrednio do sklepu. W PL większy udział ma import prosto do sklepu (wniosek, nie zweryfikowany w tym researchu).
- Wątek JTL z 2026 pokazuje, że sprzedawcy z dziesiątkami tysięcy SKU potrzebują delty, reguł zaokrągleń i wyboru dostawcy. Funkcja „diff” jest więc w DE realnie poszukiwana.

### Gaps
- Wątków o tym temacie na wp-forum.de, w forum Gambio, na r/de_EDV i r/selbststaendig **nie udało się potwierdzić** (wyszukiwanie nic nie zwróciło).
- Ogłoszeń z freelancermap, malt.de ani niemieckich zleceń na Upwork typu „Lieferantendaten importieren” **nie udało się potwierdzić**: wyszukiwarka zwróciła tylko strony główne platform, bez ogłoszeń. Do sprawdzenia ręcznie po zalogowaniu.
- Artykułów Händlerbund/OnlineHändler-News, t3n ani EHI konkretnie o problemie importu danych dostawców **nie znalazłem**.

## 2. Konkurenci w DE — co robią, cena, dowolny dostawca czy lista stała

### Takeaway
DE jest wyraźnie bardziej nasycone niż PL. Istnieją co najmniej dwa narzędzia niemal identyczne z pomysłem: **REPMOD** (konwerter BMEcat/Datanorm/CSV → JTL-Ameise/Shopware/WooCommerce/Shopify, profile mapowania per dostawca, porównanie asortymentu) oraz **Import2Shop** (ciągła synchronizacja dowolnych dostawców ze sklepami, 69 €/mies., **ma też polską wersję strony**). Do tego dochodzą iPaaS (Synesty od 99 €/mies.), serwisy danych produktowych (excodata) i pluginy Shopware (Firebear 56–75 €/mies.).

### Cited Findings
**Bezpośredni konkurenci (konwersja plików dostawców):**
- **REPMOD** (repmod.de, założyciel Patrick Wilke / REP Solution). Konwertuje BMEcat-XML (m.in. 2005 i dialekty), DATANORM 4 i 3 oraz CSV na gotowe importy dla JTL-Ameise (5 plików CSV plus ceny progowe i media), Shopware 6, WooCommerce, Shopify, Plentymarkets i neutralny CSV ERP/PIM. Ma też:
  - profile mapowania zapisywane per dostawca,
  - normalizację jednostek, warianty parent/child, ceny progowe, rabaty i narzuty per dostawca,
  - generowanie tytułów SEO,
  - uzupełnianie danych producenta pod GPSR, Amazon ASIN, walidację cyfr kontrolnych GS1,
  - „Sortiments-Abgleich” (wykrywa artykuły wycofane i daje CSV z Active=0).

  Cena: **od 89 € za pakiet 5 000 artykułów, bez abonamentu**, 250 artykułów gratis. Na stronie nie znalazłem wzmianki o AI — [repmod.de](https://repmod.de/); [DATANORM in CSV umwandeln](https://repmod.de/datanorm-in-csv-umwandeln); [Lieferantendaten konvertieren](https://repmod.de/lieferantendaten-konvertieren)
- **Import2Shop**. Łączy dowolnych hurtowników (CSV, XML, JSON, API, EDI, FTP) ze sklepami Shopify, WooCommerce, Shopware, Gambio, PrestaShop oraz z eBay, Amazon i Kaufland. Ma reguły cenowe (narzuty, zaokrąglenia, minimalna marża) per dostawca, automatyczną synchronizację stanów z dezaktywacją wyprzedanych produktów, przekazywanie zamówień do dostawcy i AI do tekstów SEO. Gotowe integracje m.in. InnoCigs, vidaXL, BigBuy, Kaysser. Cena: **69 €/mies. netto** za 1 hurtownika i 1 kanał (kolejne płatne dodatkowo), bez limitu artykułów, bez opłaty wdrożeniowej, wypowiedzenie miesięczne. Strona jest dostępna w wersjach DE/EN/ES/IT/**PL**/NL, co czyni ich konkurentem także w Polsce — [Import2Shop Preise](https://import2shop.com/de/preise/); [Import2Shop Shopware connector](https://import2shop.com/en/shopware-connectors/) (strona zmodyfikowana w październiku 2026)
- **excodata** (serwery w AT i DE). Oferuje oprogramowanie i usługę: przygotowanie i walidację danych produktowych z Excel, CSV, PDF i BMEcat do sklepu lub ERP, plus narzędzie BMEtoolbox (BMEcat → Excel/CSV). Na stronie piszą wprost: „Every supplier uses a different format … the mapping has to be rebuilt for every file”. Cennik: Check od 290 € jednorazowo, Set up od 490 € jednorazowo, ciągła obsługa od 99 €/mies. — [excodata.com](https://www.excodata.com/en/)
- **Synesty** (iPaaS no-code z Niemiec). Importy i eksporty CSV/XML dla Shopware, JTL, PlentyONE i marketplace’ów, także między dostawcami a sklepem. Cena **od 99 €/mies.** przy rozliczeniu rocznym, bezterminowy darmowy test — [Synesty Pricing](https://synesty.com/de/pricing/); [Synesty Shopware Add-On](https://synesty.com/en/addon/shopware/); [Amazon SP Appstore: „from EUR 99 per month”](https://sellercentral.amazon.com/selling-partner-appstore/dp/amzn1.sp.solution.c71bcbfa-804c-47e8-85f0-4f8857649e89?mons_sel_locale=en_US)
- **nexoma**. Portal, do którego dostawcy sami wgrywają dane (albo robi to sprzedawca), z transformacją i walidacją danych i eksportem do Shopware. Obsługuje też FAB-DIS. Ceny nie udało się potwierdzić — [nexoma Shopware anbinden](https://www.nexoma.de/produkte/features/shopware-anbinden/)

**Pluginy i funkcje platform:**
- **Shopware 6, wbudowany Import/Export**: import CSV przez „Profile”, które przypisują kolumny do pól. Błędne rekordy trafiają do osobnego pliku CSV. Obsługuje tylko natywny CSV, nie Excel — [docs.shopware.com](https://docs.shopware.com/en/shopware-en/settings/importexport)
- **Firebear „Improved Import, Export & Mass Actions”** (Shopware Store). Obsługuje CSV, XML, XLSX i Google Sheets. Pozwala zapisać mapowanie kolumn dostawcy i używać go ponownie, ma importy według harmonogramu i FTP/SFTP. Cena **75 €/mies. lub 675 €/rok (56,25 €/mies.)**, ocena 4,33/5 z 26 recenzji. Wśród recenzji jest jedna negatywna: „Bekommen wir nicht zum Laufen” — [Shopware Store: Firebear](https://store.shopware.com/en/fireb81914862032m/improved-import-export-mass-actions.html)
- **Webiprog „BMEcat XLSX and CSV Import Tool for Shopware”**, plugin do Shopware 6. Ceny nie udało się potwierdzić — [webiprog.de](https://www.webiprog.de/en/bmecat-xlsx-and-csv-import-tool-for-shopware/)
- **JTL-Wawi + JTL-Ameise**: wbudowane narzędzie importu i eksportu oparte na szablonach, pozwala codziennie importować stany dostawców z CSV — [JTL-Guide: Ameise Artikeldaten importieren](https://guide.jtl-software.com/jtl-wawi/jtl-ameise/artikeldaten-importieren/); [Mader Systemtechnik](https://mader-systemtechnik.de/warenwirtschaft-jtl-wawi/jtl-ameise/). JTL-Wawi opisywane jest jako darmowa WaWi — [Visitmedia](https://visitmedia.de/jtl-software/jtl-wawi-kostenlose-warenwirtschaft/) (daty nie udało się potwierdzić; aktualnego cennika JTL nie sprawdzałem). Według forum Ameise wymaga gotowego, czystego CSV, a „brudną” pracę sprzedawca wykonuje sam (Python/Excel) — [JTL-Forum 2026](https://forum.jtl-software.de/threads/arbeiten-mit-lieferanten-eks-workflows-und-sql.247773/)
- **PlentyONE (plentymarkets)**: import z zewnętrznych źródeł limitowany planem, od „bis zu 5.000 Updates pro Tag” (Lite/Lite+) przez 15 000 (Expand) i 50 000 (Scale) do ponad 50 000 (Ultimate) — [PlentyONE Preise & Tarife](https://www.plentyone.com/de/preise-und-tarife). Szczegółów ElasticSync ani cen nie udało się potwierdzić.
- **WooCommerce**: ma wbudowany CSV Importer z mapowaniem kolumn. Od WooCommerce 11.1 warianty można importować jednym plikiem, jeśli wiersz rodzica stoi przed wierszami wariantów — [WooCommerce docs](https://woocommerce.com/document/product-csv-importer-exporter/). Popularnym rozszerzeniem jest **WP All Import** (drag & drop, CSV/XML/Excel, aktualizacja cen i stanów) — [wpallimport.com](https://www.wpallimport.com/import-woocommerce-product-price-stock/). Cen WP All Import nie udało się potwierdzić w tym researchu.

### Inferences
- **REPMOD to niemal 1:1 opisany pomysł** (mapowanie per dostawca, diff asortymentu, wiele formatów docelowych) z dodatkiem standardów DE (BMEcat, Datanorm, GPSR). Model cenowy „per paczka artykułów, bez abonamentu” kosztuje około 1,8 ct za artykuł. Różnicą dla nas może być obsługa PDF/Excel „z wolnej ręki” z AI oraz UX. REPMOD na stronie nie wspomina o AI ani PDF.
- **Import2Shop jest już w Polsce** (strona PL), więc to zagrożenie na rynku startowym, nie tylko w DE. Jego model to synchronizacja feedów (API/CSV/XML) w stylu dropshippingu, a nie „wgraj dowolny plik Excel/PDF, dostań import”.
- Ceny w DE: pluginy i SaaS dla MŚP mieszczą się w przedziale ~56–99 €/mies. (Firebear, Import2Shop, Synesty), usługi danych zaczynają się od ~290–490 € jednorazowo (excodata). To wskazuje na wyższą gotowość płacenia niż w PL (porównania z cenami w PL ten research nie obejmuje).

### Gaps
- Nie udało się potwierdzić funkcji i cen: Pickware, Billbee, Xentral, Afterbuy, Magnalister, DreamRobot, Sellerlogic, Channable, Lengow, productsup, Contentserv, Dataspot, neuroflash, „SpeedStars Lieferantenmodul”, plentymarkets ElasticSync. Z wiedzy ogólnej (niezweryfikowanej) to głównie ERP/WaWi, multichannel albo feedy wyjściowe (shop → marketplace), a nie konwersja plików dostawców na wejściu. Wymaga sprawdzenia.
- Nie udało się potwierdzić pełnej listy pluginów w Shopware Store dla frazy „Lieferantenimport” ani ich cen (wyszukiwanie z ograniczeniem do domeny zwróciło głównie pluginy eksportu zamówień).

## 3. Specyfika niemiecka (BMEcat, Datanorm, Grundpreis, EAN, GPSR, VAT, Amazon.de)

### Takeaway
Niemieckie dane dostawców są bardziej ustandaryzowane (BMEcat, Datanorm, ETIM) niż polskie Excele, ale same standardy też sprawiają kłopoty (kodowanie, jednostki, dialekty). Obowiązki prawne (GPSR Art. 19, Grundpreis z PAngV) wymuszają dodatkowe pola w imporcie, a GPSR jest już przedmiotem upomnień (Abmahnungen). Konkurent REPMOD już obsługuje GPSR, ASIN i GS1, więc w DE to wymóg wejścia, a nie wyróżnik.

### Cited Findings
- **BMEcat**: standard XML katalogów B2B. Typowe błędy importu to złe kodowanie (umlauty), zła kolejność elementów i jednostki zapisane tekstem („piece”/„pack”) zamiast kodów — [onveda: BMEcat explained](https://www.onveda.de/en/blog/bmecat); producenci tacy jak LAPP udostępniają katalog w BMEcat do integracji z WaWi — [LAPP](https://www.lapp.com/en/at/service/product-services/product-master-data/e/096921); przegląd formatów BMEcat, ETIM xChange, DATANORM, cXML/OCI — [entitys.io](https://entitys.io/magazin/elektronische-kataloge)
- **Datanorm** powstał jako standard dla budownictwa, do wymiany danych między producentami, hurtownikami i wykonawcami — [Pimics](https://www.pimics.com/de/produkt/eigenschaften/import-und-export). REPMOD normalizuje jednostki z Datanorm i przenosi numer artykułu hurtownika jako numer dostawcy — [repmod.de/datanorm-in-csv-umwandeln](https://repmod.de/datanorm-in-csv-umwandeln)
- **GPSR (rozporządzenie UE 2023/988), Art. 19**: w każdej ofercie online trzeba podać m.in. dane producenta (nazwa lub marka, adres pocztowy, adres elektroniczny), osobę odpowiedzialną w UE, gdy producent jest spoza UE, identyfikator produktu oraz ostrzeżenia i informacje o bezpieczeństwie. Dotyczy to także sprzedawców cudzych towarów, którzy muszą „die Herstellerinformationen für jedes Produkt kennen und produktgenau einpflegen” — [Händlerbund: GPSR](https://www.haendlerbund.de/de/ratgeber/recht/produktsicherheitsverordnung); [ihp media 2026](https://www.ihp-media.com/ratgeber/gpsr-onlineshop-pflichtangaben-2026/); [IT-Recht Kanzlei](https://www.it-recht-kanzlei.de/eu-produktsicherheitsverordnung-gpsr-haendler-informationspflichten.html)
- Pierwsze upomnienia za GPSR Händlerbund odnotował w maju 2025, z udokumentowanym przypadkiem kosztów 357 € (źródło wtórne, powołuje się na Händlerbund) — [xictron](https://www.xictron.com/de/blog/gpsr-produktsicherheitsverordnung-online-shop-2026/)
- **Grundpreis (PAngV)**: obowiązek podawania ceny jednostkowej, z wyjątkami (np. towary do samodzielnego nalewania) — [eRecht24](https://www.e-recht24.de/ecommerce/13092-preisangabenverordnung.html); tekst PAngV ze zmianą z października 2026 (BGBl. 2026 I Nr. 314) — [gesetze-im-internet.de](https://www.gesetze-im-internet.de/pangv_2022/BJNR492110021.html); w WooCommerce Grundpreis obsługuje się zwykle pluginem (np. German Market) — [hostpress](https://www.hostpress.de/blog/gpsr-woocommerce/)
- **EAN/GTIN**: EAN jest w DE kluczem łączenia plików producenta z WaWi — [forum.shopware.com 2022](https://forum.shopware.com/t/import-von-produktdaten-in-shopware-abgleich-und-vereinen-zweier-excel-dateien-mit-uebereinstimmenden-zeilen-auf-basis-ean/95391); REPMOD sprawdza cyfry kontrolne GS1 — [repmod.de](https://repmod.de/)

### Inferences
- Do produktu na DE potrzebne są: parsery BMEcat i Datanorm, przeliczenie Grundpreis (ilość, jednostka bazowa, cena za 1 kg/l/m), pola GPSR (producent, osoba odpowiedzialna w UE, ostrzeżenia), walidacja EAN, stawki VAT 19% / 7% przy przeliczaniu netto ↔ brutto. W PL odpowiednikiem jest VAT 23/8/5%, a cena jednostkowa obowiązuje na podobnej zasadzie (dyrektywa 98/6/WE). Architektura „mapowanie + reguły” przenosi się więc dobrze, ale potrzeba osobnego pakietu reguł DE.
- Docelowe formaty w DE to nie tylko sklep: JTL-Ameise (najczęstszy WaWi wśród MŚP) jest kluczowym targetem. REPMOD stawia go na pierwszym miejscu.

### Gaps
- Szablonów Amazon.de (flat file / inventory file templates) ani ich specyfiki DE **nie udało się potwierdzić** w tym researchu.
- Wpływu Verpackungsgesetz/LUCID na dane produktowe **nie udało się potwierdzić**. LUCID to rejestracja sprzedawcy, a nie pole produktu (wiedza ogólna, niezweryfikowana linkiem).
- Oficjalnego źródła o stawkach VAT 19/7% nie pobrałem (fakt powszechnie znany, ale bez linku w tym researchu).

## 4. Liczby rynku e-commerce MŚP w DE

### Takeaway
Rynek DE jest kilkukrotnie większy od PL. Sprzedaż online w DE to około 83–92 mld € (zależnie od definicji). W rejestrach firm jest ~63 tys. sklepów internetowych, w większości mikro- i małych. Shopware jest liderem wśród top-1000 sklepów według EHI, ale udział podawany w różnych źródłach się różni. Shopify prowadzi według liczby wdrożeń (Statista, 2026).

### Cited Findings
- Sprzedaż online w DE w 2025: 83,1 mld € brutto (towary), prognoza na 2026 ~86,3 mld € — [wnm.de (źródło wtórne)](https://wnm.de/e-commerce-zahlen-2026-kennzahlen-trends-und-was-sie-fuer-ihren-shop-bedeuten). Inny agregat podaje 92,3 mld € w 2025 (+3,9%), z czego 56,7% przez marketplace’y — [waredock (źródło wtórne)](https://www.waredock.com/magazine/ecommerce-market-in-germany/). HDE: 88,8 mld € netto w 2024 (+3,8%) — [HDE Online Monitor 2025 (PDF)](https://einzelhandel.de/images/Konjunktur/Online_Monitor_2025_HDE.pdf). Liczby różnią się z powodu definicji (brutto/netto, towary/usługi).
- **Liczba sklepów**: 62 734 firm w bazie Listflix sklasyfikowanych jako „Online-Shops”. 61,7% to drobni przedsiębiorcy (Kleingewerbe) lub freelancerzy, 12 160 to mikro-, 10 623 małe, 965 średnie, a 260 duże firmy (dane aktualizowane codziennie, metodologia własna) — [Listflix](https://listflix.de/statistik/online-shops/)
- **Shopware**: według komunikatu Shopware (1.10.2025, EHI) 11,5% top sklepów online w DE używa Shopware, czwarty rok z rzędu lider. EHI oczekuje +5,3% wzrostu w 2025 — [Shopware press release](https://www.shopware.com/en/press/press-releases/for-the-fourth-year-in-a-row-shopware-remains-germanys-market-leader-among/). **Sprzeczność**: Qualimero podaje 25,7% „Marktanteil” wśród top 1 000 sklepów B2C (EHI 2025) — [Qualimero](https://qualimero.com/blog/shopware-vs-woocommerce). Prawdopodobnie to inna metryka (np. ważona obrotem), co nie zostało potwierdzone.
- Statista: w sierpniu 2026 Shopify był wiodącym dostawcą oprogramowania e-commerce w DE (dokładny % ukryty za paywallem) — [Statista](https://www.statista.com/statistics/685489/e-commerce-software-provider-market-share-in-germany/)
- Rekomendacje platform w DACH: dla „Small German shop” Gambio, Shopify, WooCommerce, dla „Dropshipping or supplier-led store” Shopify, WooCommerce (blog, opinia) — [ecommercegermany.com](https://ecommercegermany.com/blog/top-20-e-commerce-platforms-in-the-dach-region/)

### Inferences
- Segment docelowy (małe i średnie sklepy z wieloma dostawcami) w DE liczy prawdopodobnie dziesiątki tysięcy firm, czyli więcej niż w PL. Udział Shopify w DE rośnie, a pomysł nie ma Shopify na liście startowych targetów. Warto to rozważyć.

### Gaps
- Deklarowanej przez Shopware liczby klientów (~100 000+) **nie udało się potwierdzić**. Scraper zwrócił „115”, co najpewniej oznacza 115 z top 1 000 sklepów, a nie łączną liczbę klientów.
- Udziału WooCommerce w DE (liczba sklepów DE) **nie udało się potwierdzić** z wiarygodnego źródła. Dane 6sense i Red Stag są globalne.

## 5. Ocena ogólna: czy DE jest łatwiejsze czy trudniejsze niż PL

### Takeaway
Problem jest w DE ten sam i lepiej udokumentowany. Gotowość płacenia jest wyższa (~56–99 €/mies. za plugin lub SaaS, 290–490 € za jednorazowe usługi danych). Konkurencja jest jednak **znacznie silniejsza i bardziej wyspecjalizowana**: REPMOD robi niemal dokładnie ten produkt z obsługą standardów DE, Import2Shop robi ciągłą synchronizację za 69 €/mies. i działa także w PL, do tego Synesty, excodata i Firebear. Wejście do DE wymaga lokalnych standardów (BMEcat, Datanorm, JTL-Ameise, GPSR, Grundpreis) i obsługi po niemiecku. DE jest więc rynkiem większym i lepiej płacącym, ale trudniejszym do wejścia; ma sens jako drugi krok tylko z wyraźnym wyróżnikiem.

### Cited Findings
- REPMOD ma już mapowanie per dostawca, diff asortymentu, BMEcat i Datanorm, GPSR, ASIN oraz cele JTL/Shopware/Woo/Shopify/Plenty — [repmod.de](https://repmod.de/)
- Import2Shop kosztuje 69 €/mies. netto, z obsługą wielu shopsystemów i marketplace’ów oraz stroną w języku polskim — [Import2Shop Preise](https://import2shop.com/de/preise/)
- Synesty od 99 €/mies. — [Synesty](https://synesty.com/de/pricing/); Firebear 56,25–75 €/mies. — [Shopware Store](https://store.shopware.com/en/fireb81914862032m/improved-import-export-mass-actions.html); excodata 290 € (check) / 490 € (setup) / 99 €/mies. — [excodata](https://www.excodata.com/en/)
- Sprzedawcy DE wciąż piszą własne skrypty (Python + Ameise) i proszą o import delty — [JTL-Forum 2026](https://forum.jtl-software.de/threads/arbeiten-mit-lieferanten-eks-workflows-und-sql.247773/)
- Shopware 6 natywnie importuje tylko CSV według profili, więc Excel i PDF trzeba najpierw przekształcić — [docs.shopware.com](https://docs.shopware.com/en/shopware-en/settings/importexport)

### Inferences
- **Podobieństwa z PL**: ten sam ból (różne formaty dostawców, ręczne VLOOKUP, powtarzanie przy każdym cenniku, potrzeba diffu). Te same platformy (WooCommerce, Shopify), choć w DE dodatkowo Shopware, JTL i Gambio.
- **Różnice**:
  1. Więcej ustandaryzowanych formatów (BMEcat, Datanorm), więc mniej „brudnego Excela/PDF” u większych hurtowni. Wartość AI do „brudnych” plików może być w DE relatywnie mniejsza dla branż technicznych, a większa dla lifestyle i dropshippingu.
  2. Silna warstwa WaWi/ERP (JTL), więc targetem jest często Ameise, a nie sklep.
  3. Więcej obowiązków prawnych na poziomie danych (GPSR, Grundpreis) i realne ryzyko upomnień, co może zwiększać gotowość płacenia za walidację.
  4. Wyższe ceny SaaS.
- **Rekomendacja robocza dla foundera**: DE jako drugi rynek jest zasadne, jeśli produkt w PL wypracuje przewagę, której REPMOD i Import2Shop nie mają (np. AI do PDF i nieustrukturyzowanych Excel, UX „wgraj i gotowe”, diff z akceptacją zmian). Wejście powinno startować od integracji JTL-Ameise i Shopware oraz pakietu „GPSR + Grundpreis”. Trzeba też uwzględnić, że Import2Shop konkuruje już w PL.
- Bariery: język i wsparcie po niemiecku (forum i recenzje w Shopware Store są po niemiecku, a negatywne recenzje dotyczą głównie supportu — [Firebear reviews](https://store.shopware.com/en/fireb81914862032m/improved-import-export-mass-actions.html)), kanał dystrybucji przez Shopware Store i partnerów JTL, oczekiwania prawne (Impressum, AVV/DSGVO — wiedza ogólna, niezweryfikowana).

### Gaps
- Brak twardych danych porównawczych o liczbie sklepów w PL i DE oraz o cenach w PL w tym researchu (inny zakres).
- Liczby klientów REPMOD i Import2Shop (trakcja konkurencji) **nie udało się potwierdzić**.
- Udziału sprzedawców MŚP w DE korzystających z JTL-Wawi **nie udało się potwierdzić**.

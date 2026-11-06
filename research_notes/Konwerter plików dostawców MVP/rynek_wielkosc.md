# Wielkość rynku: sklepy internetowe w PL i DE według platformy oraz udział sklepów sprzedających towar od dostawców zewnętrznych

Data researchu: 2026-11-06. Konwencja: **[OFICJALNE]** = dane spółki, rejestru lub urzędu; **[SKAN]** = automatyczne wykrywanie technologii (Store Leads, AfterShip, ShopRank, 6sense; liczą domeny/witryny, a nie firmy); **[WTÓRNE]** = blog lub agregator przytaczający cudze dane; **[OBLICZENIE]** = moje przeliczenie z cytowanych liczb.

## 1. Ile jest aktywnych sklepów internetowych w Polsce?

### Takeaway
Liczba zależy od tego, co się liczy. Firm zarejestrowanych jako sklep internetowy jest ok. 75 tys. (Dun & Bradstreet, 2025). Skanery technologii wykrywają ok. 143 tys. witryn sklepowych z dostawą fizyczną (ShopRank, XI 2026; AfterShip podaje podobny rząd wielkości). Do TAM lepiej pasuje 75 tys. jako dolna granica (firmy) i ok. 140 tys. jako górna granica (domeny).

### Cited Findings
- D&B Poland dla „Rzeczpospolitej”: w 2025 r. zarejestrowano ok. 7,8 tys. nowych e-sklepów, wykreślono 5,4 tys. Przyrost netto w 12 miesięcy to ponad 2,4 tys. (ok. +3,4% r/r, średnio ok. 200 sklepów miesięcznie). Łączna liczba aktywnych podmiotów „zbliża się do 75 tys.” **[OFICJALNE: dane rejestrowe D&B, przez media]**. Źródła: [ewp.pl, 28.01.2026](https://ewp.pl/liczba-sklepow-internetowych-w-polsce-rosnie-mimo-presji-globalnych-platform/), [pro.rp.pl: „Rynek e-handlu w Polsce to już niemal 75 tys. sklepów”](https://pro.rp.pl/raporty-ekonomiczne/art43687641-polacy-radza-sobie-z-chinczykami-codziennie-powstaje-szesc-nowych-e-sklepow), [dlahandlu.pl](https://www.dlahandlu.pl/e-commerce/polska-odporna-na-presje-temu-i-shein-codziennie-powstaje-6-nowych-e-sklepow,165980.html)
- Dla porównania, dane historyczne D&B: na początku stycznia 2021 r. zarejestrowanych było ok. 44,5 tys. sklepów internetowych **[OFICJALNE, 2021]**. [dnb.com](https://www.dnb.com/pl-pl/blog/dane/liczba-sklepow-internetowych.html)
- ShopRank (XI 2026): w Polsce jest „143.6k verified e-commerce stores” z dostawą fizyczną. W szerszej populacji sygnałów (272 204 domeny, także bez wykrytej platformy) WooCommerce ma 125 470 witryn **[SKAN]**. [shoprank.com/countries/poland](https://shoprank.com/countries/poland)
- AfterShip (PL): WooCommerce ma 72,07 tys. sklepów, czyli 50,31% wszystkich sklepów w regionie **[SKAN]**. [aftership.com/…/regions/pl](https://www.aftership.com/ecommerce/statistics/regions/pl)
  - Z tych dwóch liczb wynika łączna baza ok. 143 tys. **[OBLICZENIE]**.
  - Na tej samej stronie jest nagłówek „Total Stores 24.39K”, który do tego nie pasuje. Prawdopodobnie to inna metryka (np. nowe sklepy); traktować ostrożnie.
- Wpis na LinkedIn (Chris Stola, PhD) podaje „167,140 total eCommerce websites in Poland”; Shoper ma tam 15 124 sklepy, PrestaShop 14 488 **[WTÓRNE; źródło danych nieujawnione, data wpisu ok. 2026]**. [LinkedIn](https://www.linkedin.com/posts/chrisstolaphd_shopify-ecommerce-poland-activity-7453382860369170432-Uf4v)
- Mits.pl: „Zbadaliśmy 82 904 polskie sklepy internetowe”. To próbka z badania dostępności (EAA), a nie spis rynku **[WTÓRNE]**. [mits.pl](https://mits.pl/blog/dynamika-rynku-e-commerce-w-polsce-2025-co-nas-czeka)
- Kontekst popytowy:
  - Gemius „E-commerce w Polsce 2025”: zakupy online deklaruje 78% internautów, w polskich sklepach 77%, w zagranicznych serwisach 41%. [Gemius PDF](https://gemius.com/documents/81/RAPORT_E-COMMERCE_2025.pdf)
  - Według GUS e-zakupy stanowiły w 2025 r. 9,1% sprzedaży detalicznej (8,9% rok wcześniej). [rp.pl](https://www.rp.pl/handel/art44790431-polski-handel-online-rosnie-szybciej-niz-europa-ale-dystans-wciaz-jest-ogromny)

### Inferences
- Liczba z D&B (75 tys.) to firmy zarejestrowane jako e-sklep, najpewniej z PKD 47.91 jako działalnością główną. Pomija firmy, które prowadzą sklep obok innej działalności, np. producentów i sklepy stacjonarne z e-sklepem.
- Liczby ze skanerów (ok. 143 tys.) liczą domeny. Jedna firma może mieć kilka domen, a część domen to sklepy martwe lub hobbystyczne.
- Realistyczny przedział „aktywnych sklepów-firm” w PL to **ok. 75–140 tys.** Do dalszych obliczeń sugeruję **ok. 100 tys.** jako wartość środkową **[OBLICZENIE/założenie]**.

### Gaps
- Brak 2025/26 danych Ceneo o liczbie sklepów w porównywarce: nie udało się potwierdzić.
- Statista, BuiltWith i Wappalyzer: nie udało się pobrać aktualnych liczb dla .pl (paywall lub brak w wynikach).
- Pełna treść artykułu rp.pl z danymi D&B jest za paywallem, więc nie ma rozbicia na formy prawne ani regiony.

## 2. Ile aktywnych sklepów ma każda platforma w Polsce?

### Takeaway
WooCommerce dominuje liczebnie (ok. 51–72 tys. sklepów PL). Za nim są PrestaShop (ok. 16,5–17,4 tys.), Shoper (ok. 13,6–15,4 tys. według skanów; spółka mówi o „ponad 20 tys. e-sklepów”) i Shopify (ok. 9–14,5 tys.). Mniejsze platformy to IdoSell (ok. 3–4 tys. według skanów, ok. 7–8 tys. według spółki), ShopGold (ok. 4,2 tys.) i Sky-Shop (ok. 2,2 tys.).

### Cited Findings

**Tabela porównawcza (sklepy w PL)**

| Platforma | ShopRank, XI 2026: sklepy z dostawą fizyczną [SKAN] | ShopRank: wszystkie witryny z sygnałem [SKAN] | AfterShip PL [SKAN] | Store Leads [SKAN] | Dane spółki [OFICJALNE] |
|---|---|---|---|---|---|
| WooCommerce | 51 134 (35,6%) | 125 470 | 72,07 tys. (50,31%) | – | – |
| Custom / własne | 23 883 (16,6%) | 31 808 | 18,03 tys. (12,59%) | – | – |
| PrestaShop | 16 523 (11,5%) | 22 066 | 17,4 tys. (12,14%) | – | – |
| Shoper | 15 227 (10,6%) | 19 897 | 13,56 tys. (9,46%) | 15 425 globalnie, 95,2% w PL (ok. 14,7 tys.) | „ponad 20 tys. e-sklepów” (Grupa Shoper) |
| Shopify | 14 493 (10,1%) | 20 745 | 9,16 tys. (6,40%) | – | – |
| ShopGold | 4 216 (2,9%) | 5 415 | – | – | – |
| IdoSell | 4 054 (2,8%) | 5 907 | 3,04 tys. (2,12%) | – | ok. 7 tys. sklepów PL (Montagu); „blisko 8 tys.” (IAI) |
| Sky-Shop | 2 174 (1,5%) | 2 374 | – | – | – |
| Magento | 1 490 (1,0%) | 3 535 | – | – | – |
| OpenCart | 1 115 (0,8%) | 1 607 | – | – | – |

Źródła do tabeli: [ShopRank PL](https://shoprank.com/countries/poland), [AfterShip PL](https://www.aftership.com/ecommerce/statistics/regions/pl), [Store Leads – Shoper (aktualizacja 30.10.2026)](https://storeleads.app/reports/shoper).

**Shoper (Shoper S.A., GPW)**
- Grupa Shoper „wspiera ponad 20 tys. e-sklepów” (boilerplate komunikatu z 04.03.2026) **[OFICJALNE]**. [investors.shoper.pl](https://investors.shoper.pl/en/press-office/wyniki-finansowe-q4-2025---komunikat)
- Wyniki 2025 z tego samego komunikatu **[OFICJALNE]**:
  - przychody 218 mln zł (+13% r/r), skorygowana EBITDA 80 mln zł, marża 36,7%;
  - GMV omnichannel klientów ponad 21 mld zł (+45% r/r), w Q4 2025 6,5 mld zł (+50% r/r).
  - [investors.shoper.pl](https://investors.shoper.pl/en/press-office/wyniki-finansowe-q4-2025---komunikat)
- Ekosystem cyber_Folks + PrestaShop (po przejęciu PrestaShop) obejmuje „około 700 tys. merchantów” w Europie. cyber_Folks ma 49,9% Shopera **[OFICJALNE]**. [investors.shoper.pl](https://investors.shoper.pl/en/press-office/wyniki-finansowe-q4-2025---komunikat)
- Shoper ma też Apilo, narzędzie do sprzedaży wielokanałowej, czyli konkurenta BaseLinkera **[OFICJALNE]**. [investors.shoper.pl](https://investors.shoper.pl/en/press-office/wyniki-finansowe-q4-2025---komunikat)
- Dokładna liczba klientów (sklepów) na koniec Q2/Q3 2026 z raportów okresowych: nie udało się potwierdzić. Raport Q1 2026 istnieje ([PAP Biznes](https://biznes.pap.pl/wiadomosci/firmy/shoper-sa-raport-okresowy-kwartalny-skonsolidowany-12026-qsr): przychody Q1 2026 55,7 mln zł vs 51,7 mln zł), ale KPI liczby sklepów nie zostało pobrane.

**IdoSell (IAI S.A., od 2025 w portfelu Montagu)**
- Strona IAI: IdoSell „obsługuje blisko 8 tysięcy sklepów internetowych”, które generują roczne obroty 16,5 mld zł GMV **[OFICJALNE; data strony nieznana, prawdopodobnie 2025]**. [iai-sa.com/pl/o-iai](https://www.iai-sa.com/pl/o-iai/)
- Montagu: „IAI serves ~7,000 stores in Poland and ~6,000 in Hungary” (marki IdoSell, AtomStore i inne) **[OFICJALNE, 2025]**. [montagu.com](https://montagu.com/montagu-to-acquire-iai-group-polands-leading-digital-retail-solutions-provider/)
- LinkedIn IAI: „around 13,000 online stores” (PL i HU łącznie) **[OFICJALNE profil]**. [LinkedIn](https://pl.linkedin.com/company/iai-sa)
- Transakcja: MCI sprzedało IAI do Montagu, wpływ netto ok. 470 mln zł. [ewp.pl](https://ewp.pl/470-mln-zl-mci-sprzedaje-grupe-iai/)
- IdoSell celuje w średnie i duże sklepy („tysiące transakcji miesięcznie”). [mci.pl](https://mci.pl/mci-sprzedaje-grupe-iai-globalnemu-funduszowi-montagu-private-equity)

### Inferences
- Rozjazd Shoper (skan ok. 15 tys. vs spółka „ponad 20 tys.”) wynika prawdopodobnie z tego, że spółka liczy całą grupę (Apilo, Sempire, sklepy bez własnej domeny).
- Rozjazd IdoSell (skan 3–6 tys. vs spółka 7–8 tys.) może wynikać z white-label, AtomStore i sklepów B2B niewykrywanych przez skaner.
- SAM dla segmentu SaaS PL (Shoper + IdoSell + Sky-Shop + ShopGold) to ok. **25–35 tys. sklepów** **[OBLICZENIE]**.
- Open source (WooCommerce + PrestaShop) w PL to ok. **68–90 tys.** sklepów z dostawą fizyczną **[OBLICZENIE z ShopRank/AfterShip]**. Dużą część stanowią jednak mikrosklepy.

### Gaps
- Sky-Shop i ShopGold: brak danych spółek o liczbie klientów (nie udało się potwierdzić).
- BuiltWith i Wappalyzer dla .pl: brak aktualnych liczb.
- Store Leads ma raporty per platforma (np. [storeleads.app/reports](https://storeleads.app/reports)), ale pobrano tylko Shoper i Shopware.

## 3. Ilu sprzedawców firmowych jest na Allegro? Ilu użytkowników ma BaseLinker (Base.com)?

### Takeaway
Allegro ma ok. 160 tys. sprzedawców (partnerów). Oficjalna metryka to „LTM active sellers”, a cel ESG to 177 tys. sprzedawców z ofertą do 2026. Base.com (BaseLinker) ma „ponad 30 tys. klientów” (PL i zagranica) oraz integracje z ponad 400 hurtowniami. To bardzo istotne dla produktu: BaseLinker już rozwiązuje część problemu importu od hurtowni.

### Cited Findings
- **Allegro**
  - Equity Story FY2025 definiuje metrykę „Number of merchants represents LTM active sellers (verified merchants who have listed an offer on allegro.pl marketplace within the last 12 months…)” **[OFICJALNE]**. Samej liczby nie udało się wyekstrahować z PDF (48 stron, parser zawiódł), więc dokładna wartość FY2025 z tego dokumentu: nie udało się potwierdzić. [Allegro Equity Story FY2025 PDF](https://about.allegro.eu/wp-content/uploads/2026/05/Allegro-Equity-Story-FY2025-Introduction-to-Allegro.pdf)
  - „Sfinansuje 20 ze 160 tys. sprzedawców na Allegro” (wypowiedź Szymona Midery, PKO BP) **[WTÓRNE, ok. 2025/26]**. [xyz.pl](https://xyz.pl/pko-bp-i-allegro-zmieniaja-zasady-gry-milion-nowych-klientow-i-15-mld-zl-finansowania-dla-sprzedawcow/)
  - EuroEcom (zweryfikowane 21.09.2026): „more than 160,000 partners across the ecosystem”, ponad 15,3 mln aktywnych kupujących w PL na koniec 2025, GMV grupy 69,2 mld zł w 2025 **[WTÓRNE]**. [euroecom.com](https://euroecom.com/blog/allegro-explained-why-over-150000-merchants-trust-this-fast-growing-marketplace/)
  - Raport ESG Allegro: cel „177 tys. sprzedawców z ofertą do 2026 roku” **[WTÓRNE omówienie raportu ESG]**. [akademiaesg.pl](https://akademiaesg.pl/esg-allegro/)
  - Historycznie: ponad 133 tys. sprzedawców (raport ESG za 2021) [Allegro ESG 2021 PDF](https://about.allegro.eu/wp-content/uploads/2026/02/PL_ESG_REPORT_ALLEGRO_EU.pdf); ok. 128 tys. na koniec 2020 [FOB](https://odpowiedzialnybiznes.pl/partnerzy/allegro/); 125 tys. (wywiad z F. Nuytsem, ok. 2021) [wiadomoscihandlowe.pl](https://www.wiadomoscihandlowe.pl/e-commerce-i-e-grocery/rynek-e-grocery/francois-nuyts-prezes-allegro-z-naszej-platformy-korzysta-juz-125-tys-sprzedawcow-2413548).
  - Allegro: „GMV nears 70 bln PLN in 2025” **[OFICJALNE]**. [media.allegro.pl](https://en.media.allegro.pl/449995-allegros-gmv-nears-70-bln-pln-in-2025-as-it-enters-new-market-segments)
- **Base.com (BaseLinker)**
  - „W 2021 r. obsługiwaliśmy od 8 do 10 tys. klientów. Dziś jest ich już ponad 30 tys.” (wypowiedź zarządu Base przy przejęciu, wycena ok. 1 mld zł) **[OFICJALNE: wypowiedź spółki, przez media, 2025]**. [xyz.pl](https://xyz.pl/base-sebastiana-kulczyka-kupil-firme-szefa-pko-bp-uwolni-miedzynarodowy-potencjal-polskich-sprzedawcow/). Potwierdzenie: „ponad 30 tys. klientów i 90 mln zł inwestycji w rozwój tylko w 2024 r.” [LinkedIn iKomersiak #38](https://pl.linkedin.com/pulse/ikomersiak-38-wojciech-kotlicki-4qrzf)
  - Integracje Base.com (strona pomocy, modyfikacja 30.09.2026) **[OFICJALNE]**: „ponad 100 najpopularniejszych platform marketplace”, „ponad 50 platform sklepów internetowych”, „ponad 400 hurtowni”. [base.com – Czym jest Base](https://base.com/pl-PL/pomoc/wiedza/czym-jest-base-com/)
  - Rozbicie klientów Base.com PL vs zagranica: nie udało się potwierdzić.
  - Raport analityczny Shopera (IX 2025) wspomina „spektakularny wzrost po podwyżce cen przez BaseLinker”, czyli wzrost Apilo kosztem BaseLinkera **[WTÓRNE, raport rekomendacyjny]**. [strefainwestorow.pl PDF](https://strefainwestorow.pl/sites/default/files/attachments/52439589_13572353_52439589_20250915_0956_SHO_PL_RI.pdf)

### Inferences
- Sprzedawcy Allegro (ok. 160 tys.) w dużej mierze pokrywają się ze sklepami z pkt 1–2, bo wielu prowadzi i sklep, i konto na Allegro. Nie należy ich sumować.
- Ok. 30 tys. klientów Base.com to dobra proxy dla „profesjonalnych multichannel sellerów” w PL (i części CEE). To segment, który już płaci za automatyzację, ale ma też integracje z hurtowniami. Narzędzie do plików dostawców musi więc obsłużyć dostawców spoza tej listy: PDF, Excel ad hoc, nietypowe XML.

### Gaps
- Dokładna liczba „LTM active sellers” Allegro za FY2025: nie udało się potwierdzić (PDF nieprzeparsowany).
- Udział firm (B2C business sellers) vs osób prywatnych na Allegro: nie udało się potwierdzić.

## 4. Niemcy: łączna liczba sklepów, Shopware, WooCommerce, Amazon.de, JTL, Gambio, plentymarkets, Shopify

### Takeaway
Oficjalnego spisu niemieckich sklepów nie ma. Skanery wykrywają ok. 410 tys. witryn sklepowych w DE (AfterShip, przeliczenie). Shopware ma ok. 20–25 tys. sklepów w DE, WooCommerce i Shopify po ok. 110 tys., JTL-Shop i Gambio po ok. 6 tys. Na Amazon.de według źródeł wtórnych działa ok. 240 tys. sprzedawców, z czego ok. 48 tys. to firmy niemieckie. Liczby Amazona są słabo udokumentowane.

### Cited Findings
- **AfterShip DE** **[SKAN]**: WooCommerce 110,67 tys. (26,83%), Shopify 109,51 tys. (26,55%), Custom Cart 69,91 tys. (16,95%), Shopware 24,92 tys. (6,04%), JTL-Shop 6,35 tys. (1,54%), Gambio 6,05 tys. (1,47%), Others 28,3 tys. (6,86%). [aftership.com/…/regions/de](https://www.aftership.com/ecommerce/statistics/regions/de)
  - Z udziału WooCommerce wynika łączna baza ok. 412 tys. sklepów **[OBLICZENIE: 110,67/0,2683]**.
  - Nagłówek „Total Stores 86.21K” na tej stronie nie pasuje do tabeli; prawdopodobnie inna metryka.
- **Shopware**
  - Store Leads: 29 931 live stores globalnie, 67,0% w Niemczech, czyli ok. 20,05 tys. w DE **[SKAN + OBLICZENIE]**. Do tego 4,2% w Szwajcarii, 3,9% w Austrii. [storeleads.app/reports/shopware](https://storeleads.app/reports/shopware)
  - 6sense: 3 024 „customers” Shopware w Niemczech (77,2%) **[SKAN, inna metodologia – firmy w bazie 6sense, mocno zaniżone]**. [6sense](https://www.6sense.com/tech/ecommerce-platform/shopware-market-share)
  - EHI 2025: Shopware jest liderem wśród systemów sklepowych czwarty rok z rzędu i ma 11,5% z 1 000 największych sklepów B2C w DE **[OFICJALNE (EHI), przez Shopware i agencję]**. [shopware.com press](https://www.shopware.com/en/press/press-releases/for-the-fourth-year-in-a-row-shopware-remains-germanys-market-leader-among/), [leineglueck.de](https://www.leineglueck.de/shopware-marktfuehrer-shopsysteme-deutschland-2025/?upage=3)
  - Oficjalna liczba klientów Shopware w 2025/26: nie udało się potwierdzić.
- **Rynek DE ogółem**
  - EHI/ECDB: top 1 000 sklepów B2C miało 80,4 mld EUR netto w 2024 (77,5 mld w 2023) **[OFICJALNE]**. [ehi.org](https://www.ehi.org/presse/onlinehandel-in-deutschland-legt-wieder-zu/), [velobiz.de](https://www.velobiz.de/news/onlinehandel-in-deutschland-legt-wieder-zu-veloQXJ0aWNsZS8zMzU4Mgbiz)
  - HDE Online Monitor 2025: „Der Anteil der Händler, die Waren über das Internet verkaufen, liegt 2024 bei 40 Prozent” **[OFICJALNE]**. [HDE PDF](https://einzelhandel.de/images/Konjunktur/Online_Monitor_2025_HDE.pdf)
  - HDE szacuje obroty online w DE na 92,3 mld EUR w 2025 (+3,9% r/r) **[WTÓRNE cytowanie HDE]**. [ecommercegermany.com](https://ecommercegermany.com/blog/top-100-online-shops-by-turnover-in-germany/)
- **Amazon.de**
  - Amazon: „Über 225.000 europäische kleine und mittlere Unternehmen und Marken verkaufen bei Amazon” (+20% r/r). To liczba dla całej Europy, nie tylko DE **[OFICJALNE]**. [sellercentral.amazon.de](https://sellercentral.amazon.de/), [sell.amazon.de](https://sell.amazon.de/en)
  - „In Deutschland sind etwa 240.000 Seller aktiv und bieten rund 229 Millionen Produkte an” **[WTÓRNE, źródło pierwotne nieustalone]**. [mediasprout.de](https://www.mediasprout.de/amazon-statistiken/)
  - „over 48.000 german businesses … sell on Amazon” **[WTÓRNE]**. [adsmasters.de](https://adsmasters.de/selling-on-amazon-germany/)
  - Marketplace Pulse: sprzedawcy z Niemiec stanowią 53,17% sprzedawców Amazon.de, z UK 20,61% **[OFICJALNE dane MP, ale stary artykuł – rok nieustalony, prawdopodobnie ok. 2017]**. [marketplacepulse.com](https://www.marketplacepulse.com/articles/we-are-now-tracking-amazon-and-ebay-germany)
- **plentymarkets, Shopify DE (oficjalne)**: liczby spółek nie zostały znalezione (nie udało się potwierdzić). Shopify DE według skanu to 109,5 tys. (AfterShip, wyżej).

### Inferences
- Segment „Shopware + JTL + Gambio” w DE to ok. **32–37 tys.** sklepów **[OBLICZENIE z AfterShip/Store Leads]**. To typowy niemiecki Mittelstand; JTL i plentymarkets to też ERP-y z własnym importem.
- DE jest ok. 3x większe od PL liczbą sklepów (ok. 410 tys. vs ok. 143 tys. domen).
- Shopify DE (ok. 110 tys.) to w dużej mierze D2C i dropshipping. To potencjalnie duży, ale inny segment, bo dostawców obsługują tam aplikacje Shopify App Store.

### Gaps
- Oficjalna liczba niemieckich sklepów (Destatis, bevh): nie udało się potwierdzić. bevh publikuje obroty, nie liczbę sklepów.
- Liczba sprzedawców Amazon.de z Marketplace Pulse za 2025: nie udało się potwierdzić (strona „Top Amazon.de sellers” podaje ranking, nie sumę). [marketplacepulse.com](https://www.marketplacepulse.com/top-amazon-germany-sellers)
- Liczba klientów plentymarkets i JTL (spółki): nie udało się potwierdzić.

## 5. Jaki odsetek sklepów MŚP sprzedaje towar od hurtowni lub w dropshippingu, a jaki własną produkcję?

### Takeaway
**Nie znaleziono żadnego wiarygodnego badania ankietowego (PL ani DE) podającego udział sklepów kupujących od hurtowni lub w dropshippingu.** Jedyna liczba to globalne 27% sklepów z dropshippingiem jako głównym modelem (SaleHoo), a to źródło niskiej jakości. Udział trzeba więc oszacować założeniem i oznaczyć je wyraźnie w raporcie.

### Cited Findings
- SaleHoo (2026): „Roughly 27% of online stores now use dropshipping as their primary fulfillment model. About 23% of all ecommerce sales worldwide come from dropshipped products” **[WTÓRNE, agregator dostawcy dropshippingu, dane globalne, metodologia nieznana: niska wiarygodność]**. [salehoo.com](https://www.salehoo.com/learn/dropshipping-market-size)
- Budujecommerce.pl (I 2026): typowy start sklepu w PL to „gotowy sklep, integracja z dużą hurtownią, plik XML z kilkoma tysiącami produktów”. Autor sam zaznacza, że liczby („tysiąc sklepów z jednej hurtowni”) są „obrazowe… a nie wynik badania” (cytat z Pawła Mielczarka, vSprint) **[OPINIA]**. [budujecommerce.pl](https://budujecommerce.pl/logistyka-i-zwroty/dropshipping-jak-zaczac)
- HDE: 40% detalistów w DE sprzedaje online (2024). To nie mówi nic o źródle towaru, ale pokazuje, że duża część sklepów online w DE to detaliści, czyli odsprzedawcy, a nie producenci **[OFICJALNE]**. [HDE PDF](https://einzelhandel.de/images/Konjunktur/Online_Monitor_2025_HDE.pdf)
- Shoper, Apilo, Selly i Base.com mają dedykowane poradniki i funkcje dropshippingu oraz importu z hurtowni. To sygnał podażowy, że to masowy przypadek użycia, ale nie twarda liczba. [shoper.pl](https://www.shoper.pl/learn/artykul/dropshipping-co-wziac-pod-uwage-podczas-nawiazywania-wspolpracy-z-hurtownia), [apilo.com](https://apilo.com/pl/dropshipping-krok-po-kroku-od-czego-zaczac/), [selly.pl](https://www.selly.pl/dropshipping/)

### Inferences
- Model PKD 47.91 (handel detaliczny przez internet) z definicji oznacza odsprzedaż. Większość z ok. 75 tys. firm z D&B to więc najpewniej resellerzy kupujący od hurtowni lub dystrybutorów, a nie producenci. To wnioskowanie, nie dane.
- Proponowany zakres założenia do SAM: **40–70% sklepów MŚP** pracuje na plikach od zewnętrznych dostawców (hurtownia, dystrybutor, dropshipping). Dropshipping „czysty” to raczej **10–25%**. Oba zakresy to **[ZAŁOŻENIE, niepotwierdzone]**. Warto je zweryfikować własną ankietą lub wywiadami.

### Gaps
- Badanie PL (Gemius, IAB, Shoper, IdoSell, eIzba) z odsetkiem sklepów-resellerów vs producentów: nie udało się potwierdzić.
- Badanie DE (EHI, HDE, bevh, Händlerbund) z udziałem dropshippingu lub Großhandel-Bezug: nie udało się potwierdzić.

## 6. Ile hurtowni w Polsce oferuje pliki XML/CSV lub dropshipping?

### Takeaway
Najlepszą twardą proxy jest Base.com, które ma integracje z „ponad 400 hurtowniami”. Starsze listy (home.pl, 2021) wymieniały ok. 300 hurtowni dropshippingowych. Faktyczna liczba dostawców udostępniających pliki (wliczając małych dystrybutorów, którzy wysyłają Excel lub PDF mailem) jest najpewniej znacznie większa, ale tego nie potwierdzono.

### Cited Findings
- Base.com: integracje z „ponad 400 hurtowni” (oraz ponad 50 platform sklepowych i ponad 100 marketplace’ów), stan strony z 30.09.2026 **[OFICJALNE]**. [base.com](https://base.com/pl-PL/pomoc/wiedza/czym-jest-base-com/)
- home.pl (2021): „listę 300 rekomendowanych hurtowni internetowych dla sklepów online, działających w modelu dropshipping” **[WTÓRNE, 2021]**. [blog.home.pl](https://blog.home.pl/2021/05/najlepsze-hurtownie-dropshipping-dla-sklepow-internetowych/)
- Base.com, „Hurtownie dropshipping w Polsce [LISTA 2026]” (publikacja 23.10.2025, aktualizacja 26.06.2026): lista istnieje, ale łącznej liczby z treści nie udało się wyekstrahować. [base.com/blog](https://base.com/pl-PL/blog/hurtownie-dropshipping/)
- DE: niemieckie listy „Top 20 Dropshipping-Lieferanten” (BigBuy, VidaXL i inni) wskazują CSV/XML/API jako standard feedów **[WTÓRNE]**. [base.com DE](https://base.com/de-DE/blog/dropshipping-lieferanten/), [easync.io](https://easync.io/de/articles/dropshipping-lieferanten/)

### Inferences
- Ponad 400 hurtowni z gotową integracją w Base.com to dostawcy już obsłużeni. Nisza produktu to długi ogon dostawców bez integracji (Excel, PDF, nietypowe XML) oraz sklepy bez BaseLinkera.
- Liczba hurtowni w PL ogółem (PKD 46.x) jest rzędu dziesiątek tysięcy, ale tego nie zweryfikowano w tym researchu (nie udało się potwierdzić).

### Gaps
- Łączna liczba hurtowni w PL z feedem XML/CSV: nie udało się potwierdzić.
- Liczba integracji hurtowni w IdoSell, Shoper i Apilo: nie udało się potwierdzić.

### Zbiorcza tabela liczb do TAM/SAM (dla report writera; dotyczy wszystkich pytań; przeliczenia oznaczone)

| Segment | PL | DE | Źródło / status |
|---|---|---|---|
| Firmy zarejestrowane jako e-sklep | ok. 75 tys. | brak danych | D&B 2025 [OFICJALNE] |
| Witryny sklepowe (skan) | ok. 143 tys. | ok. 412 tys. | ShopRank / AfterShip [SKAN, OBLICZENIE] |
| WooCommerce | 51–72 tys. | ok. 111 tys. | [SKAN] |
| PrestaShop | 16,5–17,4 tys. | brak danych | [SKAN] |
| Shoper | ok. 14,7–15,4 tys. (skan) / ponad 20 tys. (spółka) | – | [SKAN] / [OFICJALNE] |
| IdoSell | 3–6 tys. (skan) / ok. 7–8 tys. (spółka) | – | [SKAN] / [OFICJALNE] |
| Shopware | – | ok. 20–25 tys. | Store Leads / AfterShip [SKAN] |
| JTL-Shop + Gambio | – | ok. 12,4 tys. | AfterShip [SKAN] |
| Shopify | 9–14,5 tys. | ok. 110 tys. | [SKAN] |
| Sprzedawcy marketplace | Allegro ok. 160 tys. | Amazon.de ok. 240 tys. (w tym ok. 48 tys. firm DE) | [WTÓRNE] |
| Klienci Base.com | ponad 30 tys. (wielokrajowo) | – | [OFICJALNE przez media] |
| Udział sklepów z dostawcami zewnętrznymi | brak badania; założenie 40–70% | brak badania | [ZAŁOŻENIE] |

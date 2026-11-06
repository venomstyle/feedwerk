# Konkurencja w Polsce: import plików dostawców/hurtowni do sklepów internetowych

Stan badania: 6.11.2026. Ceny netto, chyba że zaznaczono inaczej. Starsze informacje mają podany rok.
Skróty: "dowolny plik" = arbitralny XML/CSV/XLS/PDF od dowolnego dostawcy, z własnym mapowaniem robionym samodzielnie, bez wdrożenia przez vendora.

---

## 1. BaseLinker / Base.com: jak działa import z hurtowni, czy obsługuje dowolny plik, ile kosztuje, co mówią użytkownicy?

### Takeaway
Base obsługuje hurtownie z gotowej listy (plik XML/CSV/API skonfigurowany przez Base) oraz przez darmowe Base Connect. Własny import z pliku przyjmuje dowolny CSV, ale XML tylko o znanej strukturze (np. Ceneo); XLS nie jest obsługiwany, a import z pliku nie tworzy wariantów. Base oficjalnie podaje, że nie integruje hurtowni wprost ze sklepem internetowym, bo nastawia się na marketplace'y. Cennik zależy od liczby zamówień (279 zł + 0,99 zł/zamówienie) i wywołał w 2024–2026 wiele skarg na podwyżki.

### Cited Findings
**Cennik (odczyt 11.2026)**
- Freemium: 0 zł, do 100 zamówień/mies., do 1000 produktów, synchronizacja co godzinę, przechowywanie danych 6 mies. — [Base.com cennik](https://base.com/pl-PL/cennik/)
- Business: 279 zł stałej opłaty + 0,99 zł za zamówienie; bez limitu produktów i użytkowników, synchronizacja w czasie rzeczywistym, dane przez 24 mies. Enterprise: wycena indywidualna, ponad 5000 zamówień lub 1 mln zł GMV miesięcznie. Ceny netto — [Base.com cennik](https://base.com/pl-PL/cennik/)
- Hurtownie: przez Base Connect bez limitu i bez opłat na każdym planie. Hurtownie podłączone inaczej (np. plikiem integracyjnym): jedna za darmo, każda kolejna 50 zł/mies. i wymaga planu Business. Integracje z hurtowniami spoza Base Connect są wyłączone z zasady „wszystkie integracje w cenie abonamentu" — [Base.com cennik, FAQ](https://base.com/pl-PL/cennik/); [Pomoc Base: hurtownie](https://base.com/pl-PL/pomoc/wiedza/hurtownie/)
- Recenzja z 2026 wymienia dodatkowe opłaty za częstszą synchronizację stanów z hurtownią: 10 zł (co godzinę) do 200 zł/mies. (co 5 min). Źródło jest stroną trzecią; na oficjalnym cenniku nie potwierdziłem tych kwot — [jakwybrachosting.pl recenzja Base 2026](https://jakwybrachosting.pl/recenzja-baselinker/)
- Przykładowe wyliczenia: 1000 zamówień ≈ 1269 zł/mies., 5000 zamówień ≈ 5229 zł albo Enterprise (odczyt 13.10.2026) — [EcomFlowLab](https://ecomflowlab.pl/baselinker-podrozal-migracja-apilo-sellasist/)

**Funkcje: hurtownie i import z pliku**
- Moduł „Hurtownie" (Integracje → Dodaj integrację → Hurtownie) obsługuje hurtownie standardowe (plik XML, CSV lub API) i Base Connect. Do podłączenia potrzebny jest link do pliku XML, dane logowania lub token API — [Pomoc Base: hurtownie](https://base.com/pl-PL/pomoc/wiedza/hurtownie/) (aktualizacja 05.2026)
- Hurtownia jest w Base osobnym magazynem. Stany i ceny pobierane są mniej więcej co godzinę, reszta danych raz na dobę w nocy. Pierwsze pojawienie się produktów może potrwać do 12 h. Są mnożniki cen według progów cenowych i korekta stanów (np. 0–10 szt. pokazuj jako 0) — [Pomoc Base: hurtownie](https://base.com/pl-PL/pomoc/wiedza/hurtownie/)
- FAQ Base: XML (np. od hurtowni) można zaimportować do magazynu Base „tylko jeżeli ma on znaną Base.com strukturę (np. format Ceneo)", natomiast „możliwy jest import z dowolnego pliku CSV" — [Pomoc Base: hurtownie](https://base.com/pl-PL/pomoc/wiedza/hurtownie/)
- FAQ Base: „Czy za pomocą systemu BaseLinker mogę zintegrować z hurtownią mój sklep internetowy? Niestety aktualnie nie ma takiej możliwości." Produkty z hurtowni można wystawiać na marketplace'ach z integracją dwukierunkową — [Pomoc Base: hurtownie](https://base.com/pl-PL/pomoc/wiedza/hurtownie/)
- Hurtownię spoza listy można podłączyć wyłącznie samodzielnie przez API Base, czyli wymaga to programowania — [Pomoc Base: hurtownie](https://base.com/pl-PL/pomoc/wiedza/hurtownie/)
- Import produktów z pliku: CSV w dowolnym formacie lub XML w domyślnej strukturze. Plik XLS nie jest obsługiwany („Nie jest możliwy import pliku w formacie XLS"). Import nie tworzy wariantów („Import nie pozwala na tworzenie wariantów produktów") — [Pomoc Base: import produktów](https://base.com/pl-PL/pomoc/wiedza/import-produktow/) (aktualizacja 06.2026)
- Base podaje „ponad 600 zintegrowanych hurtowni" (cytat za stroną trzecią, odczyt 09.2026) — [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/)
- Wdrożeniowiec opisuje Base Connect tak: połączenie wymaga akceptacji hurtowni, synchronizacja do co 5 min, import jest szybki (2321 produktów w 6 min). W kreatorze importu nie ma opcji „bierz cenę sugerowaną", zostaje mnożnik. Base Connect sam nie wystawia ofert — [EcomFlowLab, 09.2026](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/)
- Na rynku są płatne nakładki na Base do „dowolnej hurtowni z pliku XML/CSV", np. Sellpander („Moduł Integracji hurtowni pozwala importować i aktualizować produkty z dowolnego pliku XML lub CSV… jako link"). Strona pochodzi z 2021, ostatnia modyfikacja 04.2024; ceny nie znalazłem — [Sellpander](https://www.sellpander.pl/integracja-z-hurtownia/)
- Na grupie FB „BaseLinker Expert" użytkownicy proszą o pomoc w integracji pliku XML z hurtowni, a w odpowiedziach pojawiają się oferty usług (treść widoczna tylko we fragmencie) — [Facebook, grupa baselinkerexpert](https://www.facebook.com/groups/baselinkerexpert/posts/4330824827189409/)

**Opinie i skargi**
- Wątek na Społeczności Allegro (od 04.10.2024 do 12.2025): po zapowiedzi podwyżki i przejścia na Enterprise od 5 tys. zamówień użytkownicy opisują wzrost kosztów o 300–1100%. Jeden pisze o skoku z 3 tys. do 45 tys., inny o koszcie obsługi 6–7 zł za zamówienie. Narzekają też, że system jest przeładowany funkcjami. Jako alternatywy padają: IDEAerp, Atom Store, xSale, Apilo, Sellasist, Syncsphere, Listerro — [Społeczność Allegro](https://spolecznosc.allegro.pl/t5/zaawansowani-sprzedawcy/alternatywa-dla-baselinker-podwy%C5%BCka-od-stycznia-i-enterprise-od/td-p/882117)
- Relacje z grup FB (lipiec 2026), przytaczane anonimowo przez autora artykułu: skoki abonamentu z 3 tys. na 28 tys. zł/mies. albo 15 tys. zamiast 2,5 tys. Autor zaznacza, że to relacje użytkowników, nie dane Base — [EcomFlowLab](https://ecomflowlab.pl/baselinker-podrozal-migracja-apilo-sellasist/)
- Gazeta Wyborcza (2024) pisała o „burzy" w sieci po zmianie cennika BaseLinkera; artykuł za paywallem, widoczny tylko fragment — [wyborcza.biz](https://wyborcza.biz/biznes/7,147743,30280548,spolka-miliardera-sebastiana-kulczyka-jest-atakowana-w-sieci.html)
- Capterra: 4,5/5 przy 14 opiniach (łatwość 4,5, value for money 4,7, obsługa 4,8). Wady z opinii: wysoki koszt dla małych firm (04.2026), interfejs mógłby być przyjaźniejszy (06.2026), długie wdrożenie automatyzacji (08.2026), brak lepszego importu wariantów z WooCommerce (10.2022), roczny problem z synchronizacją 500 produktów zaimportowanych z eMAG (05.2023) — [Capterra: Base](https://www.capterra.com/p/245981/Base/)
- Wady według recenzji z 2026: wysoki koszt przy dużym wolumenie (bez progów ilościowych), dopłaty za kolejne hurtownie i częstszą synchronizację, ogrom funkcji przytłacza początkujących, niezbyt nowoczesny interfejs, brak czatu na żywo. Pełna konfiguracja zajmuje kilka dni. Recenzent podsumowuje, że skargi rzadko dotyczą tego, czego system nie umie, a częściej tego, ile kosztuje — [jakwybrachosting.pl](https://jakwybrachosting.pl/recenzja-baselinker/)

### Inferences
- Base nie rozwiązuje przypadku „mały sklep na Shoper/WooCommerce + dowolny plik od niszowego dostawcy". Brakuje mu XLS, PDF i XML o nieznanej strukturze, wariantów przy imporcie z pliku i bezpośredniego zasilania sklepu z hurtowni. Do tego dochodzi minimum 279 zł/mies., gdy potrzeba więcej niż jednej hurtowni z pliku.
- Podwyżki i złożoność narzędzia to nośny argument marketingowy dla prostego, taniego narzędzia jednozadaniowego.

### Gaps
- Nie znalazłem opinii Trustpilot ani G2 o Base z 2025–2026 (w wynikach był tylko Capterra). Wykop i fora PL widoczne tylko pośrednio w recenzji jakwybrachosting.
- Nie sprawdziłem, czy import CSV w Base zapamiętuje szablon mapowania i czy działa cyklicznie z URL (strona pomocy tego nie podaje).
- Brak oficjalnego potwierdzenia opłat 10–200 zł za częstszą synchronizację z hurtownią.

---

## 2. Apilo: integracje z hurtowniami, aplikacje Shoper, cennik

### Takeaway
Apilo (właściciel: Shoper/grupa) ma około 400 gotowych hurtowni. Shoper nie ma własnej integracji z hurtowniami i odsyła do aplikacji Apilo: 99 zł/mies. za 3 hurtownie albo 649 zł/rok za 1 hurtownię. Hurtownia spoza listy wymaga płatnego wdrożenia od 599 zł jednorazowo, więc Apilo nie oferuje samoobsługowego „dowolnego pliku". Dane z hurtowni pobierane są maksymalnie 3 razy dziennie, a produkty trafiają do sklepu ręcznie (CSV lub formularz).

### Cited Findings
- Koszt hurtowni: pierwsza z listy za -50% (Starter) lub bez dopłat (Basic i wyżej), każda kolejna 59 zł/mies. Podłączenie hurtowni spoza listy od 599 zł netto jednorazowo (analiza 300 zł płatna z góry + wdrożenie od 299 zł) — [Pomoc Apilo: podłączenie hurtowni](https://apilo.com/pl/help/podlaczenie-hurtowni-import-xml-csv/) (aktualizacja 08.2026)
- Konfiguracja: link do pliku FULL XML/CSV oraz LIGHT, FTP albo API; prefiks SKU dla każdej hurtowni; narzut %; wybór pola ceny (podstawowa lub zakupu); reguły stanów (np. 0–3 szt. → 0); filtry (kategoria, marka, minimalny stan, przedział cen, pomijanie produktów bez zdjęć). Pobieranie z hurtowni 3 razy dziennie. Zdjęcia dociągane są w tle i mogą się importować „od kilku do kilkunastu godzin" — [Pomoc Apilo](https://apilo.com/pl/help/podlaczenie-hurtowni-import-xml-csv/)
- Aplikacje w Shoper App Store: „Dropshipping moduł Apilo" za 649 zł netto/rok (1 hurtownia, kolejne +45 zł/mies., Shoper + Allegro, do 1000 zamówień/mies.) oraz „Integracje z Hurtowniami" za 99 zł netto/mies. (3 hurtownie, kolejne +45 zł/mies., wiele kanałów, do 500 zamówień/mies.). W obu limit 50 000 ofert. Apilo nie wysyła automatycznie zamówień do hurtowni ani produktów do sklepu: przenosi się je plikiem CSV lub formularzem — [Pomoc Apilo: porównanie aplikacji](https://apilo.com/pl/help/aplikacja-integracje-z-hurtowniami-czy-dropshipping-modul-apilo-co-wybrac/) (aktualizacja 10.2025); [Shoper: Pakiet 3 Hurtownie](https://www.shoper.pl/aplikacje/integracje-z-hurtowniami); [Shoper: Dropshipping moduł Apilo](https://www.shoper.pl/aplikacje/dropshipping-modul-apilo)
- Lista hurtowni w aplikacji Shoper obejmuje generyczne pozycje „Plik XML wg schematu Ceneo / IOF / IOF (wielojęzykowy) / TrisoShop", czyli ustandaryzowane formaty da się podpiąć bez wdrożenia. Są tam też dublety typu „Aquario (nowy plik)" i „Sollux (stary plik)", co pokazuje, że zmiana pliku przez hurtownię wymaga nowego konektora — [Shoper: Pakiet 3 Hurtownie](https://www.shoper.pl/aplikacje/integracje-z-hurtowniami)
- Abonament Apilo po podwyżce z 1.09.2026: Starter 39 zł (do 2000 ofert), Basic 199 zł (do 10 000 ofert), Professional 399 zł, Optimum 799 zł, Advanced 999 zł. Synchronizacja „na żywo" stanów i cen jest płatna osobno, 59–349 zł/mies. za każdą. Dodatkowy użytkownik 9 zł — [EcomFlowLab, odczyt 13.10.2026](https://ecomflowlab.pl/baselinker-podrozal-migracja-apilo-sellasist/); oficjalny cennik: [apilo.com/pl/cennik-apilo](https://apilo.com/pl/cennik-apilo/) (nie zescrapowałem go w całości)
- Doświadczenia wdrożeniowca (07.2026): import z pliku kończył się statusem OK i zerem produktów, bo serwer hurtowni wysyłał XML z nagłówkiem HTML. W panelu importu brakowało przycisku „uruchom teraz" i logów, a zaplanowany import dwa razy się nie wykonał. Apilo nie ma typu produktu „wariant", więc warianty trzeba było zrobić obok, przez API sklepu. Godzinę po imporcie 17 080 z 28 890 produktów nie miało zdjęć, a eksport nie zgłosił błędu — [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/)
- Najczęstsza skarga po migracji z Base na Apilo (grupy FB, 2026): „i tak trzeba dokupić synchronizację" — [EcomFlowLab](https://ecomflowlab.pl/baselinker-podrozal-migracja-apilo-sellasist/)

### Inferences
- Apilo to główny „oficjalny" konkurent w ekosystemie Shoper, ale model „hurtownia z listy albo wdrożenie od 599 zł" zostawia lukę dla dostawców spoza listy, plików XLS/PDF i małych lokalnych dostawców. Brak wariantów i brak automatycznego zasilania sklepu to bezpośrednie bóle, które nasz produkt adresuje.

### Gaps
- Nie zweryfikowałem bezpośrednio pełnego cennika Apilo (dane za EcomFlowLab, 13.10.2026).
- Brak ocen aplikacji Apilo w Shoper App Store: strona nie pokazała ocen w scrapie.

---

## 3. Sellasist (integrator, alternatywa dla Base)

### Takeaway
Sellasist deklaruje ponad 200 hurtowni, ale ceny integracji z hurtowniami nie są publiczne („wyceniane osobno"). Abonament jest tańszy od Base przy dużym wolumenie, a użytkownicy skarżą się na trudny start.

### Cited Findings
- „200+" gotowych integracji z hurtowniami (odczyt 09.2026); integracje z hurtowniami wyceniane osobno, kwot nie ma w cenniku — [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/); [EcomFlowLab porównanie](https://ecomflowlab.pl/baselinker-podrozal-migracja-apilo-sellasist/)
- Abonament (13.10.2026): 59 zł (100 zamówień), 189 zł (500), 359 zł (1000), 699 zł (do 5000), 899 zł (10 000). Próg wyznacza wyższa z dwóch liczb: zamówienia albo aktywne oferty. Mini WMS kosztuje 50 zł/użytkownika — [EcomFlowLab](https://ecomflowlab.pl/baselinker-podrozal-migracja-apilo-sellasist/); oficjalny: [sellasist.pl/cennik](https://sellasist.pl/cennik)
- Opinie po migracji z Base (grupa FB, 10.2026, kilkanaście odpowiedzi, przytoczone przez autora): plusem jest cena i moduł magazynowy, minusem nieintuicyjny panel, dużo ustawień i słabsze masowe działania na Allegro; jedna firma zrezygnowała po trialu — [EcomFlowLab](https://ecomflowlab.pl/baselinker-podrozal-migracja-apilo-sellasist/)
- Strona produktu „Integracja z hurtowniami i dropshipping 2.0" (aktualizacja 10.2026) mówi o przekazywaniu zamówień dostawcom i wyliczaniu cen według marży; samoobsługowego mapowania dowolnego pliku na niej nie znalazłem — [Sellasist](https://sellasist.pl/rozwiazania/integracje-z-hurtowniami-i-dropshipping-2-0/)

### Gaps
- Nie wiadomo, czy Sellasist pozwala samodzielnie zmapować dowolny XML/CSV i ile kosztuje integracja hurtowni.

---

## 4. Sky-Shop: wbudowane integracje z hurtowniami i dropshipping

### Takeaway
Sky-Shop ma najbardziej rozbudowany wbudowany moduł hurtowni wśród platform SaaS (około 580 gotowych integracji). Płaci się osobno za moduł, według liczby hurtowni i częstotliwości aktualizacji: 49–319 zł/mies. Obsługuje tylko gotowe integracje z listy; publicznej informacji o samoobsługowym mapowaniu dowolnego pliku nie znalazłem.

### Cited Findings
- Cennik modułu „Integrator z hurtowniami": 1 hurtownia od 49 zł/mies. (umowa roczna, aktualizacja 1x/dobę) do 129 zł/mies. (umowa miesięczna, 12x/dobę); bez limitu hurtowni od 119 do 319 zł/mies. Częstotliwość aktualizacji do wyboru: 1x, 2x, 4x, 8x lub 12x na dobę. Moduł wysyła zamówienia do hurtowni średnio co 1 h. Ponad 580 hurtowni, z czego 305 dropshippingowych. Strona aktualizowana 07.2024 — [Sky-Shop: cennik modułu](https://sky-shop.pl/cennik-modul-integracji-z-hurtowniami/)
- Liczby gotowych integracji różnią się między źródłami: Shoper (porównanie Sky-Shop vs Shoper) podaje 577, w tym 302 dropshipping; platformy-ecommerce.pl pisze o „ponad 1200 hurtowniach" — [Shoper Learn](https://www.shoper.pl/learn/artykul/sky-shop-czy-shoper); [platformy-ecommerce.pl](https://platformy-ecommerce.pl/opinie/sky-shop/)
- Osobny cennik pakietów sklepu dla dropshippingu — [Sky-Shop: cennik dropshipping](https://sky-shop.pl/cennik-dropshipping/) (szczegóły nie zescrapowane)
- Strona cennika modułu nie mówi, czy da się podpiąć dowolny plik XML i za ile (ekstrakcja: brak informacji) — [Sky-Shop](https://sky-shop.pl/cennik-modul-integracji-z-hurtowniami/)

### Inferences
- Sky-Shop to silny konkurent w segmencie dropshipping z popularnymi hurtowniami. Klient Sky-Shop z nietypowym dostawcą (plik XLS/PDF od producenta) prawdopodobnie zostaje bez narzędzia, ale tego nie potwierdziłem.

### Gaps
- Nie znalazłem informacji, czy Sky-Shop wdraża hurtownię spoza listy i za ile. Nie zebrałem też opinii użytkowników o module.

---

## 5. IdoSell: import z pliku, IdoSell (IAI) Downloader, IOF

### Takeaway
IdoSell ma najbardziej zaawansowany wbudowany mechanizm wśród polskich platform: IdoSell/IAI Downloader importuje i aktualizuje ofertę z XML, CSV i IOF z przypisywaniem typów danych do kolumn. Dla nietypowego XML potrzebny jest jednak sterownik XSLT przygotowany pod daną ofertę, a dokumentacja zaleca konwersję innych formatów (np. XLS) do CSV/XML. IdoSell jest też autorem otwartego standardu IOF, w którym wiele hurtowni udostępnia pliki.

### Cited Findings
- IAI Downloader obsługuje CSV, XML i IOF (w tym gateway.xml w IOF 2.6). Po analizie pliku program wyświetla okno przypisania typów danych („przypisz typ danych"); w trybie oferty trzeba wskazać unikalny indeks towaru. Dla XML można wskazać „sterownik XSLT przygotowany specjalnie do danej oferty". Pliki w innych formatach trzeba zapisać do CSV/XML. Synchronizacja z URL lub FTP. Strona aktualizowana 10.2026 — [Pomoc IdoSell: integracja z hurtownią](https://pomoc.idosell.com/towary/iai-downloader/integracja-z-hurtownia)
- IdoSell opisuje Downloader jako program do importowania i aktualizowania oferty na podstawie danych od dostawcy (fragment z wyników wyszukiwania; pełna strona się nie załadowała) — [IdoSell Downloader](https://www.idosell.com/en/iai-downloader-automatic-import-offer-updates-and-integration-with-suppliers/)
- IOF (Internet Offer Format) to otwarty format IdoSell z osobnym plikiem pełnym i „light" do częstych aktualizacji cen i stanów; obok formatu Ceneo jest najczęstszym standardem plików hurtowni — [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/); [IdoSell IOF](https://www.idosell.com/pl/developers/otwarte-standardy-i-api-do-integracji/internet-offer-format-iof/)
- Hurtownie udostępniają gotowe pliki XML „dla IAI Downloadera" w panelu klienta (przykład: hurtownia yournewstyle.pl) — [yournewstyle.pl](https://yournewstyle.pl/tresc/jak-zintegrowac-sklep)
- Wokół IdoSell działa rynek usług i narzędzi do przygotowania importu: freelancer mhajok.pl (import do IdoSell z XML/CSV/XLSX, mapowanie wariantów, cen, stanów), PrePIM (integrator hurtowni z IdoSell z filtrami), SellStar — [mhajok.pl](https://mhajok.pl/import-produktow-idosell); [PrePIM](https://prepim.eu/integracje/hurtownie/idosell/); [SellStar](https://sellstar.pl/integracje-sklepow-z-hurtowniami/idosell-hurtownia/)

### Inferences
- Użytkownicy IdoSell mają najlepsze narzędzie wbudowane, ale istnienie płatnych usług (mhajok, PrePIM, SellStar) pokazuje, że XLSX, XSLT i warianty nadal sprawiają trudność. Dla IdoSell przewagą naszego produktu byłyby XLS/PDF, automatyczne mapowanie bez XSLT i diff zmian.

### Gaps
- Nie ustaliłem, czy Downloader jest aplikacją desktopową (Windows) czy webową ani czy jest płatny ponad abonament IdoSell: strony produktowe IdoSell nie załadowały się (timeout lub przekierowanie).
- Brak opinii użytkowników o Downloaderze (forum IdoSell nie było przeszukane).

---

## 6. Shoper: wbudowany import i aplikacje Shoper App Store

### Takeaway
Shoper ma wbudowany import i eksport CSV oparty na profilach (separator kolumn i kategorii, zakres danych), ale bez importu dowolnego XML od hurtowni i bez harmonogramu. Wsparcie dla wariantów wymaga osobnej aplikacji. Do hurtowni Shoper oficjalnie poleca aplikacje Apilo; są też aplikacje dedykowane pojedynczym hurtowniom (np. Incom za 189 zł/mies.) oraz nowa aplikacja AI Witly, bezpośredni konkurent.

### Cited Findings
- Import i eksport CSV w panelu Shoper działa przez profile: wybór zakresu danych, separatory kolumn i kategorii, które muszą być identyczne w pliku i profilu — [Shoper Learn: zarządzanie plikami CSV](https://www.shoper.pl/learn/artykul/zarzadzanie-plikami-csv)
- Stanami atrybutów i wariantów zarządza się po zainstalowaniu aplikacji „Import/Export CSV – Warianty i Atrybuty" — [Shoper Learn](https://www.shoper.pl/learn/artykul/zarzadzanie-plikami-csv-grupowe-dodawanie-producenta)
- „Shoper nie ma własnej integracji z hurtowniami, jego oficjalna strona odsyła do aplikacji Apilo (pakiet 3 hurtowni za 99 zł miesięcznie)" — [EcomFlowLab, 09.2026](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/); [Shoper: integracje z hurtowniami](https://www.shoper.pl/integracje-hurtownie)
- Aplikacje Apilo w Shoper App Store: Pakiet 3 Hurtownie (99 zł/mies.), Dropshipping moduł Apilo (649 zł/12 mies.), „Integracja z hurtowniami – Apilo" (+45 zł/mies. za hurtownię) — [Shoper App Store](https://www.shoper.pl/aplikacje/integracje-z-hurtowniami); [Dropshipping moduł Apilo](https://www.shoper.pl/aplikacje/dropshipping-modul-apilo); [Integracja z hurtowniami - Apilo](https://www.shoper.pl/aplikacje/integracja-z-hurtowniami-apilo)
- Aplikacja dedykowana jednej hurtowni: „Integracja z Incom" (import i aktualizacja stanów), subskrypcja 189 zł/mies. — [Shoper App Store: Incom](https://www.shoper.pl/aplikacje/integracja-z-incom)
- **Witly** („Import i edycja produktów AI") w Shoper App Store: ekosystem 20 agentów AI, import z hurtowni oraz plików CSV, XLS, XML i JSON, sterowanie poleceniem tekstowym lub głosowym — [Shoper App Store: Witly](https://www.shoper.pl/aplikacje/witly) (szczegóły w sekcji 9)
- Usługi wdrożeniowe dla Shoper (np. agencja Vinson, poradnik integracji Shopera z hurtownią przez import XML, marże i filtry) pokazują popyt na pomoc przy integracji — [vinson.agency](https://vinson.agency/blog/integracja-shopera-z-hurtownia-import-xml-i-automatyczna-aktualizacja-stanow)

### Inferences
- Użytkownik Shopera z dostawcą spoza listy Apilo ma do wyboru: ręczne przerabianie pliku do profilu CSV, płatne wdrożenie Apilo (od 599 zł) albo Witly. To najlepszy segment startowy dla naszego produktu. Witly jest jednak realnym konkurentem w tej samej niszy.

### Gaps
- Nie przejrzałem pełnej kategorii „Import/eksport" w Shoper App Store (np. ceny aplikacji „Import/Export CSV – Warianty i Atrybuty", aplikacje innych vendorów do importu XML).
- Na forum.shoper.pl nie szukałem skarg dotyczących importu.

---

## 7. WooCommerce: wtyczki do importu z hurtowni

### Takeaway
WooCommerce ma najbogatszy rynek wtyczek. Polska wtyczka WP Desk „Dropshipping Import Products" (329 zł/rok, 1 strona) obsługuje dowolny XML/CSV z mapowaniem drag & drop, wariantami, marżą i harmonogramem, czyli jest funkcjonalnie bliska naszemu pomysłowi. Nie obsługuje jednak XLS ani PDF, a wymaga hostingu, crona i konfiguracji technicznej. Wbudowany importer WooCommerce przyjmuje tylko CSV i nie ma harmonogramu.

### Cited Findings
- WP Desk „Dropshipping Import Products dla WooCommerce": 329 zł netto (404,67 zł z VAT), subskrypcja roczna na 1 stronę. Obsługuje XML i CSV od dostawcy, mapper z drag & drop, produkty proste, z wariantami i afiliacyjne, marżę i modyfikację cen, harmonogram (dni i godziny), decyzję co zrobić z produktami, które zniknęły z feedu. Ponad 700 aktywnych instalacji (według strony producenta) — [WP Desk PL](https://www.wpdesk.pl/sklep/dropshipping-xml-woocommerce/) (aktualizacja 08.2026)
- Darmowa wersja na WordPress.org: ocena 4,3/5 przy 11 opiniach (9× pięć gwiazdek, 2× jedna). W wersji PRO są m.in. cron, logika warunkowa, modyfikator cen, przenoszenie znikniętych produktów do kosza i więcej niż jedno zdjęcie. Negatywne opinie dotyczą opisu funkcji niezgodnego z działaniem (narzut procentowy per produkt) i braku reakcji supportu. Ostatnia zmiana w changelogu: 1.7.5 z 2026-11-05 — [WordPress.org](https://wordpress.org/plugins/dropshipping-xml-for-woocommerce/)
- Wbudowany importer WooCommerce przyjmuje tylko CSV i nie ma harmonogramu, więc do cyklicznych aktualizacji potrzebna jest wtyczka, np. WP All Import albo Dropshipping XML od WP Desk — [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/); [WooCommerce docs](https://woocommerce.com/document/product-csv-importer-exporter/)
- Witly deklaruje obsługę WooCommerce (sekcja 9) — [Witly cennik](https://witly.ai/cennik)

### Inferences
- Dla WooCommerce przewaga naszego produktu musiałaby leżeć w prostocie (SaaS bez hostingu i crona), obsłudze XLS/PDF, pamięci mapowania „per dostawca" w sensie nietechnicznym oraz raporcie diff przed importem. Sama obsługa dowolnego XML/CSV z mapowaniem już istnieje.

### Gaps
- Nie zweryfikowałem cen i ocen WP All Import ani innych wtyczek PL. Nazwy „Hurtapp" i „Sklepy24" z briefu nie pojawiły się w wynikach.

---

## 8. PrestaShop: moduły importu hurtowni

### Takeaway
Dla PrestaShop istnieje wiele polskich modułów od 399 do 1600 zł z dożywotnią licencją. PrestaShow Importer obsługuje dowolny XML/CSV/API z mapowaniem pól i kombinacjami. Moduł x13 jest dostarczany „pod konkretną hurtownię", a jego opis mówi wprost, że integracja nie jest uniwersalna. Cykliczność zapewnia CRON na serwerze sklepu.

### Cited Findings
- x13 „Import hurtowni – XML / CSV / API z AI ChatGPT": 399 zł netto, licencja 1 rok z supportem (opcje: 2 lata -10%, 3 lata -15%, dożywotnia). Obsługuje atrybuty i kombinacje, ma AI (ChatGPT) do opisów, tytułów i meta. Cytat: „Integracja nie jest uniwersalna. My przygotowujemy ją pod odpowiedni format pliku." Strona zawiera też sprzeczną informację o licencji dożywotniej — [x13.pl](https://x13.pl/integracje-prestashop/import-xml-do-prestashop.html)
- PrestaShow „PrestaShop Importer": Standardowa 650,41 zł netto, Profesjonalna 1300,81 zł netto, dożywotnia licencja na 1 sklep i 3 mies. wsparcia. „Moduł obsługuje wszystkie pliki i feedy XML oraz CSV"; mapowanie pól XML/CSV/API na pola PrestaShop; generowanie kombinacji z atrybutów; uruchamianie przez CRON, SSH lub ręcznie. 138 komentarzy, 82 recenzje w danych strukturalnych — [PrestaShow](https://prestashow.pl/pl/moduly-prestashop/5-prestashop-importer-integracja-z-hurtowniami-xml-csv-api.html)
- Inne aktywne moduły PL: PrestaDev „Import hurtownia Pro", SEIGI (integracje XML/CSV z hurtowniami, także thirtybees), Dobre Wtyczki (import XML/CSV/API z cenami z podatkiem i zakupu), Astrabit; na PrestaShop Addons są m.in. „Easy Import & Export Products: CSV, Excel, XML, JSON" i MyPrestaModules „Product Catalog Import & Update – CSV, Excel, XML" — [PrestaDev](https://prestadev.pl/pl/import-xml-hurtowania-prestashop.html); [SEIGI](https://seigi.eu/moduly-prestashop/integracja-z-hurtownia.html); [Dobre Wtyczki](https://dobrewtyczki.pl/moduly/105-import-hurtowni-xml-do-prestashop.html); [Astrabit](https://astrabit.com/p/xml-prestashop/); [Addons: Easy Import](https://addons.prestashop.com/pl/transfer-danych-kopia-zapasowa/24523-easy-import-products-from-csv-excel-xml-json-txt.html); [Addons: MyPrestaModules](https://addons.prestashop.com/en/data-transfer-backup/19091-product-catalog-csv-excel-import.html)
- Apilo eksportuje produkty do PrestaShop plikiem CSV — [Pomoc Apilo](https://apilo.com/pl/help/eksport-produktow-do-presta-plik-csv/)

### Inferences
- Rynek PrestaShop jest nasycony modułami jednorazowymi. Klient kupuje je raz i konfiguruje (często z pomocą wdrożeniowca). Model SaaS z abonamentem musi tu bronić się wygodą, obsługą XLS/PDF i diffem. Ceny modułów (400–1600 zł jednorazowo) wyznaczają punkt odniesienia dla wartości.

### Gaps
- Moduł „Mypresta PL" i „Sensbit" z briefu nie zostały zweryfikowane. Brak cen i ocen modułów PrestaDev, SEIGI, Dobre Wtyczki i Astrabit.

---

## 9. Niezależne narzędzia i narzędzia AI (2024–2026): kto robi „dowolny plik → plik importu"?

### Takeaway
Pojawiły się bezpośredni konkurenci oparci na AI. **Witly** (PL, Shoper/WooCommerce/PrestaShop, od 99 zł/mies., import XLS/XLSX/CSV/XML/JSON z zapamiętanym scenariuszem per plik i walidacją schematu) jest najbliższy naszej koncepcji. **SellStar** to polski PIM od 159 zł/mies. z importem od dostawców i mapowaniem AI. **Upsellr** to zagraniczny PIM z agentami AI (od 79 €/mies.), który czyta katalogi PDF, ale nie eksportuje do polskich platform. Feedink zajmuje się feedami wyjściowymi (marketing), nie importem od dostawców. Narzędzi „Imprezzo", „XMLimport" i „Zaufane hurtownie" nie znalazłem.

### Cited Findings
**Witly (witly.ai)**
- Artykuł z 12.03.2026 opisuje pipeline 4 agentów AI (planowanie, wykonanie, kontrola jakości, testy w przeglądarce). Obsługiwane formaty: XLS, XLSX, CSV, XML, JSON, JSONL. Agent planowania rozpoznaje strukturę i zadaje pytania: grupowanie wierszy w produkty i warianty, mapowanie kolumn, kategorie, duplikaty, tłumaczenia, HTML. Import cykliczny z URL działa według harmonogramu z raportem. Witly używa tego samego scenariusza przy kolejnych plikach, także ręcznie wgrywanych Exceli od dostawcy, waliduje zgodność schematu i powiadamia o zmianie formatu przed zmianami w sklepie. Platformy: Shoper, WooCommerce, PrestaShop — [Witly: import produktów](https://witly.ai/news/import-produktow)
- Cennik: od 99 zł netto/mies. z 10 000 kredytów, +100 zł za każde kolejne 10 000 kredytów; po wyczerpaniu kredytów płatne funkcje się wyłączają; 30 dni testu bez karty — [Witly cennik](https://witly.ai/cennik)
- Aplikacja jest dostępna w Shoper App Store („Import i edycja produktów AI — Witly") — [Shoper App Store](https://www.shoper.pl/aplikacje/witly)

**SellStar (sellstar.pl)**
- Polski PIM: łączy dane z wielu źródeł, ma mapowanie kategorii z AI (zatwierdzane przez człowieka), reguły wyliczania cen, tłumaczenia i automatyzacje. Oferuje też strony docelowe pod zadania typu „Import produktów z CSV/XML w Shoper" i „IdoSell i dane z hurtowni" — [SellStar platforma](https://sellstar.pl/platforma/); [SellStar Shoper CSV/XML](https://sellstar.pl/en/tasks/shoper/import-produktow-csv-xml); [SellStar IdoSell](https://sellstar.pl/integracje-sklepow-z-hurtowniami/idosell-hurtownia/)
- Cennik: Plus 159 zł/mies. (30 000 produktów, 3000 kredytów AI, 2 użytkowników), Max 299 zł (100 000 produktów), Ultra 599 zł (300 000 produktów); 14 dni testu bez karty; ceny końcowe (sprzedaż zwolniona z VAT). Oferty dostawców, z których nie utworzono produktu, nie liczą się do limitu; import pokazuje raport pominiętych pozycji — [SellStar cennik](https://sellstar.pl/cennik/)

**Upsellr (upsellr.io)**
- PIM z „zespołem agentów AI": importuje pliki dostawców, arkusze i katalogi PDF, przypisuje kolumny, a dane z PDF zachowują źródło. Pomoc obejmuje mapowanie pól, raporty importu i bibliotekę „Sources". Eksport do PrestaShop, Shopify, Akeneo, CSV/Excel, Amazon, ManoMano, Carrefour (bez Shoper, IdoSell i WooCommerce na stronie). Cena od 79 €/mies. (Core rocznie 948 €) — [Upsellr PL](https://www.upsellr.io/pl); [Upsellr pomoc: import](https://www.upsellr.io/pl/pomoc/tematy/import-produktow)

**Inne**
- Feedink: zarządzanie plikiem produktowym dla kanałów marketingowych (Ceneo, Google Shopping, Criteo, FB); import z XML, CSV, API lub crawlingu. Narzędzie służy do wyjścia ze sklepu, nie do importu od dostawcy do sklepu — [Feedink](https://feedink.com/)
- TrafficWatchdog „Agent AI do wprowadzania produktów" (automatyzacja pozyskiwania informacji produktowych, deklaracja obcięcia kosztu wdrożenia SKU o 80%); szczegółów i ceny nie sprawdzałem — [TrafficWatchdog](https://trafficwatchdog.pl/pl/blog/y2imlerqp6bd7bdn5q65lr1w/agent-ai-do-wprowadzania-produktow-jak-obciac-koszt-wdrozenia-sku-o-80)
- Usługi zamiast narzędzi: Zintegrujemy.pl (ZintHUB, abonament na integrację produktów z pliku XML/CSV), Variantai.lt (import od dostawców z XML/CSV/Excel/API na wycenę), Tracify (import cennika z Excela do Subiekta/Optimy) — [Zintegrujemy](https://zintegrujemy.pl/cennik-gotowych-integracji); [Variantai](https://variantai.lt/pl/uslugi-programistyczne/import-produktow-od-dostawcow/); [Tracify](https://systemy.tracify.pl/import-eksport-danych/)
- Inne platformy SaaS z wbudowanym importem XML/CSV hurtowni: Selly (integracja przez analizę pliku przez obsługę platformy), ShopGold, sStore (sklepywww.pl) — [Selly](https://www.selly.pl/integracja-z-hurtowniami-dropshipping-xml/); [ShopGold](https://www.shopgold.pl/import-produktow-z-plikow-xml-zewnetrznego-dostawcy-hurtowni-n-202.html); [sklepywww.pl](https://sklepywww.pl/hurtownie-i-dropshipping/)
- Wyszukiwanie „Feedink OR Imprezzo OR XMLimport OR Zaufane hurtownie" zwróciło wyłącznie Feedink; Imprezzo, XMLimport i Zaufane hurtownie się nie pojawiły — [wyniki wyszukiwania, 06.11.2026; brak trafień]

### Inferences
- Hipoteza „nikt nie robi PL platformy + dowolny dostawca" jest częściowo obalona: Witly od 03.2026 robi niemal dokładnie to (Shoper, Woo, Presta, XLS/CSV/XML, zapamiętany scenariusz, alert przy zmianie formatu), choć jako szeroki „ekosystem agentów", nie jako narzędzie jednozadaniowe. Nie znalazłem u Witly: obsługi PDF, eksportu dla IdoSell i Allegro ani czytelnego diffu biznesowego (nowe/usunięte produkty, zmiany cen i stanów) przed importem. To potencjalne pola różnicowania, które warto zweryfikować na trialu.
- PDF jako wejście obsługuje tylko Upsellr, który nie integruje się z polskimi platformami.

### Gaps
- Brak opinii użytkowników o Witly i SellStar (nowe produkty, w scrapie brak ocen w Shoper App Store).
- Nie wiem, ile kredytów Witly zużywa import pliku i aktualizacja (koszt per import).
- Nie zweryfikowałem, czy SellStar przyjmuje XLS/PDF: ekstrakcja ogólna to sugerowała, ale weryfikacja dosłowna na stronie cennika tego nie potwierdziła.

---

## 10. Porównanie zbiorcze i problemy przekrojowe

### Takeaway
Rynek dzieli się na (a) integratory z listą gotowych hurtowni (Base, Apilo, Sellasist, Sky-Shop), gdzie dostawca spoza listy oznacza wdrożenie lub API, (b) wtyczki i moduły per platforma (Woo, Presta), elastyczne, ale techniczne, bez XLS/PDF i bez diffu, (c) nowe narzędzia AI (Witly, SellStar, Upsellr). Wspólne bóle z wdrożeń to netto vs brutto, cennik detaliczny vs zakupowy, rozmiar w nazwie, warianty, duble EAN, stan „TAK/NIE", zmiany układu pliku i ciche błędy importu. Diff „co się zmieniło od ostatniego pliku" nie występuje jako funkcja w żadnym przebadanym narzędziu.

### Cited Findings
| Narzędzie | Platformy docelowe | Dowolny plik (samoobsługowo)? | XLS / PDF | Warianty | Cena (od) | Źródło |
|---|---|---|---|---|---|---|
| Base.com | marketplace'y; sklep pośrednio | CSV tak; XML tylko znana struktura | XLS nie; PDF nie | import z pliku: nie | 0 zł (≤100 zam.) / 279 zł + 0,99 zł/zam.; kolejne hurtownie 50 zł | [cennik](https://base.com/pl-PL/cennik/), [pomoc](https://base.com/pl-PL/pomoc/wiedza/import-produktow/) |
| Apilo | Shoper, Allegro, Presta (CSV), inne | nie (spoza listy od 599 zł wdrożenia); generyczne Ceneo/IOF tak | brak informacji | brak typu „wariant" (07.2026) | 39 zł/mies.; Shoper app 99 zł/mies. lub 649 zł/rok | [pomoc](https://apilo.com/pl/help/podlaczenie-hurtowni-import-xml-csv/), [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/) |
| Sellasist | sklepy, marketplace'y | brak informacji | brak informacji | brak informacji | 59 zł/mies.; hurtownie wyceniane osobno | [EcomFlowLab](https://ecomflowlab.pl/baselinker-podrozal-migracja-apilo-sellasist/) |
| Sky-Shop | tylko Sky-Shop | brak informacji (lista ~580) | brak informacji | brak informacji | moduł 49–319 zł/mies. | [Sky-Shop](https://sky-shop.pl/cennik-modul-integracji-z-hurtowniami/) |
| IdoSell Downloader | tylko IdoSell | tak (CSV/XML/IOF, XSLT dla XML) | konwersja do CSV/XML | brak informacji | brak informacji | [pomoc](https://pomoc.idosell.com/towary/iai-downloader/integracja-z-hurtownia) |
| WP Desk Dropshipping | WooCommerce | tak (XML/CSV, drag & drop) | nie | tak | 329 zł/rok | [WP Desk](https://www.wpdesk.pl/sklep/dropshipping-xml-woocommerce/) |
| PrestaShow Importer | PrestaShop | tak (XML/CSV/API) | brak informacji | tak (kombinacje) | 650 zł jednorazowo | [PrestaShow](https://prestashow.pl/pl/moduly-prestashop/5-prestashop-importer-integracja-z-hurtowniami-xml-csv-api.html) |
| x13 Import hurtowni | PrestaShop | nie („nie jest uniwersalna") | brak informacji | tak | 399 zł | [x13](https://x13.pl/integracje-prestashop/import-xml-do-prestashop.html) |
| Witly | Shoper, Woo, Presta | tak (AI, zapamiętany scenariusz) | XLS tak; PDF brak informacji | tak (grupowanie wierszy) | 99 zł/mies. (kredyty) | [Witly](https://witly.ai/news/import-produktow), [cennik](https://witly.ai/cennik) |
| SellStar | wiele (PIM) | tak (PIM, AI mapowanie kategorii) | niezweryfikowane | z wariantami w limicie | 159 zł/mies. | [SellStar](https://sellstar.pl/cennik/) |
| Upsellr | Presta, Shopify, marketplace'y EU | tak | PDF tak | brak informacji | 79 €/mies. | [Upsellr](https://www.upsellr.io/pl) |

Problemy z realnych wdrożeń (kilkanaście plików, 135 do prawie 30 tys. pozycji, 07–09.2026) — [EcomFlowLab](https://ecomflowlab.pl/integracja-sklepu-z-hurtownia/):
- W jednym z 5 plików był cennik detaliczny zamiast zakupowego. Netto/brutto oznaczył wprost tylko 1 dostawca z 5, a pomyłka przesuwa ceny o 23%. Skończyło się na 3 regułach cenowych dla 5 dostawców.
- Rozmiar w nazwie („ROZM. 43") udało się wyciągnąć automatycznie z 669 nazw na 1028.
- 60 zdublowanych EAN w jednym pliku, 165 pustych, 11 wierszy z przesuniętymi kolumnami. Pseudo-EAN-y hurtowni powodowały złe dopasowania kart na Allegro.
- Stan „TAK" czytany jest jako 1 szt.
- Zdjęcia 240–400 px są odrzucane przez Allegro; w jednym pliku tylko 46% pozycji miało zdjęcia.
- Integrator przenosi „płasko" wiersz na rozmiar i kolor: z 4667 pozycji zrobiło się 1069 kart z wyborem rozmiaru.
- Zmiany układu pliku zatrzymują import, nawet przy gotowych konektorach (dublety „nowy plik 2026" / „stary plik" na liście Apilo).

### Inferences
- Najsilniejsze, wciąż słabo pokryte różnicowanie dla naszego MVP: (1) diff vs poprzedni plik jako raport przed importem (nie znalazłem go u żadnego konkurenta), (2) wejście PDF i XLS dla polskich platform, (3) automatyczne wykrywanie netto/brutto, typu ceny, rozmiaru w nazwie i grupowania w warianty, (4) eksport jednocześnie do formatów Shoper, IdoSell, Woo, Presta i Allegro, (5) cena poniżej integratorów i bez minimalnego abonamentu 279 zł.
- Witly to najgroźniejszy bezpośredni konkurent: ma ten sam rynek (Shoper App Store), cenę 99 zł/mies., XLS i zapamiętywanie scenariusza. Przed dalszym budowaniem MVP warto zrobić test Witly na trialu (30 dni za darmo).

### Gaps
- Brak systematycznych opinii z wykop.pl i forum.shoper.pl; brak ocen aplikacji w Shoper App Store (scrap nie zwrócił ocen).
- Brak danych o udziale rynkowym i liczbie klientów poszczególnych narzędzi.

# Prompt: audyt rzetelności raportu o pomyśle na produkt

Użycie: otwórz NOWĄ rozmowę (najlepiej inny model albo inne narzędzie, z dostępem do internetu), wklej poniższy prompt, a na końcu wklej raport w miejsce `[WKLEJ RAPORT]`. Pola w nawiasach kwadratowych uzupełnij albo usuń.

---

Jesteś sceptycznym recenzentem due diligence. Twoim zadaniem NIE jest ocena pomysłu, tylko sprawdzenie, czy poniższy raport jest rzetelny i czy jego wnioski wynikają z dowodów. Raport napisał model językowy albo analityk, który mógł mieć skłonność do optymizmu, do potwierdzania założeń zleceniodawcy i do przedstawiania słabych dowodów jako mocnych.

Kontekst:
- Pomysł: [jedno zdanie]
- Rynek: [kraj/region]
- Ograniczenia twórcy: [np. solo, kilka tygodni, budżet]
- Data dzisiejsza: [data]. Sprawdzaj stan na dziś, nie na datę raportu.

Zasady:
- Masz dostęp do internetu, więc otwieraj linki i szukaj samodzielnie. Nie opieraj się na pamięci.
- Nie bądź przekorny dla zasady. Jeśli coś się zgadza, napisz, że się zgadza.
- Jeśli czegoś nie możesz sprawdzić, napisz „niesprawdzalne” i dlaczego. Nie zgaduj.
- Nie dopisuj nowych dowodów na korzyść pomysłu, jeśli ich nie znalazłeś w źródłach.

## Krok 1. Weryfikacja twierdzeń

Wypisz 15–25 najważniejszych twierdzeń raportu, od tych, na których opiera się werdykt, przez liczby i ceny, po konkurencję. Dla każdego:
- otwórz podany link i sprawdź, czy źródło naprawdę mówi to, co raport mu przypisuje,
- sprawdź datę źródła i czy dane są aktualne,
- oceń jakość źródła: oficjalne (firma, urząd, dokumentacja) / niezależne badanie / blog, agregator, materiał marketingowy / snippet z wyszukiwarki bez otwarcia strony.

Wynik podaj w tabeli: twierdzenie | link | werdykt (potwierdzone / częściowo / nieprawdziwe / nieaktualne / niesprawdzalne) | jakość źródła | komentarz.

## Krok 2. Błędy rozumowania

Sprawdź raport pod kątem tych typowych błędów i dla każdego znalezionego podaj cytat albo miejsce w raporcie:

1. **Podaż mylona z popytem.** Np. liczba ofert freelancerów, liczba konkurentów, liczba wątków założonych przez innych twórców przedstawiona jako dowód, że klienci chcą płacić.
2. **„Ludzie mają problem” zamiast „ludzie płacą za rozwiązanie”.** Czy jest choć jeden dowód faktycznej zapłaty: kwoty, cenniki z klientami, budżety zleceń, opinie płacących użytkowników?
3. **Dowody z innego rynku.** Czy dowody pochodzą z kraju lub segmentu, o którym jest raport? Czy przeniesienie wniosków jest uzasadnione?
4. **Założenia udające fakty.** Szacunki rynku (TAM/SAM), odsetki, konwersje. Czy są jasno oznaczone? Co się stanie z wnioskiem, jeśli założenie jest 3 razy gorsze?
5. **Brak dowodu przedstawiony jako luka rynkowa.** „Nie znaleziono funkcji X u konkurenta” to nie to samo co „konkurent nie ma X”. Ile luk opiera się tylko na tym, że czegoś nie znaleziono?
6. **Pominięte substytuty.** Czy raport uwzględnia: robienie tego ręcznie, Excel, ogólne narzędzia AI (ChatGPT, Claude, Gemini), wbudowane funkcje platform, zatrudnienie osoby, integratorów? Który z nich jest dziś realną alternatywą?
7. **Pominięta konkurencja.** Wyszukaj samodzielnie 5–10 fraz, którymi klient szukałby rozwiązania (w języku rynku). Czy znalazłeś konkurentów, których raport nie wymienia?
8. **Niespójności.** Czy werdykt na początku zgadza się z dowodami i ryzykami opisanymi dalej? Czy liczby w różnych sekcjach się zgadzają?
9. **Optymizm w doborze.** Czy dowody przeciw pomysłowi są opisane równie szczegółowo jak dowody za? Czy raport mówi, co oznaczałby brak sukcesu?
10. **Świeżość.** Czy coś zmieniło się w ostatnich 12 miesiącach (nowi gracze, zmiany cen, nowe funkcje platform, regulacje, możliwości AI), co osłabia wnioski?

## Krok 3. Kontrdowody

Poszukaj aktywnie dowodów PRZECIW pomysłowi: wątków, w których ludzie mówią, że problem rozwiązali inaczej albo że nie jest ważny; zamkniętych startupów z tym samym pomysłem; opinii, że ludzie nie chcą za to płacić. Podaj 3–10 pozycji z linkami albo napisz wprost, że nic nie znalazłeś.

## Krok 4. Ocena końcowa

1. **Ocena rzetelności raportu** w skali 1–5 z jednym zdaniem uzasadnienia.
2. **Co w raporcie jest najmocniejsze** (maks. 3 punkty) i **najsłabsze** (maks. 5 punktów).
3. **Poprawiony werdykt** w 3–5 zdaniach, oparty wyłącznie na tym, co zostało potwierdzone. Podaj subiektywne prawdopodobieństwo (w %), że w ciągu 6 miesięcy znajdzie się co najmniej 10 płacących klientów, i wyjaśnij, z czego wynika.
4. **Trzy najważniejsze niewiadome**, które rozstrzygają o sensie pomysłu, i dla każdej **najtańszy test** (do 2 tygodni, bez budowania produktu) z liczbowym progiem „kontynuować / porzucić”.

Pisz konkretnie i krótko. Bez ogólników typu „warto zrobić więcej badań”: zawsze mów, jakich badań, gdzie i z jakim progiem.

---

[WKLEJ RAPORT]

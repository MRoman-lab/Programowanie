# Programowanie Zaawansowane - Projekt Klient-Serwer

## Skład zespołu
* Jakub Pawłowski - nadzór nad architekturą, integracja wygenerowanego kodu, weryfikacja założeń biznesowych oraz ręczne testowanie scenariuszy brzegowych.
* Mateusz Romańczuk - implementacja modeli danych, obsługa wyjątków sieciowych (w tym ClassCastException), przetwarzanie danych przy użyciu Stream API oraz przygotowanie dokumentacji technicznej.

## Instrukcja techniczna
### Wymagania
* Java 19 (lub nowsza)
* Środowisko IDE (np. IntelliJ IDEA)

### Uruchomienie aplikacji
1. Skompiluj projekt w swoim środowisku IDE.
2. Uruchom klasę Serwer (plik Serwer.java). W konsoli pojawi się informacja o nasłuchiwaniu na porcie 8080 oraz logi inicjalizacji mapy.
3. Uruchom klasę Klient (plik Klient.java). Klient nawiąże połączenie, pobierze dane z użyciem Stream API oraz celowo wywoła błąd rzutowania (ClassCastException) w celu jego obsłużenia.
4. Aby przetestować limit połączeń, uruchom cztery instancje klasy Klient równocześnie. Czwarty klient otrzyma natychmiastowy status REFUSED.

### Uruchomienie testów
1. Upewnij się, że biblioteka JUnit 5 (wersja 5.8.1 lub nowsza) jest dodana do classpath projektu.
2. Przed uruchomieniem testów zamknij wszystkie działające ręcznie instancje serwera, aby zwolnić port 8080.
3. Uruchom klasę AplikacjaTest. Przeprowadzi ona automatycznie testy jednostkowe, integracyjne oraz E2E (weryfikacja limitu klientów).

## Deklaracja użycia sztucznej inteligencji
[cite_start]W trakcie realizacji projektu w szerokim zakresie korzystano z asystenta AI (Google Gemini)[cite: 44].
* *Zastosowanie:* Narzędzie posłużyło do wygenerowania głównego szkieletu aplikacji klient-serwer na gniazdach (Socket) oraz implementacji mechanizmu wielowątkowości (klasa ObslugaKlienta implementująca Runnable). AI napisało również pełny zestaw zautomatyzowanych testów w JUnit 5, modele danych wraz z wymaganymi metodami oraz pomogło zdiagnozować i ominąć błąd uszkodzonego nagłówka przy serializacji obiektów przesyłanych przez sieć.
* *Przykładowe prompty:* * "Napisz szkielet serwera w Javie obsługującego wielu klientów za pomocą wątków, z twardym limitem MAX_CLIENTS."
  * "Jak odsyłać obiekty przez ObjectOutputStream tak, aby u klienta wywołać celowy błąd ClassCastException używając Stream API?"
  * "Napisz testy E2E w JUnit 5, które udowodnią, że czwarty podłączający się do serwera klient zostanie automatycznie odrzucony."

# Raport z Audytu Aplikacji juice-shop

Wersja raportu: 1
Data raportu: 12.01.2022
Wykonali: Bartłomiej Kołodziejczyk, Aleksandra Grębosz


## 1. Podsumowanie

Przeprowadzony audyt aplikacji juice-shop wykonany był jako audyt zgodności ze
standardem Application Security Verification Standard 4.0.3, a także weryfikował
ogólny stan bezpieczeństwa aplikacji.

Ogólny stan zgodności aplikacji ze standardem ,,Application Security Verification
Standard 4.0.3 można określić jako Bardzo Słaby.

Problemy wpływające między innymi na niezgodność aplikacji z wymaganiami to między innymi:

```
● Możliwość logowania jako administrator
● Możliwość utworzenia skryptu do łamania haseł innych użytkowników
● Wykorzystywanie User ID innych użytkowników
● Dostęp do prywatnych zasobów innych użytkowników
● Brak walidacji metody płatności
● Słabe zabezpieczenia uwierzytelniania
```
## 2. Zakres i cele

**2.1 Cel i metodologia audytu**

Celem przeprowadzenia audytu była weryfikacja spełnienia standardu
bezpieczeństwa ASVS 4.0 na poziomie 1 wobec nowoczesnej aplikacji webowej
juice-shop.

Wybrano ASVS 4.0 ponieważ oferuje szeroki zakres bezpieczeństwa wobec aplikacji
webowych. 

**2.2 Zakres audytu**

Zakres audytu to wybrane luki aplikacji z przedstawionymi rozwiązaniami naprawy

Audyt obejmuje poniższe obszary:

```
V2 Uwierzytelnianie
V3 Zarządzanie sesją
V4 Kontrola Dostępu
V5 Walidacje, sanityzacja i kodowanie
V6 Kryptografia
V7 Obsługa błędów i logowanie
V8 Ochrona danych
V9 Komunikacja
V10 Złośliwy kod
V11 Logika biznesowa
V12 Pliki i zasoby
```
**2.3 Wykonanie czynności**

W ramach audytu zostały wykonane następujące czynności
● Analiza kodu na środowisku testowym
● Analiza zwracanych wartości
● Analiza wybranych bibliotek wykorzystywanych przez aplikacje
● Analiza dokumentacji wykorzystywanych frameworków
● Testy na uruchomionej lokalnie aplikacji

**2.4 Napotkane ograniczenia**

Audytowana aplikacja nie posiada ograniczeń. Kod jest udostępniony i zahostowany.
Modyfikacje backendu zwracają statyczne strony z endpointami restowymi do
odpowiednich zapytań.

**2.5 Aplikacja**

Aplikacja Juice Shop jest napisany w Node.js, Express i Angular. Jest to aplikacja
zawierająca ogromną liczbę błędów o różnym stopniu trudności. Aby sprawdzić
swoje umiejętności hackerskie użytkownicy mogą przejść przez wszystkie poziomy i
wykonać całą tablice score-board.


## 3. Testowanie komponentów i obszarów

3.1 Wykres podatności:

![1](/1.jpg)

**Poziom ważności: Krytyczny**

Luki, które otrzymały ocenę krytyczną, zazwyczaj posiadają większość z poniższych
cech:

```
● Wykorzystanie luki prawdopodobnie doprowadzi do przejęcia kontroli nad
serwerami lub urządzeniami infrastruktury na poziomie użytkownika.
● Wykorzystanie jest zazwyczaj proste, w tym sensie, że atakujący nie
potrzebuje żadnych specjalnych danych uwierzytelniających ani wiedzy o
poszczególnych ofiarach, nie musi też przekonywać docelowego użytkownika,
na przykład za pomocą socjotechniki, do wykonania jakiejś specjalnej funkcji.
● W przypadku krytycznych luk, zaleca się jak najszybsze ich załatanie lub
aktualizację, chyba że istnieją inne środki zaradcze. Na przykład, czynnikiem
łagodzącym może być fakt, że instalacja nie jest dostępna z Internetu.
```
**Poziom ważności: Wysoki**

Luki, które uzyskały wysoki poziom istotności, zazwyczaj posiadają niektóre z
poniższych cech:


```
● Luka jest trudna do wykorzystania.
● Wykorzystanie jej może prowadzić do zwiększenia poziomu uprawnień.
● Wykorzystanie luki może spowodować znaczną stratę danych lub przestój w
pracy.
```
**Poziom ważności: Średni**

Luki, które osiągają średni poziom istotności, zazwyczaj posiadają niektóre z
poniższych cech:

```
● Podatności, które wymagają od atakującego manipulowania ofiarami za
pomocą taktyk socjotechnicznych.
● Podatności na ataki typu Denial of Service, które są trudne do
skonfigurowania.
● Exploity, które wymagają, aby atakujący znajdował się w tej samej sieci
lokalnej co ofiara.
● Luki, których wykorzystanie zapewnia jedynie bardzo ograniczony dostęp.
● Luki, które do skutecznego wykorzystania wymagają uprawnień użytkownika.
```
**Poziom istotności: Niski**

Luki o niskim poziomie istotności mają zazwyczaj bardzo mały wpływ na działalność
organizacji. Wykorzystanie takich podatności wymaga zazwyczaj lokalnego lub
fizycznego dostępu do systemu.

**Oceny CVSS v**

```
● 0.1 - 3.9 Niski
● 4.0 - 6.9 Średni
● 7.0 - 8.9 Wysoki
● 9.0 - 10.0 Krytyczny
```

## 4. Przegląd wyników i zaleceń

**4.1 Dostęp do cudzego koszyka**

**Poziom ryzyka: Średni**

Istnieje możliwość podmiany numeru ID koszyka z 25 na 26 otwierając tym samym zasoby
innego użytkownika.

Mój koszyk:
![1](/2.jpg)
Koszyk innego użytkownika:
![1](/3.jpg)

![1](/4.jpg)
Rozwiązania:

```
● Jeśli istnieje jeden koszyk dla konkretnego klienta powinno się zwracać bez
podawania numeru koszyka
● Trzymać dane zagnieżdżone w profilu użytkownika
● Dodać User ID do koszyka oraz sprawdzać czy pasuje z tokenem
```
**4.2 Deluxe membership**

**Poziom ryzyka: Krytyczny**

Brak walidacji karty kredytowej, wystarczy wpisać przypadkowe dane oraz numery karty i
automatycznie użytkownik zostaje uznany jako ‘Deluxe Membership’
![1](/5.jpg)

Rozwiązanie:

```
● Dodać walidacje przynajmniej po stronie serwera
● Najpierw dodać kartę na innej stronie tam sprawdzić jej ważność, a następnie w
metodzie płatności wybrać tą kartę. Dzięki temu pobieramy dane z bazy a nie od
użytkownika.
```
**4.3 Logowanie jako administrator**

**Poziom ryzyka: Krytyczny**

Poprzez bezpośrednie wpisanie e-maila do zapytania SQL możemy się zalogować jako
administrator.
![1](/6.jpg)

Rozwiązanie:

```
● Dodac walidaje SQLowych znaków dla każdej formy zapytań do bazy danych
(https://www.ptsecurity.com/ww-en/analytics/knowledge-base/how-to-prevent-sql-inje
ction-attacks/)
```

**4.4. Dodanie skargi z User ID innego użytkownika**

**Poziom ryzyka: Krytyczny**

Można wprowadzić zmianę User ID z 1 na 20, i następuje response 200
![1](/7.jpg)

Rozwiązanie:

```
● Pobierać User ID z tokena
```
**4.5. Feedback wysłany pod innym User**

**Poziom ryzyka: Krytyczny**

Zmiana User ID użytkownika pozwala na dodanie feedbacku jako inny użytkownik

Wprowadzona zmiana User ID z 1 na 30
![1](/8.jpg)

Rozwiązanie:
● Pobierać User ID z tokena

**4.6 Brak walidacji hasła**

**Poziom ryzyka:Średni**

Brak walidacji hasła po stronie serwera (sprawdzanie siły jedynie na FE)
![1](/9.jpg)
![1](/10.jpg)

**4.7 Wyświetlenie wybranej nazwy autora**

**Poziom ryzyka: Niski**

![1](/11.jpg)
![1](/12.jpg)
![1](/13.jpg)

Rozwiązanie:

```
● Pobieranie nazwy na backendzie z tokena lub bazy danych
```
**4.8 Wklejenie do filtra kodu, który się wykonuje**

**Poziom ryzyka: Niski**

![1](/14.jpg)

Rozwiązanie:

```
● Walidacja input value podczas wpisywania przed zatwierdzeniem
```
**4.9 Wartość null dla gwiazdek w feedbacku**

**Poziom ryzyka:Niski**

![1](/15.jpg)
![1](/16.jpg)

Rozwiązanie:

```
● Dodanie funkcji sprawdzającej po stronie FE czy wartość istnieje -> jeżeli nie
wyświetla -> nie wyświetlaj
```
**4.10 Skrypt do łamania haseł**

**Poziom ryzyka:Krytyczny**

Możliwe jest napisanie skryptu do łamania haseł z powodu braku zabezpieczenia do
formularza zmiany hasła. Istnieje możliwość na wysyłanie nieskończonej liczby próśb przez
co mozna sprawdzac rozne kombinacje dla szukanego hasła.
![1](/17.jpg)

Rozwiązanie:

```
● Dla danego IP istnieje ograniczona ilość prób. Następnie po jej przekroczeniu
następuje kara czasowa/zablokowanie konta.
```
**4.11 Dostęp do zasobów płatnych**

**Poziom ryzyka: Krytyczny**

Każdy użytkownik może pobrać płatny zasób (dokladnie 3D print). Ściezka jest dostępna w
konfiguracji.
![1](/18.jpg)


Rozwiązanie:

```
● Aby zapobiec podobnemu wyciekowi należy trzymać taki zasób na backendzie w
osobnym folderze i udostępniać jedynie po dokonaniu poprawnej
autoryzacji/płatności
```


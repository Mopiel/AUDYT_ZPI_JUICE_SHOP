**4.1 Deluxe membership**

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
**4.2 Logowanie jako administrator**

Poprzez bezpośrednie wpisanie e-maila do zapytania SQL możemy się zalogować jako
administrator.
![1](/6.jpg)

Rozwiązanie:

```
● Dodac walidaje SQLowych znaków dla każdej formy zapytań do bazy danych
(https://www.ptsecurity.com/ww-en/analytics/knowledge-base/how-to-prevent-sql-inje
ction-attacks/)
```

**4.3. Dodanie skargi z User ID innego użytkownika**

Można wprowadzić zmianę User ID z 1 na 20, i następuje response 200
![1](/7.jpg)

Rozwiązanie:

```
● Pobierać User ID z tokena
```
**4.4. Feedback wysłany pod innym User**

Zmiana User ID użytkownika pozwala na dodanie feedbacku jako inny użytkownik

Wprowadzona zmiana User ID z 1 na 30
![1](/8.jpg)

Rozwiązanie:
● Pobierać User ID z tokena

**4.5 Brak walidacji hasła**

Brak walidacji hasła po stronie serwera (sprawdzanie siły jedynie na FE)
![1](/9.jpg)
![1](/10.jpg)

**4.6 Wyświetlenie wybranej nazwy autora**

![1](/11.jpg)
![1](/12.jpg)
![1](/13.jpg)

Rozwiązanie:

```
● Pobieranie nazwy na backendzie z tokena lub bazy danych
```
**4.7 Wklejenie do filtra kodu, który się wykonuje**

![1](/14.jpg)

Rozwiązanie:

```
● Walidacja input value podczas wpisywania przed zatwierdzeniem
```

**4.8 Skrypt do łamania haseł**

Możliwe jest napisanie skryptu do łamania haseł z powodu braku zabezpieczenia do
formularza zmiany hasła. Istnieje możliwość na wysyłanie nieskończonej liczby próśb przez
co mozna sprawdzac rozne kombinacje dla szukanego hasła.
![1](/17.jpg)

Rozwiązanie:

```
● Dla danego IP istnieje ograniczona ilość prób. Następnie po jej przekroczeniu
następuje kara czasowa/zablokowanie konta.
```


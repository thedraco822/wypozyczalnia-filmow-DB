# Wypożyczalnia Filmów

## Opis projektu
Projekt "Wypożyczalnia Filmów" to system zarządzania wypożyczalnią filmów, zaimplementowany w SQL. Baza danych obsługuje informacje o klientach, filmach, pracownikach, wypożyczeniach, opłatach i promocjach. System zawiera tabele, wyzwalacze (triggery) oraz dane testowe, które umożliwiają zarządzanie procesem wypożyczania filmów, naliczania opłat i przypisywania promocji.

### Funkcjonalności
- Rejestracja klientów i ich danych kontaktowych.
- Zarządzanie katalogiem filmów (tytuł, gatunek, rok produkcji, liczba kopii, reżyser).
- Obsługa wypożyczeń z automatycznym zmniejszaniem liczby kopii filmów.
- Rejestracja opłat za wypożyczenia.
- Zarządzanie promocjami i przypisywanie ich do klientów.
- Zarządzanie danymi pracowników wypożyczalni.

### Struktura bazy danych
Baza danych składa się z następujących tabel:
- **WYF_KLIENCI**: Przechowuje dane klientów (imię, nazwisko, email, telefon).
- **WYF_PRACOWNICY**: Informacje o pracownikach (imię, nazwisko, stanowisko, wynagrodzenie).
- **WYF_FILMY**: Katalog filmów (tytuł, gatunek, rok produkcji, liczba kopii, reżyser).
- **WYF_WYPOŻYCZENIA**: Rejestruje wypożyczenia (data wypożyczenia, data zwrotu, klient, film, koszt).
- **WYF_OPLATY**: Przechowuje dane o opłatach za wypożyczenia.
- **WYF_PROMOCJE**: Informacje o promocjach (nazwa, rabat, daty ważności).
- **WYF_KLIENCI_PROMOCJE**: Relacja wiele-do-wielu między klientami a promocjami.

Schemat bazy danych można znaleźć w pliku `docs/BAZA_WYP.pdf`.

### Wymagania
- Serwer bazy danych zgodny z Oracle SQL (np. Oracle Database, Oracle SQL Developer).

### Instalacja
1. Sklonuj repozytorium:
   ```bash
   git clone https://github.com/<twoj-username>/wypozyczalnia-filmow.git
2. Skonfiguruj serwer bazy danych Oracle.
3. Wykonaj skrypt sql/BAZA_WYP.sql w narzędziu SQL, aby utworzyć tabele i wstawić dane testowe:
@sql/BAZA_WYP.sql

### Użycie
Skrypt BAZA_WYP.sql tworzy wszystkie tabele, wyzwalacze i wstawia przykładowe dane.
Wyzwalacz decrease_copies_after_rental automatycznie zmniejsza liczbę kopii filmu po wypożyczeniu.
Wyzwalacz TRG_AFTER_INSERT_WYPOZYCZENIA automatycznie rejestruje opłaty po dodaniu wypożyczenia.
Aby dodać nowe dane, użyj poleceń INSERT w odpowiednich tabelach.

### Przykładowe zapytania
1. Sprawdzenie aktywnych promocji dla klienta:
SELECT * FROM WYF_FILMY;
2. Sprawdzenie aktywnych promocji dla klienta:
SELECT k.imie, k.nazwisko, p.nazwa_promocji, p.rabat
FROM WYF_KLIENCI k
JOIN WYF_KLIENCI_PROMOCJE kp ON k.id_klienta = kp.id_klienta
JOIN WYF_PROMOCJE p ON kp.id_promocji = p.id_promocji
WHERE kp.status = 'aktywna';

### Uwagi
- Plik BAZA_WYP.sql zawiera przykładowe dane, takie jak filmy (np. "Inception", "The Godfather") i klienci.
- Upewnij się, że serwer bazy danych obsługuje składnię Oracle SQL.
- W przypadku błędów związanych z kluczami obcymi, upewnij się, że tabele są tworzone w odpowiedniej kolejności.
[BAZA_WYP.pdf](https://github.com/user-attachments/files/21164420/BAZA_WYP.pdf)

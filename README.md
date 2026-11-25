# 🚗 Carpooling – Miejski System Współdzielenia Przejazdów

Wieloplatformowa aplikacja (iOS, Android, Windows) wspierająca codzienne dojazdy w obrębie miasta i aglomeracji, zaprojektowana w oparciu o model **Ekonomii Współdzielenia (Sharing Economy)**. System łączy kierowców pokonujących swoje stałe lub planowane trasy z pasażerami podróżującymi w tym samym kierunku, automatyzując rezerwacje miejsc, niezarobkowy podział kosztów paliwa oraz naliczanie benefitów miejskich. Projekt realizowany z zachowaniem dobrych praktyk inżynierii oprogramowania oraz poparty analizą europejskiego rynku mobilności miejskiej.

## 👥 Autorzy
- Szymon Masalski
- Michał Chomontowski
- Gabriel Smyk
- Daniel Wawrzos
- Jan Praga
- Jakub Bandurski
- Anna Kalinowska

## 🎯 Funkcjonalności i Założenia Systemu
*(Sekcja aktualizowana na bieżąco wraz z wdrażaniem kolejnych modułów)*

- **Model Domenowy i Baza Danych:** Relacyjna struktura danych odwzorowująca kluczowe encje systemu (`Uzytkownik`, `Pojazd`, `Trasa`, `Przystanek`, `Rezerwacja`, `PortfelWirtualny`, `Ocena`, `BenefitMiejski`) wraz z konfiguracją powiązań pomiędzy użytkownikami, przejazdami i transakcjami.
- **Publikacja i Zarządzanie Trasami:** Moduł umożliwiający kierowcom dodawanie planowanych przejazdów (punkt startowy, docelowy, przystanki pośrednie, harmonogram, liczba wolnych miejsc) z automatyczną kalkulacją sugerowanego udziału w kosztach paliwa.
- **Wyszukiwarka i Rezerwacja Miejsc Online:** Przeglądanie i filtrowanie dostępnych przejazdów przez pasażerów (według lokalizacji, przedziału czasowego, przebiegu trasy oraz średniej ocen kierowcy) wraz z obsługą rezerwacji miejsc w czasie rzeczywistym.
- **Rozliczanie Kosztów (Wirtualny Portfel):** Bezgotówkowy mechanizm partycypacji w kosztach paliwa i eksploatacji samochodu między kierowcą a pasażerami przy użyciu wewnętrznej wirtualnej waluty w aplikacji.
- **Integracja z Benefitami Miejskimi (Współpraca B2G):** Zaprojektowany na podstawie analizy rynku europejskiego moduł gratyfikacji we współpracy z Urzędem Miasta dla kierowców oferujących „podwózki” (m.in. punkty lojalnościowe wymienne na bilety komunikacji miejskiej, zniżki w Strefie Płatnego Parkowania lub priorytet na parkingach P+R).
- **System Zaufania i Recenzji:** Dwustronny mechanizm wystawiania ocen i opinii po zakończonym przejeździe (kierowca ↔ pasażer), wspierający bezpieczeństwo i wiarygodność społeczności.
- **Autoryzacja i Role Użytkowników:** Bezpieczny moduł rejestracji i logowania z podziałem uprawnień:
  - **Niezalogowany:** Dostęp do publicznej wyszukiwarki tras oraz informacji o programie benefitów miejskich.
  - **Użytkownik (Kierowca / Pasażer):** Publikacja tras, rezerwacja miejsc, obsługa wirtualnego portfela, wymiana punktów miejskich oraz wystawianie ocen.
  - **Administrator:** Moderacja użytkowników i zgłoszeń oraz zarządzanie pulą benefitów we współpracy z Urzędem Miasta.

## 🛡️ Architektura, Model Biznesowy i Bezpieczeństwo Danych
- **Gwarancja Niezarobkowego Charakteru Przejazdów:** System limituje maksymalny udział pasażera w kosztach na podstawie długości trasy i średniego zużycia paliwa, dzięki czemu platforma realizuje model koleżeńskiego podziału kosztów (Carpooling), a nie komercyjnego przewozu osób.
- **Ochrona Integralności Danych i Rozliczeń:** W celu zabezpieczenia historii transakcji w wirtualnym portfelu, wystawionych opinii oraz naliczonych punktów miejskich, usunięcie konta użytkownika nie powoduje kaskadowej utraty danych powiązanych (zastosowanie anonimizacji danych osobowych przy zachowaniu spójności rekordów historycznych).
- **Weryfikacja Wspólnych Przejazdów (Anti-Fraud):** Naliczanie benefitów w ramach współpracy z Urzędem Miasta wymaga obustronnego potwierdzenia odbycia podróży (kod QR / weryfikacja startu i końca trasy), co zapobiega generowaniu fikcyjnych przejazdów.
- **Prywatność Lokalizacji i Zarządzanie Sekretami:** Dokładne punkty początkowe/końcowe kierowcy są maskowane do momentu akceptacji rezerwacji. Klucze dostępowe do bazy danych w chmurze oraz API map są wykluczone z repozytorium (obsługa przez plik `.env` / `--dart-define`).

## 📂 Struktura Repozytorium
- `/docs` – Analiza europejskiego rynku carpoolingu (na podstawie raportów *Deloitte* oraz badań mobilności miejskiej) i projekt systemu benefitów we współpracy z Urzędem Miasta.
- `/lib` – Kod źródłowy aplikacji Flutter (ekrany, modele, serwisy API, logika biznesowa).
- `.env.example` – Szablon wymaganych zmiennych środowiskowych (adres i klucze bazy online).

## 💻 Technologie
- **Frontend (Multiplatform):** Flutter, Dart (wsparcie dla Windows, iOS, Android)
- **Backend i Baza Danych (Online):** Supabase (PostgreSQL + Auth), Stripe
- **Mapy i Geokodowanie:** OpenStreetMap (`flutter_map`), OSRM / Nominatim

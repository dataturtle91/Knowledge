# Działanie sklepu internetowego przez pryzmat modelu OSI

Model **OSI** (Open Systems Interconnection) składa się z 7 warstw. Każda z nich ma swoje odpowiedniki w działaniu sklepu internetowego.

---

## 7. Warstwa aplikacji
To tutaj klient ma kontakt z interfejsem sklepu.

- **HTTP/HTTPS** – przesyłanie stron i danych o produktach.  
- **TLS/SSL** – szyfrowanie logowania, płatności, danych osobowych.  
- **Przykłady w sklepie:**  
  - **Wyświetlenie strony** – przeglądarka wysyła żądanie `GET /`, serwer odpowiada stroną główną.  
  - **Logowanie na konto klienta** – `POST /login` z danymi logowania (e-mail, hasło).  
  - **Zapis do newslettera** – `POST /newsletter` z adresem e-mail.  
  - **Dodanie do koszyka** – `POST /cart` z ID produktu.  
  - **Finalizacja zakupu** – `POST /checkout` z danymi dostawy i płatności.

---

## 6. Warstwa prezentacji
Odpowiada za **formatowanie i transformację danych**.

- Kodowanie/kompresja (np. gzip, brotli).  
- Szyfrowanie sesji (TLS handshake, certyfikaty).  
- **Przykłady w sklepie:**  
  - JSON z koszyka zamieniany na czytelną tabelkę w przeglądarce.  
  - Dane klienta (np. w logowaniu) szyfrowane protokołem TLS.  
  - Obrazy produktów kompresowane w locie (np. WebP).

---

## 5. Warstwa sesji
Zarządza **utrzymaniem i kontrolą sesji** między klientem a serwerem.

- **Utrzymanie logowania** – sesja użytkownika (cookie, token JWT).  
- **Koszyk użytkownika** – przypisanie do konkretnej sesji, nawet po przeładowaniu strony.  
- **Płatność online** – spójność sesji między stroną sklepu a bramką płatniczą.  
- **Przykłady w sklepie:**  
  - Klient loguje się i może przeglądać historię zamówień bez ponownego wpisywania hasła.  
  - Sesja newslettera – system rozpoznaje, czy adres e-mail już istnieje.  
  - Sesja API – np. integracja z systemem magazynowym.

---

## 4. Warstwa transportowa
Tutaj działa **TCP** – gwarancja dostarczenia danych.

- **Trójstopniowy handshake** przy nawiązywaniu połączenia.  
- **Kontrola przepływu** – dane ładowane bez gubienia pakietów.  
- **Przykłady w sklepie:**  
  - Wysyłanie danych logowania do serwera (`POST /login`).  
  - Dodanie e-maila do bazy newslettera.  
  - Przekazanie danych płatności do operatora.  
  - Pobieranie zdjęć produktów w całości i w odpowiedniej kolejności.

---

## 3. Warstwa sieciowa
Zapewnia **adresację i trasowanie**.

- Adres IP serwera sklepu i klienta.  
- Routing przez sieci operatorów i ISP.  
- **Zabezpieczenia:** firewall, filtrowanie ruchu, systemy IDS/IPS.  
- **Przykłady w sklepie:**  
  - Zapytanie klienta z Polski trafia do najbliższego serwera CDN (np. w Warszawie).  
  - Próba ataku brute force na logowanie blokowana przez firewall.  
  - Połączenie z API płatności kierowane do odpowiedniego centrum danych dostawcy.

---

## 2. Warstwa łącza danych
Odpowiada za **komunikację w ramach sieci lokalnej**.

- Przesył ramek Ethernet w centrum danych sklepu.  
- Komunikacja routerów, switchy, load balancerów.  
- Weryfikacja poprawności ramek (CRC).  
- **Przykłady w sklepie:**  
  - Serwer WWW komunikuje się z serwerem bazy danych przez sieć LAN.  
  - Load balancer rozdziela ruch logowania i płatności na różne serwery aplikacyjne.  

---

## 1. Warstwa fizyczna
Najniższy poziom – **fizyczny transport bitów**.

- Światłowody, kable Ethernet, fale radiowe (Wi-Fi, LTE).  
- Zasilanie, okablowanie, sygnały elektryczne/świetlne.  
- **Przykłady w sklepie:**  
  - Klient przegląda stronę przez Wi-Fi w domu.  
  - Dane z logowania płyną światłowodem operatora do centrum danych sklepu.  
  - Serwer w data center podłączony do redundantnych łączy operatorskich.

---

## Przykład – scenariusze działania

### 1. Logowanie na konto klienta
1. **Aplikacja (7):** klient wysyła dane logowania (`POST /login`).  
2. **Prezentacja (6):** dane szyfrowane TLS.  
3. **Sesja (5):** serwer tworzy sesję użytkownika.  
4. **Transport (4):** TCP dba o niezawodność przesyłu.  
5. **Sieć (3):** routing do adresu IP serwera sklepu.  
6. **Łącze (2):** przesył ramek przez sieć operatora i centrum danych.  
7. **Fizyczna (1):** bity idą przez Wi-Fi, światłowód, Ethernet.  

### 2. Zapis do newslettera
- Formularz `POST /newsletter` wysyła adres e-mail przez HTTPS.  
- Dane trafiają bezpiecznie przez warstwy 7–1.  
- System zapisuje adres w bazie i przypisuje do sesji klienta.

### 3. Wyświetlenie strony głównej
- Przeglądarka wysyła `GET /`.  
- Serwer odpowiada kodem HTML, który przechodzi przez wszystkie warstwy OSI.  
- TCP gwarantuje pełne przesłanie pliku HTML i obrazów produktów.  
- Użytkownik widzi stronę z ofertą sklepu.

---

## Podsumowanie
- **OSI** rozbija działanie sklepu na 7 poziomów – od kliknięcia klienta po przesył bitów w kablu.  
- **Praktyczne przykłady** (logowanie, newsletter, wyświetlenie strony, koszyk, płatność) pokazują, że każda warstwa jest niezbędna.  
- W e-commerce szczególnie kluczowe są:  
  - warstwa aplikacji (interakcja klienta),  
  - warstwa sesji (utrzymanie logowania i koszyka),  
  - warstwa transportowa (TCP – niezawodność).

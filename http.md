# Protokół HTTP – Notatki ChatGPT5

HTTP (Hypertext Transfer Protocol) to podstawowy protokół komunikacyjny w Internecie, używany do przesyłania danych pomiędzy klientem (np. przeglądarką) a serwerem. Jest protokołem **bezstanowym** – każda wiadomość (żądanie/odpowiedź) jest niezależna od poprzednich.

---

## Model działania HTTP

1. **Klient** (np. przeglądarka, aplikacja mobilna) wysyła żądanie do serwera.  
2. **Serwer** przetwarza żądanie i zwraca odpowiedź.  
3. Komunikacja zawiera:  
   - Linię startową (np. metoda i ścieżka w żądaniu).  
   - Nagłówki (metadane).  
   - Opcjonalne ciało (body).  

---

## Metody HTTP

- **GET** – pobiera zasób (np. strona produktu).  
- **POST** – przesyła dane do serwera (np. logowanie, dodanie do koszyka).  
- **PUT** – nadpisuje zasób (np. aktualizacja danych adresowych klienta).  
- **PATCH** – częściowa modyfikacja zasobu (np. zmiana statusu zamówienia).  
- **DELETE** – usuwa zasób (np. usunięcie adresu dostawy).  
- **HEAD** – pobiera nagłówki odpowiedzi (np. sprawdzanie dostępności pliku).  
- **OPTIONS** – sprawdza możliwości serwera (często w CORS).  
- **CONNECT** – tworzy tunel do serwera (np. HTTPS przez proxy).  
- **TRACE** – zwraca żądanie (debugowanie, rzadko używane).  

---

## Nagłówki HTTP

Nagłówki (headers) przenoszą metadane żądania i odpowiedzi. Mogą kontrolować zachowanie połączenia, format danych czy mechanizmy bezpieczeństwa.

### Kategorie nagłówków

- **Ogólne**  
  - `Date` – data odpowiedzi  
  - `Connection: keep-alive` – utrzymanie połączenia dla wielu żądań  

- **Żądania (Request Headers)**  
  - `Host: sklep.example.com`  
  - `User-Agent: Mozilla/5.0 (Windows NT 10.0)`  
  - `Accept: application/json` – klient oczekuje JSON (np. API e-commerce)  
  - `Authorization: Bearer <token>` – token JWT przy logowaniu  
  - `Cookie: sessionid=abc123` – sesja użytkownika sklepu  

- **Odpowiedzi (Response Headers)**  
  - `Server: nginx/1.23`  
  - `Content-Type: application/json`  
  - `Content-Length: 789`  
  - `Set-Cookie: sessionid=abc123; HttpOnly; Secure`  
  - `Cache-Control: no-store` – brak cache dla stron z danymi osobowymi  

- **Nagłówki bezpieczeństwa**  
  - `Strict-Transport-Security: max-age=31536000; includeSubDomains`  
  - `X-Content-Type-Options: nosniff`  
  - `X-Frame-Options: DENY`  
  - `Content-Security-Policy: default-src 'self'`  

---

## Statusy HTTP

- **1xx – Informacyjne**  
  `100 Continue`  

- **2xx – Sukces**  
  `200 OK` – operacja zakończona sukcesem  
  `201 Created` – zasób został utworzony  

- **3xx – Przekierowania**  
  `301 Moved Permanently` – zasób przeniesiony  
  `302 Found` – tymczasowe przekierowanie  

- **4xx – Błędy klienta**  
  `400 Bad Request` – źle sformatowane żądanie  
  `401 Unauthorized` – brak logowania  
  `403 Forbidden` – brak dostępu  
  `404 Not Found` – zasób nie istnieje  

- **5xx – Błędy serwera**  
  `500 Internal Server Error` – problem w backendzie  
  `503 Service Unavailable` – serwis przeciążony  

---

## Przykłady w e-commerce

- **Logowanie klienta** → `POST /login` + `Set-Cookie` z ID sesji.  
- **Dodanie produktu do koszyka** → `POST /koszyk` z ID produktu.  
- **Finalizacja zamówienia** → `POST /zamowienie` z danymi adresowymi i metodą płatności.  
- **Newsletter** → `POST /newsletter` z adresem e-mail (duplikat = `409 Conflict`).  

---

## Przykłady w bezpieczeństwie

- **Atak CSRF**  
  Brak tokena CSRF → atakujący może wymusić akcję.  
  Rozwiązanie: `SameSite=Strict` w cookie + dodatkowy token.  

- **Przechwycenie sesji**  
  Jeśli ciasteczko nie ma `Secure`, można je przechwycić.  
  Rozwiązanie: `Secure`, `HttpOnly`, `SameSite`.  

- **Nagłówki ochronne**  
  - `Content-Security-Policy` blokuje XSS.  
  - `X-Frame-Options` chroni przed clickjackingiem.  

---

## Cechy HTTP

- **Bezstanowy** – każda transakcja jest niezależna.  
- **Rozszerzalny** – możliwość definiowania własnych nagłówków.  
- **Niezależny od treści** – obsługuje dowolne typy danych (HTML, JSON, obrazy, wideo).  
- **Warstwowy** – może działać z proxy, CDN, load balancerami i firewallami WAF.  

---

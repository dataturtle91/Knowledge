# Źródło: ChatGPT 5
# Działanie sklepu internetowego przez pryzmat modelu TCP/IP

## 1. Warstwa aplikacji (HTTP/HTTPS, TLS)
To tutaj użytkownik **wchodzi na stronę sklepu** (np. `https://mojsklep.pl`).

- **HTTP/HTTPS** odpowiada za przesyłanie treści: kodu HTML, CSS, JavaScript, obrazów produktów, API koszyka itp.  
- **TLS (SSL)** szyfruje komunikację, aby nikt po drodze nie widział haseł, danych osobowych czy numerów kart.  
- **Przykłady w sklepie:**  
  - wyświetlenie strony produktu (`GET /produkt/123`),  
  - dodanie do koszyka (`POST /cart`),  
  - płatność przez bramkę płatniczą (`POST /checkout`).

---

## 2. Warstwa transportowa (TCP)
Tu działa **TCP**, czyli „kręgosłup” stabilnej komunikacji w e-commerce.

- **Ustanawianie sesji:** trójstopniowy handshake (`SYN`, `SYN-ACK`, `ACK`) – np. między przeglądarką a serwerem sklepu.  
- **Niezawodność:** TCP dba, aby wszystkie fragmenty strony dotarły i były w odpowiedniej kolejności.  
- **Kontrola przeciążenia i przepływu:** jeżeli serwer płatności jest obciążony, TCP spowalnia wysyłanie pakietów zamiast je gubić.  
- **Porty:**  
  - port 443 → sklep (HTTPS),  
  - porty API dostawcy płatności, systemu ERP, systemu magazynowego.

---

## 3. Warstwa sieciowa (IP)
Tu pakiety **znajdują drogę** od klienta do sklepu.

- **Adresacja:** przeglądarka klienta wysyła pakiet do adresu IP sklepu (np. `192.0.2.25`).  
- **Routing:** pakiet idzie przez różne routery i sieci dostawców, aż trafi do serwera hostującego sklep.  
- **Bezpieczeństwo:** firewall, WAF, monitoring logów mogą zatrzymać podejrzane połączenia (np. SQL injection, brute force).

---

## 4. Warstwa dostępu do sieci (Ethernet, Wi-Fi)
To **fizyczny transport**:

- U klienta – Wi-Fi lub LTE,  
- Po drodze – światłowody, przełączniki, serwery CDN, load balancery,  
- W firmie – sieć LAN centrum danych, gdzie stoi baza danych i aplikacja sklepu.

---

## 5. TCP w praktyce działania sklepu

### Przykład: dodanie produktu do koszyka
1. Przeglądarka wysyła żądanie HTTP (w HTTPS) przez TCP do serwera sklepu.  
2. TCP dzieli dane na segmenty, numeruje je, zapewnia retransmisję jeśli coś zginie.  
3. IP kieruje je do serwera sklepu.  
4. Serwer odpowiada (np. JSON z aktualnym koszykiem).  
5. Użytkownik widzi w aplikacji webowej odświeżony koszyk.  

### Przykład: płatność online
- **Niezawodność TCP** jest krytyczna – brak utraty pakietów = brak błędów w przesyłaniu danych karty lub autoryzacji płatności.  
- **TLS nad TCP** zapewnia poufność – dane karty nie lecą otwartym tekstem.  

---

## 6. Podsumowanie (TCP w e-commerce)
- **Bez TCP** – sklep by nie działał: strony by się ładowały niekompletnie, płatności mogłyby „gubić” dane, koszyk nie odświeżałby się poprawnie.  
- **TCP daje:** niezawodność, kontrolę przepływu, podział danych na strumienie (np. kilka zapytań jednocześnie: strona + API + płatność).  
- **W e-commerce** TCP gwarantuje stabilność zakupów i bezpieczeństwo danych.

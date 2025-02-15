# System biblioteczny
**Autorzy:** Michał Goławski, Maciej Dobrowolski, Marcin Bagnowski, Marcin Sikorski
**Opis tematu:** System do zarządzania biblioteką, jej księgozbiorem, wypożyczeniami oraz czytelnikami i pracownikami. 

## Budowa projektu
Projekt składa się z następujących mikroserwisów znajdujących się w poszczególnych repozytoriach:
- Frontend - https://github.com/Kapturz0ny/pis-frontend
- Gateway Api - https://github.com/Kapturz0ny/pis-gateway-api
- Auth Api - https://github.com/Kapturz0ny/pis-auth-api
- User Management Api - https://github.com/Kapturz0ny/pis-user-management-api
- Books Api - https://github.com/Kapturz0ny/pis-books-api
- Book Rent Api - https://github.com/Kapturz0ny/pis-book-rent-api

Dodatkowo przebieg prac był planowany i monitorowany z wykorzystaniem serwisu JIRA.

## Uruchomienie
Należy pobrać kod z każdego repozytorium.

### Frontend
Frontend należy uruchomić z poziomu głównego katalogu frontendu wykorzystując polecenie: 
	
	docker-compose up –build

### Mikroserwisy
Następnie należy uruchomić kolejne api w podanej kolejności, gdzie dla każdego z nich należy wykonać 2 polecenia (oba z poziomu głównego katalogu danego api)

Polecenie budujące projekt:

	mvn clean package -DskipTests

Polecenie uruchamiające kontenery: 
	
	docker-compose up –build

Kolejność uruchamiania api:
1. Gateway Api
2. Auth Api
3. User Management Api
4. Books Api
5. Book Rent Api

Początkowo bazy danych są puste dlatego możemy wprowadzić przykładowe dane do bazy książek z wykorzystaniem skryptu book_populate.sql w Books Api.

### Jenkins, Nexus (opcjonalne)
Teraz trzeba utworzyć połączenie z serwerem poprzez ssh z przekierowaniem odpowiednich portów. Na serwerze uruchomione są usługi Jenkins oraz Nexus. Bez tego połączenia można korzystać z aplikacji jednak spowoduje to brak dostępu do tych dwóch usług. Dostęp do serwera jest za pośrednictwem serwera pośredniego `mion.elka.pw.edu.pl`

Połączenie na serwer pośredni

	ssh username@mion.elka.pw.edu.pl -L 8081:localhost:<X> -L 8080:localhost:<Y>

Połączenie na serwer docelowy

	ssh username@192.168.162.223 -L <X>:localhost:8081 -L <Y>:localhost:8080

*X i Y to dowolne wolne porty na serwerze pośredniczącym np 42000 i 42001*

#### Gotowe !
Od tego momentu są dostępne następujące usługi:
- Frontend - http://localhost:80
- Jenkins - http://localhost:8080
- Nexus - http://localhost:8081

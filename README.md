# User Management API

Prosta aplikacja REST API do zarzadzania uzytkownikami, zbudowana w oparciu o Spring Boot. Projekt realizuje podstawowe operacje CRUD, waliduje dane wejsciowe i korzysta z bazy H2 uruchamianej w pamieci.

## Tech Stack

- Java 17
- Spring Boot
- Spring Web MVC
- Spring Data JPA
- Hibernate
- H2 Database
- Maven
- Lombok

## Features

- tworzenie uzytkownika
- pobieranie listy uzytkownikow
- pobieranie uzytkownika po `id`
- aktualizacja danych uzytkownika
- usuwanie uzytkownika
- walidacja danych wejsciowych
- mapowanie encji do DTO

## Project Structure

```text
src/main/java/com/example/usermanagement
|- controller
|- dto
|- entity
|- exception
|- repository
\- service
```

## Getting Started

### Requirements

- Java 17+
- Maven 3.9+ lub Maven Wrapper

### Run locally

```bash
./mvnw spring-boot:run
```

W systemie Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

Aplikacja domyslnie uruchamia sie pod adresem:

```text
http://localhost:8080
```

### Run tests

```bash
./mvnw test
```

W systemie Windows:

```powershell
.\mvnw.cmd test
```

## Database

Projekt korzysta z bazy H2 in-memory skonfigurowanej w `src/main/resources/application.properties`.

Najwazniejsze ustawienia:

- URL: `jdbc:h2:mem:testdb`
- username: `sa`
- password: puste
- Hibernate DDL: `update`
- H2 Console: wlaczona

Konsola H2:

```text
http://localhost:8080/h2-console
```

## API Endpoints

Base URL:

```text
/api/users
```

| Method | Endpoint | Description |
| --- | --- | --- |
| `POST` | `/api/users` | Create user |
| `GET` | `/api/users` | Get all users |
| `GET` | `/api/users/{id}` | Get user by id |
| `PUT` | `/api/users/{id}` | Update user |
| `DELETE` | `/api/users/{id}` | Delete user |

## Example Request

### Create user

```http
POST /api/users
Content-Type: application/json
```

```json
{
  "firstName": "Jan",
  "lastName": "Kowalski",
  "email": "jan.kowalski@example.com"
}
```

### Example response

```json
{
  "id": 1,
  "firstName": "Jan",
  "lastName": "Kowalski",
  "email": "jan.kowalski@example.com",
  "createdAt": "2026-04-24T21:30:00"
}
```

## Validation

Pola wejsciowe sa walidowane wedlug ponizszych zasad:

- `firstName` nie moze byc puste
- `lastName` nie moze byc puste
- `email` nie moze byc puste
- `email` musi miec poprawny format

## cURL Examples

### Create user

```bash
curl -X POST http://localhost:8080/api/users \
  -H "Content-Type: application/json" \
  -d "{\"firstName\":\"Jan\",\"lastName\":\"Kowalski\",\"email\":\"jan.kowalski@example.com\"}"
```

### Get all users

```bash
curl http://localhost:8080/api/users
```

### Get user by id

```bash
curl http://localhost:8080/api/users/1
```

### Update user

```bash
curl -X PUT http://localhost:8080/api/users/1 \
  -H "Content-Type: application/json" \
  -d "{\"firstName\":\"Anna\",\"lastName\":\"Nowak\",\"email\":\"anna.nowak@example.com\"}"
```

### Delete user

```bash
curl -X DELETE http://localhost:8080/api/users/1
```


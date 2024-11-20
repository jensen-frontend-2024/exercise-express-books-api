# Book API

### Uppgiftsbeskrivning: Skapa ett RESTful API för ett Bibliotekssystem

#### Bakgrund

Du har blivit anlitad av ett lokalt bibliotek för att digitalisera deras system för hantering av böcker. Biblioteket vill ha en enkel men kraftfull lösning för att hantera sina böcker. De behöver ett RESTful API som tillåter dem att skapa, läsa, uppdatera och radera böcker från deras databas. Syftet är att förbättra bokhanteringen och ge en smidigare hantering för bibliotekspersonalen.

Ditt uppdrag är att skapa ett RESTful API med hjälp av Node.js och Express.js som kan hantera böcker i biblioteket.

Uppiften kommer i två delar.

  - Del 1: All data sparas i en array med bok-objekt. Endpointsen utför CRUD-operationer på arrayen.
  
  - Del 2: All data ska sparas i en SQLite-databas. Endpointsen utför CRUD-operationer mot databasen.

#### Uppgiftens mål

- Skapa ett RESTful API som hanterar CRUD-operationer (Create, Read, Update, Delete) för böcker.
- Använda Node.js, Express.js _( och SQLite )_ för att bygga API:et.
- Testa dina endpoints med Postman.

#### Funktionskrav (Kravspecifikation)

1. **GET /books**  
   Endpoint för att hämta en lista över alla böcker.  
   **Response Exempel**:

   ```json
   [
     {
       "id": 1,
       "title": "To Kill a Mockingbird",
       "author": "Harper Lee",
       "yearPublished": 1960,
       "genre": "Fiction"
     },
     {
       "id": 2,
       "title": "1984",
       "author": "George Orwell",
       "yearPublished": 1949,
       "genre": "Dystopian"
     }
   ]
   ```

2. **GET /books/:id**  
   Endpoint för att hämta en specifik bok med ett visst ID.  
   **Response Exempel**:

   ```json
   {
     "id": 1,
     "title": "To Kill a Mockingbird",
     "author": "Harper Lee",
     "yearPublished": 1960,
     "genre": "Fiction"
   }
   ```

3. **POST /books**  
   Endpoint för att lägga till en ny bok.  
   **Request Body Exempel**:

   ```json
   {
     "title": "The Great Gatsby",
     "author": "F. Scott Fitzgerald",
     "yearPublished": 1925,
     "genre": "Classic"
   }
   ```

   **Response**:  
   Returnerar den skapade boken med ett genererat ID.  
   **Response Exempel**:

   ```json
   {
     "id": 3,
     "title": "The Great Gatsby",
     "author": "F. Scott Fitzgerald",
     "yearPublished": 1925,
     "genre": "Classic"
   }
   ```

4. **PUT /books/:id**  
   Endpoint för att uppdatera en befintlig bok med ett visst ID.  
   **Request Body Exempel**:

   ```json
   {
     "title": "The Great Gatsby",
     "author": "F. Scott Fitzgerald",
     "yearPublished": 1925,
     "genre": "Classic Fiction"
   }
   ```

   **Response**:  
   Returnerar den uppdaterade boken.  
   **Response Exempel**:

   ```json
   {
     "id": 3,
     "title": "The Great Gatsby",
     "author": "F. Scott Fitzgerald",
     "yearPublished": 1925,
     "genre": "Classic Fiction"
   }
   ```

5. **DELETE /books/:id**  
   Endpoint för att radera en bok med ett visst ID.  
   **Response**:  
   Returnerar en bekräftelse på att boken raderats.  
   **Response Exempel**:
   ```json
   {
     "message": "Book with ID 3 has been deleted."
   }
   ```

#### Krav på API:et

- Använd följande tekniker:

  - `express` för att skapa servern. _( del 1 & del 2)_
  - `better-sqlite3` för att skapa en databaskoppling till en SQLite-databas. _( del 2 )_

- All data om böcker ska lagras på något av följande sätt:

  - I minnet i en array av bok-objekt. _( del 1 )_
  - I en SQLite databas som innehåller tabell och kolumner för en bok. _( del 2 )_
  - Endpointsen måste anpassas utifrån vilken lagringssätt som används.

- Varje bok ska ha följande egenskaper:

  - `id` (nummer, genererat automatiskt)
  - `title` (sträng)
  - `author` (sträng)
  - `yearPublished` (nummer)
  - `genre` (sträng)

- Validera inkommande data för POST och PUT endpoints. Alla fält ska vara obligatoriska (förutom `id` som genereras automatiskt).

#### Utveckling och Testning

- Använd Postman för att testa ditt API.
- Säkerställ att alla endpoints fungerar enligt specifikationen.
- Logga relevanta meddelanden till konsolen för att underlätta felsökning.

#### Utmaningar _(frivilliga)_

- Implementera en enkel sökfunktion på endpointen `/books` som filtrerar böcker baserat på `title` eller `author`.

  - Exempel: `GET /books?title=Gatsby`

  Hint: Läs om query parameterar: [Exploring Query Parameters in RESTful APIs
  ](https://blog.replaybird.com/query-parameters-in-restful-apis/)

- **GET /books/:id/with-author**

  Bryt ut alla author-namn till en egen array med author-objekt istället. En `Book` kommer ni refererar till ett author-id istället för ett namn på sitt author-attribut.

  Implementera endpointen ovan för att hämta en bok med ett specifikt id samt att du kopplar på motsvarande author-objekt istället för author-id. En pasande response skulle kunna se ut så här:

  **Response**:  
   Returnerar ett objekt som representerar en bok inklusive ett objekt som beskriver vilken author boken har.  
  **Response Exempel**:

  ```json
  {
    "title": "The Great Gatsby",
    "author": {
      "id": 2,
      "name": "F. Scott Fitzgerald"
    },
    "yearPublished": 1925,
    "genre": "Classic Fiction"
  }
  ```

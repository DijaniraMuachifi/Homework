# Tutorial: Creating a Web API with ASP.NET Core
**Last Updated:** 08/23/2024  
**Authors:** Rick Anderson and Kirk Larkin

This repository is a step-by-step guide to creating a web API using ASP.NET Core with a supporting database, focusing on controller-based APIs. For those interested in minimal APIs, see the [Tutorial: Create a Minimal API with ASP.NET Core](link to the minimal API tutorial).

## Tutorial Structure

### Overview
This tutorial covers the creation of an API with the following routes:

- **GET /api/todoitems:** Returns all todo items
- **GET /api/todoitems/{id}:** Returns a specific item
- **POST /api/todoitems:** Adds a new item
- **PUT /api/todoitems/{id}:** Updates an existing item
- **DELETE /api/todoitems/{id}:** Deletes an item

A diagram describes the architecture of the app, demonstrating the flow between the client, controller, model, and data layer.

### Prerequisites
- Visual Studio or Visual Studio Code (with ASP.NET and web development support)
- Familiarity with ASP.NET Core and Entity Framework Core

### Detailed Project Steps

1. **Creating the Web Project:**
   - Start an ASP.NET Core Web API project in Visual Studio.

2. **Adding NuGet Packages:**
   - Use `Microsoft.EntityFrameworkCore.InMemory` to support an in-memory database, ideal for testing and initial development.

3. **Testing the Project:**
   - The project includes a WeatherForecast API for initial testing, accessible via Swagger.

### Code Structure

- **Model Class (TodoItem):** The `TodoItem` class represents the structure of a todo item.
- **Database Context (TodoContext):** Responsible for managing database access.
- **Program.cs Configuration:** Registers the database context and configures Swagger for automatic API documentation.

### Controller Implementation

- Scaffold the API controller to include CRUD operations using Entity Framework.
- **PostTodoItem Method:** Modified to return a Location header with the URI of the newly created item.

### Testing the API with Swagger
- Access **POST /api/TodoItems** to add items and **GET /api/TodoItems/{id}** to retrieve them.
- The tests include checks for HTTP response codes, such as 201 for successful creation.

### More Information
For an overview of ASP.NET Core with Swagger and OpenAPI, see the [ASP.NET Core Documentation](link to the documentation).

---

## 1. Prerequisites
- Have MongoDB 6.0.5 or higher installed.
- Install the MongoDB Shell and configure access from the command line.
- Development tools like Visual Studio or VS Code.

## 2. MongoDB Setup
- Configure MongoDB for local access.
- Create a `BookStore` database and a `Books` collection.
- Insert sample data into the collection for initial testing.

## 3. Creating the API Project with ASP.NET Core
- In Visual Studio, create a new project of type ASP.NET Core Web API and select the .NET 8.0 framework.
- Install the `MongoDB.Driver` package to connect to MongoDB.

## 4. Define the Entity Model
- Create a `Book` model in a new `Models` directory, with specific attributes for MongoDB, such as `BsonId` for the primary key and `BsonElement` to customize property names.

## 5. Add Database Settings
- Define database settings in `appsettings.json`, including the connection string and database and collection names.
- Create a `BookStoreDatabaseSettings` class to map settings and facilitate the use of Dependency Injection (DI) for accessing these configurations.

## 6. CRUD Operations Service
- Create a `BooksService` class in a `Services` directory to centralize database operations. This class implements methods for:
  - `GetAsync`: Returns all documents.
  - `GetAsync(id)`: Returns a specific document by ID.
  - `CreateAsync`: Inserts a new document.
  - `UpdateAsync`: Updates an existing document.
  - `RemoveAsync`: Removes a document by ID.
- Configure the `BooksService` in the DI container as a singleton.

## 7. API Controller (BooksController)
- Implement a `BooksController` in the `Controllers` directory.
- Create endpoints to handle HTTP GET, POST, PUT, and DELETE methods:
  - **GET /api/books:** Lists all books.
  - **GET /api/books/{id}:** Returns a specific book.
  - **POST /api/books:** Adds a new book.
  - **PUT /api/books/{id}:** Updates a book.
  - **DELETE /api/books/{id}:** Removes a book.

## 8. Testing the API
- Run the API and test the endpoints using a browser or tools like Swagger.

## 9. JSON Serialization Configuration
- Adjust JSON serialization in `Program.cs` so that property names in JSON follow Pascal Case format, and modify the property name `BookName` to `Name`, applying `[JsonPropertyName("Name")]` to the `BookName` property.

---

### Key Steps Covered

#### ASP.NET Core Project Setup
- Start the configuration in `Program.cs` to enable static file services and an in-memory database (using Entity Framework with `InMemoryDatabase`).
- Include `DefaultFiles` and `StaticFiles` to allow the use of an HTML page as the entry point for the application.

#### Directory Structure
- Create a `wwwroot` folder to store static files, where subfolders for `css` and `js` are created, along with the HTML file `index.html`.

#### HTML (index.html)
- Configure an HTML page for adding, editing, and listing tasks.
- Forms for adding new tasks and editing existing tasks.
- Display a dynamic table to list todo items with Edit and Delete buttons.

#### CSS (site.css)
- Basic styles to display the todo table and adjust the layout of forms and buttons.

#### JavaScript (site.js)
- Define CRUD functions using `fetch` to interact with the API:
  - `GetItems`: Sends a GET request to list all tasks.
  - `AddItem`: Sends a POST request to add a new task.
  - `UpdateItem`: Sends a PUT request to update an existing task.
  - `DeleteItem`: Sends a DELETE request to remove a task.

#### Explanation of CRUD Methods
- **Reading Tasks:** `fetch(uri)` retrieves the items and updates the HTML page by calling the `_displayItems` function.
- **Adding Tasks:** Creates a `item` object, converts it to JSON, and sends it to the endpoint with the POST method.
- **Updating Tasks:** Similar to adding, but with a specific endpoint for the item's ID and using the PUT method.
- **Deleting Tasks:** Configures the DELETE method to remove the item by its ID.


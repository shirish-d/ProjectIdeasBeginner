# Project Ideas

## 1. Lab Assignment: Implementing CRUD Operations for a Book Application using ASP.NET Core Web API

### Objective

The objective of this lab assignment is to create a RESTful Web API using ASP.NET Core that performs CRUD (Create, Read, Update, Delete) operations for a Book application. The assignment should be completed within 60 minutes.

### Requirements

#### 1. Create a new ASP.NET Core Web API project

- Use ASP.NET Core 6.0 or later.
- Name the project BookAPI.

#### 2. Define the Book model

Create a Book class with the following properties

``` C#
{
 Id (int)
 Title (string)
 Author (string)
 PublicationDate (DateTime)
 Genre (string)
 Rating (double)
}
```

#### 3. Set up the database context

- Use Entity Framework Core to set up the database context.
- Create a BookContext class that inherits from DbContext.
- Define a `DbSet<Book>` property in the BookContext class.

#### 4. Configure the database connection

- Use an in-memory database for simplicity.
- Configure the database connection in the appsettings.json file and the Startup class.

#### 5. Implement the CRUD operations

- Create a BooksController class that inherits from ControllerBase.

- Implement the following actions

  - GetBooks: Retrieve all books using LINQ queries.
  - GetBookById: Retrieve a book by its ID using LINQ queries.
  - CreateBook: Add a new book.
  - UpdateBook: Update an existing book.
  - DeleteBook: Delete a book by its ID.

#### 6.Implement LINQ queries

- Use LINQ queries to filter, sort, and retrieve data in the GetBooks and GetBookById actions.
- Example LINQ queries
  - Retrieve all books sorted by publication date.
  - Retrieve books with a rating higher than a specified value.
  - Retrieve books of a specific genre.

#### 7.Implement Microservices

- Split the application into multiple microservices, each responsible for a specific functionality.
- Create separate microservices for managing books, authors, and genres.
- Ensure that each microservice has its own database context and controller.
- Use HTTP communication between microservices to perform CRUD operations.

#### 8.Implement Authorization using JWT tokens

- Add authentication and authorization to the API using JWT tokens.
- Configure JWT authentication in the Startup class.
- Protect the CRUD endpoints by requiring a valid JWT token for access.
- Implement a login endpoint to generate JWT tokens for authenticated users.

#### 9.Test the API

- Use Postman or any other API testing tool to test the CRUD operations.
- Ensure that all operations (Create, Read, Update, Delete) work as expected.
- Test the authorization by accessing the endpoints with and without a valid JWT token.

## 2. Movie Reservation System - Advance
### Goal
The goal of this project is to help you understand how to implement complex business logic i.e. seat reservation and scheduling, thinking about the data model and relationships, and complex queries.

### Requirements

We have intentionally left out the implementation details to encourage you to think about the design and implementation of the system. However here are some requirements that you can consider:

### User Authentication and Authorization

Users should be able to sign up and log in.
You also need roles for users, such as admin and regular user. Admins should be able to manage movies and showtimes.
Regular users should be able to reserve seats for a showtime.
You can create the initial admin using seed data. Only admins should be able to promote other users to admin and be able to do things related to movie management, reporting, etc.

### Movie Management

Admins should be able to add, update, and delete movies.
Each movie should have a title, description, and poster image.
Movies should be categorized by genre.
Movies should have showtimes.

### Reservation Management

Users should be able to get the movies and their show times for a specific date.
Users should be able to reserve seats for a showtime, see the available seats, and select the seats they want.
Users should be able to see their reservations and cancel them (only upcoming ones).
Admins should be able to see all reservations, capacity, and revenue.

### Implementation Considerations

Think about the data model and relationships between entities.
Think about how you will avoid overbooking, and how you will handle seat reservations.
Think about how you will handle the scheduling of showtimes.
Think about how you will handle the reporting of reservations.
Think about how you will handle the authentication and authorization of users.

## 3. URL Shortening Service - Intermediate

You are required to create a simple RESTful API that allows users to shorten long URLs. The API should provide endpoints to create, retrieve, update, and delete short URLs. It should also provide statistics on the number of times a short URL has been accessed.
 ![image](https://github.com/user-attachments/assets/cbb4e144-50f9-4354-9a69-915fa0509d68)

### Requirements

You should create a RESTful API for a URL shortening service. The API should allow users to perform the following operations:

- Create a new short URL
- Retrieve an original URL from a short URL
- Update an existing short URL
- Delete an existing short URL
- Get statistics on the short URL (e.g., number of times accessed)

You can optionally setup a minimal frontend to interact with the API and setup redirects for the short URLs to the original URLs.

### API Endpoints

Given below are the details for each API operation.

### Create Short URL

Create a new short URL using the POST method

```
POST /shorten
{
  "url": "https://www.example.com/some/long/url"
}
```

The endpoint should validate the request body and return a 201 Created status code with the newly created short URL i.e.

```
{
  "id": "1",
  "url": "https://www.example.com/some/long/url",
  "shortCode": "abc123",
  "createdAt": "2021-09-01T12:00:00Z",
  "updatedAt": "2021-09-01T12:00:00Z"
}
```

or a 400 Bad Request status code with error messages in case of validation errors. Short codes must be unique and should be generated randomly.

### Retrieve Original URL

Retrieve the original URL from a short URL using the GET method
`GET /shorten/abc123`
The endpoint should return a 200 OK status code with the original URL i.e.

```
{
  "id": "1",
  "url": "https://www.example.com/some/long/url",
  "shortCode": "abc123",
  "createdAt": "2021-09-01T12:00:00Z",
  "updatedAt": "2021-09-01T12:00:00Z"
}
```

or a 404 Not Found status code if the short URL was not found. Your frontend should be responsible for retrieving the original URL using the short URL and redirecting the user to the original URL.

### Update Short URL

Update an existing short URL using the PUT method

```
PUT /shorten/abc123
{
  "url": "https://www.example.com/some/updated/url"
}
```

The endpoint should validate the request body and return a 200 OK status code with the updated short URL i.e.

```
{
  "id": "1",
  "url": "https://www.example.com/some/updated/url",
  "shortCode": "abc123",
  "createdAt": "2021-09-01T12:00:00Z",
  "updatedAt": "2021-09-01T12:30:00Z"
}
```

or a 400 Bad Request status code with error messages in case of validation errors. It should return a 404 Not Found status code if the short URL was not found.

### Delete Short URL

Delete an existing short URL using the DELETE method
`DELETE /shorten/abc123`
The endpoint should return a 204 No Content status code if the short URL was successfully deleted or a 404 Not Found status code if the short URL was not found.

### Get URL Statistics

Get statistics for a short URL using the GET method
`GET /shorten/abc123/stats`
The endpoint should return a 200 OK status code with the statistics i.e.

```
{
  "id": "1",
  "url": "https://www.example.com/some/long/url",
  "shortCode": "abc123",
  "createdAt": "2021-09-01T12:00:00Z",
  "updatedAt": "2021-09-01T12:00:00Z",
  "accessCount": 10
}
```

or a 404 Not Found status code if the short URL was not found.

### Tech Stack

Feel free to use any programming language, framework, and database of your choice for this project. Here are some suggestions:

- If you are using JavaScript, you can use Node.js with Express.js
- If you are using Python, you can use Flask or Django
- If you are using Java, you can use Spring Boot
- If you are using Ruby, you can use Ruby on Rails
- For databases, you can use:
  - If you are using SQL, you can use MySQL
  - If you are using NoSQL, you can use MongoDB
    
Your job is to implement the core functionality of the API, focusing on creating, retrieving, updating, and deleting short URLs, as well as tracking and retrieving access statistics.
You don’t have to implement authentication or authorization for this project.

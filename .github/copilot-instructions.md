Since you are aiming for a professional, high-performance CMS using **ASP.NET 10 (Minimal APIs)** and **Clean Architecture**, this `copilot-instructions.md` file will act as the "source of truth" for GitHub Copilot or Cursor. It ensures the AI generates code that matches your specific architectural standards and avoids "bloat."

Place this file in your project root (or `.github/` folder).

---

# copilot-instructions.md

## 🚀 Project Overview

* **Role:** Backend API for a Technical CMS (Articles, Projects, Certificates).
* **Stack:** .NET 10, ASP.NET Core Minimal APIs, Entity Framework Core 10.
* **Architecture:** Clean Architecture (Onion Architecture).
* **Primary Goal:** High-performance, SEO-friendly content delivery with a robust management layer.

---

## 🏗 Architectural Rules

Follow **Clean Architecture** principles strictly. The solution is divided into four layers:

1. **Domain:** Core entities, Value Objects, Domain Exceptions, and Repository Interfaces. No dependencies on other layers.
2. **Application:** MediatR Commands/Queries, DTOs, Mappings (AutoMapper/Mapperly), and FluentValidation.
3. **Infrastructure:** Data Access (EF Core DbContext), Migrations, External Services (Azure Blob Storage, Email), and Identity Implementation.
4. **Presentation (Web API):** Minimal API Endpoints, Middleware, and Dependency Injection composition.

---

## 🛠 Coding Standards & Patterns

### 1. Minimal APIs (Presentation)

* Use **Route Groups** to organize endpoints (e.g., `app.MapGroup("/api/articles")`).
* Inject `IMediator` into endpoints; do not put business logic in the endpoint handler.
* Use `TypedResults` (e.g., `Results.Ok()`, `Results.NotFound()`) for better OpenAPI/Swagger documentation.

### 2. Data Access (Infrastructure)

* Use **EF Core 10**.
* Prefer `AsNoTracking()` for read-only queries (Articles/Projects list).
* Implement the **Repository Pattern** only if complex abstraction is needed; otherwise, use MediatR handlers with DbContext directly for simplicity.

### 3. C# 14/15 Features (Latest)

* Use **Primary Constructors** for Dependency Injection.
* Use **File-scoped namespaces** to reduce nesting.
* Use **Required members** or **Records** for DTOs to ensure immutability.

### 4. Error Handling & Validation

* Use a **Global Exception Handler** (IExceptionHandler).
* Use **FluentValidation** for incoming request models. Return `ValidationProblem` on failure.

---

## 📝 Entity & Feature Specifics

### CMS Requirements

* **Categories:** Must be dynamic. Use a self-referencing table if sub-categories are needed.
* **Articles:** Must support Markdown strings and Tags.
* **Certificates:** Store metadata in DB and image files in Azure Blob Storage.

### Security

* Use **ASP.NET Core Identity** with JWT Bearer tokens.
* Implement **Role-based Access Control (RBAC)**: `Admin` (You) and `User` (Visitors).

---

## 🤖 Copilot Prompting Guidance

* "Create a new MediatR Command to create a Technical Article, including FluentValidation."
* "Generate a Minimal API endpoint group for Managing Projects with Authorization."
* "Write an EF Core configuration for the Article entity with a many-to-many relationship to Tags."

---

## 🚫 What to Avoid

* **Do Not** use Controller-based APIs (prefer Minimal APIs).
* **Do Not** put logic in the Domain Entities (keep them as POCOs/Rich Domain Models).
* **Do Not** return Entities directly to the client; always use **DTOs**.
* **Do Not** use `Lazy Loading`; use `Include()` for related data.

---

### Would you like me to generate the initial folder structure and a sample `Program.cs` based on these instructions?


# ASP.NET Core 10 Project Rules

- Use C# 14 language features where appropriate
- Follow SOLID principles in class and interface design
- Implement dependency injection for loose coupling
- Use primary constructors for dependency injection in services, use cases, etc.
- Use async/await for I/O-bound operations
- Prefer record types for immutable data structures
- Prefer controller endpoints over minimal APIs
  - Utilize minimal APIs for simple endpoints (when explicitly stated or when it makes sense)
- Implement proper exception handling and logging
- Use strongly-typed configuration with IOptions pattern
- Implement proper authentication and authorization
- Use Entity Framework Core for database operations
- Implement unit tests for business logic
- Use integration tests for API endpoints
- Implement proper versioning for APIs
- Implement proper caching strategies
- Use middleware for cross-cutting concerns
- Implement health checks for the application
- Use environment-specific configuration files
- Implement proper CORS policies
- Use secure communication with HTTPS
- Implement proper model validation
- Use Swagger/OpenAPI for API documentation
- Implement proper logging with structured logging
- Use background services for long-running tasks
- Favor explicit typing (this is very important). Only use var when evident.
- Make types internal and sealed by default unless otherwise specified
- Prefer Guid for identifiers unless otherwise specified
- Use `is null` checks instead of `== null`. The same goes for `is not null` and `!= null`.




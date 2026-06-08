# Task Management System

A full-stack task management web application developed as a capstone project at MacEwan University. Designed to help teams organize workflows, manage task allocation, and track project progress.

**Project Status:** Completed — December 2024

## Tech Stack

- **Frontend:** Angular 19, TypeScript, Angular Material, CDK Drag-and-Drop
- **Backend:** ASP.NET Core 8 Minimal API, C#
- **Database:** MongoDB (MongoDB.Driver 3.6)
- **Authentication:** JWT (JSON Web Tokens), BCrypt password hashing
- **Authorization:** Role-based access control (Administrator, General, ReadOnly)
- **Deployment:** GitHub Pages (frontend), Railway (backend), MongoDB Atlas (database)

## Key Features

- **Kanban Dashboard:** Drag-and-drop task board with status columns (New, Active, Resolved, Closed)
- **JWT Authentication:** Secure login with HMAC-SHA256 signed tokens and role-based policies
- **Role-Based Access Control:** Administrator, General, and ReadOnly permission tiers
- **Task Management:** Full CRUD for tasks (Quests) with categories, priorities, and statuses
- **Soft Deletes:** Records are flagged as deleted, never physically removed
- **HTTP Interceptor:** Automatically attaches Bearer token to every outgoing request
- **Route Guards:** Protected routes redirect unauthenticated users to login
- **MongoDB Seeding:** Auto-seeds default users, categories, priorities, and statuses on first run

## Project Structure

```
Task Management System/
├── capstone.web/          # Angular 19 frontend
│   └── src/app/
│       ├── core/security/ # AuthGuard + AuthInterceptor
│       ├── dashboard/     # Kanban board with CDK drag-and-drop
│       ├── login/         # JWT login
│       └── ...            # Feature components
└── capstone.web.api/      # ASP.NET Core 8 backend
    ├── Endpoints/         # Minimal API route handlers
    ├── Models/            # MongoDB document models
    └── Data/              # MongoDbContext
```

## Setup and Installation

### Prerequisites

- Node.js 22+
- Angular CLI (`npm install -g @angular/cli`)
- .NET 8 SDK
- MongoDB (local) or MongoDB Atlas connection string

### Run the Backend

```bash
cd capstone.web.api
dotnet run
```

The API will start at `http://localhost:8080`. Swagger UI available at `/swagger`.

### Run the Frontend

```bash
cd capstone.web
npm install
ng serve
```

App runs at `http://localhost:4200`.

### Default Credentials

| Username | Password | Role |
|---|---|---|
| `admin` | `admin-password` | Administrator |
| `general` | `general-password` | General |

## Architecture Notes

- **Minimal API:** All routes defined as lambdas in `Endpoints/` — no controllers
- **MongoDB Driver:** Direct driver usage, no ORM — `IMongoCollection<T>` queries throughout
- **Sequential IDs:** Custom string IDs (`que1`, `cat1`, `pri1`, `sta1`) generated from collection count
- **CORS:** Configurable via `AllowedOrigins` config key, overridable by environment variable
- **Railway Deployment:** Reads dynamic `PORT` env var; HTTPS redirect disabled (Railway terminates SSL at load balancer)

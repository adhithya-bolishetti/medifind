# MediFind Backend

MediFind is a monolithic healthcare platform built using Java 21 and Spring Boot 3.x.

## Architecture

This project is a standalone Spring Boot monolithic application. All previous microservices have been merged into a single `medifind-backend` backend.

## Folder Structure

```text
medifind/
├── medifind-backend/   # The monolithic Spring Boot application
├── frontend/           # React application built with Vite and Material UI
├── database/           # Database scripts and seed data
└── README.md
```

## Tech Stack

- **Java 21**
- **Spring Boot 3.2.4**
- **Spring Security & JWT**
- **MySQL & Spring Data JPA**
- **Maven**
- **Lombok & MapStruct**
- **Swagger / OpenAPI 3**
- **React 19 & Vite**
- **Material UI**

## Services & Ports Configuration

| Service            | Port | Description                                      |
|--------------------|------|--------------------------------------------------|
| Backend (Monolith) | 8080 | Main Spring Boot Backend                         |
| Frontend           | 5173 | React/Vite UI application                        |

## Database Configuration

The backend expects a MySQL database named `medifind_db`.
Credentials and configurations can be defined via environment variables:
- `DB_HOST` (default: `localhost`)
- `DB_PORT` (default: `3306`)
- `DB_NAME` (default: `medifind_db`)
- `DB_USERNAME` (default: `root`)
- `DB_PASSWORD` (default: `123456`)

```sql
CREATE DATABASE IF NOT EXISTS medifind_db;
```

## Admin Account

The application includes an Admin Dashboard (`/admin/dashboard`) for users with the `ADMIN` role.

| Field  | Value                    |
|--------|--------------------------|
| Email  | `9392392909@medifind.com` |
| Mobile | `9392392909` (login uses the `+91` country code prefix) |
| Password | `DemoAdmin@123` (DEMO CREDENTIAL) |

> **Note:** Admin accounts must be created in the database — the `ADMIN` role is never
> selectable during signup. To (re)create or reset the seeded admin account, run:
>
> ```bash
> mysql -u root -p < database/seed-admin.sql
> ```

## Test Accounts

| Role    | Mobile Number | Password     | Lands on              |
|---------|---------------|--------------|-----------------------|
| Admin   | `9392392909`  | `DemoAdmin@123` (DEMO) | Admin Dashboard      |
| Patient | `5555555555`  | `Test@12345` (DEMO) | Patient Dashboard     |
| Doctor  | `4444444444`  | `Test@12345` (DEMO) | Doctor Dashboard      |
| Hospital| `3333333333`  | `Test@12345` (DEMO) | Hospital Dashboard    |

These are seed accounts used for local testing. The patient, doctor, and hospital accounts have
completed profiles; new signups are redirected to profile creation first.

## API Endpoints

### API (Backend)
Base URL: `http://localhost:8080/api`

- `POST /auth/register`: Register a new user
- `POST /auth/login`: Authenticate and receive a JWT
- `GET /auth/me`: Get current logged-in user details (Requires `Authorization: Bearer <token>`)

### Swagger Documentation
Backend API Docs: `http://localhost:8080/swagger-ui.html`

## How to Run

1. **Ensure MySQL is running**
   Create the database `medifind_db`.

2. **Run Backend**
   Navigate to the backend directory and run:
   ```bash
   cd medifind-backend
   mvn spring-boot:run
   ```

3. **Run Frontend**
   ```bash
   cd frontend
   npm install
   npm run dev
   ```

Alternatively, you can run the `MediFindApplication.java` class directly from your IDE.

## Deployment

This application natively supports deployment to **Render**. A `render.yaml` file is provided for easy deployment using Render's Infrastructure as Code (IaC) features.

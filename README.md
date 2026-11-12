<div align="center">

# 💸 Trackify — Enterprise-Grade Personal Finance Tracker

[![React 18](https://img.shields.io/badge/React_18-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot_3.3+-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)](https://spring.io/projects/spring-boot)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)

A modern, highly performant, full-stack personal finance tracking application engineered for high security, seamless state management, and real-time financial insights. Designed to help users master their budgeting, track cash flow, and achieve financial freedom.

[View Demo](#-demo--screenshots) • [Report Bug](https://github.com/your-username/trackify/issues) • [Request Feature](https://github.com/your-username/trackify/issues)

</div>

---


## ✨ Key Features

- **🔐 Stateless JWT Authentication:** Secure registration and login cycle utilizing JSON Web Tokens with HTTP-ready Bearer authorization headers and password encryption via BCrypt.
- **📈 Real-Time Financial Dashboard:** Dynamic data visualization tracking net worth, monthly cash flow, category-wise breakdown of expenses, and rolling balance trends.
- **💰 Comprehensive Transaction Management:** Granular CRUD operations for income streams and expenses with tagging, dates, and category sorting.
- **🛡️ Global Exception Handling & Validation:** Enterprise-ready backend error handling using `@ControllerAdvice`, custom exceptions, and Jakarta Bean Validation.
- **⚡ High-Performance Frontend:** Built using Vite for blazing-fast HMR, Tailwind CSS for a modern aesthetic, and custom hooks/Context API for clean state management.
- **🐳 Containerized & Cloud-Ready:** Easily deployable via Docker and Docker Compose for zero-friction environment replication.

---

## 🛠️ Tech Stack & Architecture

### **Frontend**
- **Library:** React 18 (Concurrent features, Hooks)
- **Build Tool:** Vite
- **Styling:** Tailwind CSS, PostCSS
- **State Management:** React Context API (`UserContext`), Custom Hooks (`useUserAuth`)
- **HTTP Client:** Axios (with interceptors for automatic JWT injection and token expiration handling)
- **Routing:** React Router v6

### **Backend**
- **Framework:** Spring Boot 3.3+ (Java 17+)
- **Security:** Spring Security 6, JWT Filter chain, CORS configuration
- **Data Persistence:** Spring Data JPA / Hibernate, PostgreSQL JDBC Driver
- **Database Migration/Setup:** SQL initialization script
- **Build System:** Apache Maven

---

## 📂 Project Structure

```text
trackify/
├── backend/                        ← Spring Boot REST API
│   ├── src/main/java/com/trackify/
│   │   ├── config/                 Security config, CORS mappings, static asset filters
│   │   ├── controller/             REST API entry points (Auth, Income, Expense, Dashboard)
│   │   ├── dto/                    Request & Response Data Transfer Objects
│   │   ├── entity/                 JPA Entities (User, Income, Expense)
│   │   ├── exception/              Global exception handlers & custom errors
│   │   ├── repository/             Spring Data JPA Interfaces
│   │   ├── security/               JWT generation, validation filters, user details service
│   │   └── service/                Core business logic & transaction handling
│   ├── src/main/resources/
│   │   └── application.properties  App configuration & database profiles
│   ├── Dockerfile                  Multi-stage Docker build for backend
│   └── pom.xml                     Maven dependencies & plugins
│
├── frontend/                       ← React Single Page Application
│   ├── src/
│   │   ├── components/             Reusable UI primitives (Modals, Tables, Cards, Charts)
│   │   ├── context/                Global Context providers (UserContext)
│   │   ├── hooks/                  Custom application hooks (useUserAuth, useFetch)
│   │   ├── pages/
│   │   │   ├── Auth/               Login, Signup, Forgot Password
│   │   │   └── Dashboard/          Home Overview, Income Management, Expense Analytics
│   │   ├── utils/                  Axios client setup, formatting helpers, route guards
│   │   ├── App.jsx                 Root component & router setup
│   │   └── main.jsx                DOM entry point
│   ├── Dockerfile                  Frontend production server configuration
│   ├── package.json                Node dependencies & scripts
│   └── vite.config.js              Vite bundler configuration
│
├── docker-compose.yml              Orchestration for Database, Backend, and Frontend
└── database-init.sql               PostgreSQL baseline DDL and DML scripts

---

## 🐳 Quick Docker Start (low-resource)

```bash
cp .env.example .env        # set POSTGRES_PASSWORD and APP_JWT_SECRET (32+ chars)
docker compose up -d --build
```

Open http://localhost:3000. Stop with `docker compose down` (data is kept in volumes; `down -v` wipes it).

Memory caps: db 192 MB, backend 384 MB, frontend 32 MB (~600 MB total). Nginx serves the React build and proxies `/api` and `/uploads` to the backend, so no CORS or API URL setup is needed.

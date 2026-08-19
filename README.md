# 🚀 Team Task Manager

A production-ready, full-stack team collaboration platform designed to streamline task management, enforce role-based access control (RBAC), and deliver automated deadline tracking.

---

## 🌐 Live Demo

👉 [team-task-manager-clean-production.up.railway.app](https://team-task-manager-clean-production.up.railway.app)

---

## ✨ Overview

**Team Task Manager** is a scalable web application built to simulate real-world team workflows. It enables team leaders to manage projects and permissions while allowing team members to track tasks and update progress efficiently within a clean, responsive UI.

### Key Engineering Highlights
* 🔐 **Stateless Authentication**: JWT-based authentication using HTTP-only cookies and Bearer authorization headers (`jose` + `bcryptjs`).
* 👥 **Role-Based Access Control (RBAC)**:
  * **Admin**: Full authority over project creation, user management, and task administration.
  * **Member**: Scoped access to assigned tasks and projects.
* 📊 **Automated Overdue Detection**: Dynamic status calculation powered by Mongoose virtual fields.
* 🛡️ **Defensive Schema Validation**: Server-side request payload validation using Zod schemas.

---

## 🏗️ Architecture Summary

```text
┌─────────────────────────────────────────────────────────┐
│                    Client Browser                       │
│        (Next.js React Server & Client Components)       │
└────────────────────────────┬────────────────────────────┘
                             │ HTTP / REST API
                             ▼
┌─────────────────────────────────────────────────────────┐
│              Next.js 15 App Router Middleware           │
│        • Auth Validation (JWT Cookie / Bearer)          │
│        • Role Authorization (Admin vs. Member)          │
└────────────────────────────┬────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────┐
│             API Routes & Business Logic                 │
│         /api/auth | /api/projects | /api/tasks          │
└────────────────────────────┬────────────────────────────┘
                             │ Mongoose ODM
                             ▼
┌─────────────────────────────────────────────────────────┐
│              MongoDB Database (Railway)                 │
│               User | Project | Task Schemas             │
└─────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Frontend** | Next.js 15 (App Router), React 19, Tailwind CSS v4 |
| **Backend API** | Next.js Route Handlers, Zod Payload Validation |
| **Database** | MongoDB, Mongoose ODM |
| **Authentication** | `jose` (JWT) + `bcryptjs` (Password Hashing) |
| **Deployment** | Deployed on Railway PaaS |

---

## 🔗 API Documentation

All API routes require authentication via `token` HTTP-only cookie or `Authorization: Bearer <token>` header.

| Endpoint | Method | Role Required | Description |
| :--- | :--- | :--- | :--- |
| `/api/auth/signup` | `POST` | Public | Register user (first user automatically becomes Admin) |
| `/api/auth/login` | `POST` | Public | Authenticate user & issue JWT HTTP-only cookie |
| `/api/auth/logout` | `POST` | Authenticated | Clear authentication cookie |
| `/api/auth/me` | `GET` | Authenticated | Fetch current authenticated user payload |
| `/api/projects` | `GET`, `POST` | Auth / Admin | List projects or create new project (Admin) |
| `/api/projects/:id` | `GET`, `PUT`, `DELETE` | Authenticated | Retrieve, update, or remove project |
| `/api/projects/:id/members` | `GET` | Authenticated | Fetch project team members |
| `/api/tasks` | `GET`, `POST` | Authenticated | List tasks or create task |
| `/api/tasks/:id` | `GET`, `PUT`, `DELETE` | Authenticated | Retrieve, update status, or delete task |
| `/api/users` | `GET`, `PUT` | Admin | Retrieve users or update user roles |

---

## 🚀 Setup & Installation

### Prerequisites
* Node.js 18.x or higher
* MongoDB instance (local or MongoDB Atlas)

### Local Setup

1. **Clone the repository**:
   ```bash
   git clone https://github.com/prashant2930/team-task-manager-clean.git
   cd team-task-manager-clean
   ```

2. **Install dependencies**:
   ```bash
   npm install
   ```

3. **Configure environment variables**:
   Copy `.env.example` to `.env.local`:
   ```bash
   cp .env.example .env.local
   ```
   Configure `MONGODB_URI` and `JWT_SECRET` in `.env.local`.

4. **Start development server**:
   ```bash
   npm run dev
   ```
   Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 🌍 Environment Variables

| Variable | Description |
| :--- | :--- |
| `MONGODB_URI` | Connection string for MongoDB database |
| `JWT_SECRET` | Secret key for signing JWT tokens |

---

## 👨‍💻 Author

**Prashant Srivastava** — Software Engineer

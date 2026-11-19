# Project Brief: Doctor Tracker

# 1. Summary & Purpose
**Doctor Tracker** is an administrative web app for clinic coordinators to manage medical staff (doctors) and their patient cohorts cleanly and quickly.

The application runs on a decoupled architecture with a Next.js web client, a standalone Node.js and Express REST API, and a MongoDB database with Mongoose ODM. It focuses on fast search, multi-field filtering, clean pagination, and simple charts for daily admissions and specialty distribution.

---

# 2. Target User Personas

| User Role | Primary Responsibilities | Daily Needs in the App |
| :--- | :--- | :--- |
| **Clinic Administrator** | Oversees facility capacity, doctor schedules, and department loads. | Monitors hospital metrics, tracks doctor rosters, and assigns incoming patients to specialists without UI friction. |
| **Medical Records Staff** | Handles day-to-day patient record intake, updates, and assignments. | Rapid search by patient name or condition, updating contact details, and linking patients to attending doctors. |

---

# 3. Core Problems & Solutions

| Existing Problem | Doctor Tracker Solution | Implementation Approach |
| :--- | :--- | :--- |
| **Slow, Cluttered Search** | Sub-50ms instant search across doctors and patients. | MongoDB compound and text search indexes with client-side 300ms debouncing. |
| **Orphaned & Unlinked Records** | Clear relationships between doctors and patient cohorts. | Mongoose Schema references (`ref: 'Doctor'`) with atomic `$inc` counter maintenance. |
| **Hidden or Laggy Metrics** | Instant visual insights on clinic activity and workload. | Single-pass MongoDB `$facet` aggregation pipelines powering interactive charts. |
| **Data Vulnerabilities** | Strict server-side security and input validation. | JWT stored in HttpOnly cookies, Zod schema validation, NoSQL sanitization, and rate limiting. |

---

# 4. Technology Scope

| Tier | Chosen Stack | Key Responsibilities |
| :--- | :--- | :--- |
| **Frontend Client** | Next.js 15, React 19, Tailwind CSS | Responsive dashboard, debounced search inputs, data tables, modal dialogs, and analytics charts. |
| **Backend Server** | Node.js, Express, TypeScript | REST API endpoints, JWT auth cookies, rate limiting, and business validation. |
| **Database** | MongoDB (6.0+), Mongoose ODM | Document collections (`users`, `doctors`, `patients`), compound indexes, and aggregation pipelines. |

---

# 5. Project Constraints & Boundaries

| Constraint | Scope Boundary |
| :--- | :--- |
| **Authentication Boundary** | Designed for clinic coordinators and administrative staff. Patient self-service portals are out of scope. |
| **Communication Boundary** | Client communicates with backend strictly via RESTful JSON over HTTPS. Direct database access from client is prohibited. |
| **Deployment Boundary** | Frontend client is structured for deployment to Vercel/Netlify; backend API is configured for standalone deployment to Render. |

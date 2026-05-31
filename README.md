# MCA Result Portal

A full-stack **Academic Result Management System** built for MCA departments. The portal centralizes student results, subject records, notices, analytics, users, and administrative workflows in one clean web application.

## Overview

The MCA Result Portal helps an academic department manage results and academic communication more efficiently. It supports secure login, role-based dashboards, student result cards, internal and external marks calculation, analytics, bulk marks upload, notice board management, user management, subject management, and PostgreSQL-ready deployment.

## Key Features

- Secure login with email/name and password
- Role-based dashboards for admin, teacher, faculty, and student
- Student result card with subject-wise marks, grade, percentage, and pass/fail status
- Correct marks calculation using:

```text
Internal Marks + External Marks = Total Marks Obtained
Percentage = Total Marks Obtained / Maximum Marks * 100
```

- Performance analytics with ranking and grade distribution
- Bulk marks upload using CSV / Excel-ready template
- Subject add, edit, and delete management
- User add, edit, activate/deactivate, and delete management
- Duplicate result entry delete option
- Notice board for events, R&D news, publication status, circulars, placements, projects, and timetable updates
- Forgot password request workflow handled by admin
- SQLite support for local development
- PostgreSQL support for production deployment using `DATABASE_URL`
- Modern responsive UI with animated 3D-style login page

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python Flask |
| ORM | SQLAlchemy |
| Authentication | Flask-Login |
| Database | SQLite / PostgreSQL |
| Frontend | HTML, CSS, Bootstrap, JavaScript |
| Icons | Font Awesome |
| Charts | Chart.js |

## Comprehensive Architecture Design

The application follows a layered web architecture where the browser interface communicates with Flask routes, Flask applies authentication and business rules, SQLAlchemy handles data access, and the database stores academic records.

### Architecture Color Palette

| Color | Represents |
|---|---|
| Blue | Frontend / browser interface |
| Indigo | Flask routes and backend control |
| Purple | Authentication and authorization |
| Orange | Business logic and validation |
| Green | Database and persistence |
| Cyan | Deployment and static assets |

### High-Level Architecture

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#eef4ff', 'primaryTextColor': '#182033', 'lineColor': '#3558d7', 'fontFamily': 'Arial' }}}%%
flowchart LR
    U[Users\nAdmin / Teacher / Faculty / Student] --> B[Browser UI\nHTML + CSS + Bootstrap + JS]
    B --> R[Flask Routes\napp.py]
    R --> A[Authentication Layer\nFlask-Login]
    R --> L[Business Logic Layer\nMarks, Grades, Notices, Users]
    L --> O[SQLAlchemy ORM]
    O --> D[(SQLite / PostgreSQL Database)]

    classDef user fill:#fef3c7,stroke:#f59e0b,color:#111827,stroke-width:2px
    classDef frontend fill:#dbeafe,stroke:#2563eb,color:#0f172a,stroke-width:2px
    classDef backend fill:#e0e7ff,stroke:#4f46e5,color:#111827,stroke-width:2px
    classDef auth fill:#f3e8ff,stroke:#7c3aed,color:#111827,stroke-width:2px
    classDef logic fill:#ffedd5,stroke:#f97316,color:#111827,stroke-width:2px
    classDef orm fill:#cffafe,stroke:#0891b2,color:#111827,stroke-width:2px
    classDef db fill:#dcfce7,stroke:#16a34a,color:#111827,stroke-width:2px

    class U user
    class B frontend
    class R backend
    class A auth
    class L logic
    class O orm
    class D db
```

### Layered Design

| Layer | Responsibility |
|---|---|
| Presentation Layer | Jinja templates, responsive dashboard UI, forms, charts, result card, notice board |
| Route Layer | Flask routes such as `/dashboard`, `/result/<id>`, `/upload_marks`, `/analytics`, `/users`, `/subjects` |
| Authentication Layer | Login, logout, session handling, current user detection |
| Authorization Layer | Role-based route access for admin, teacher, faculty, and student |
| Business Logic Layer | Marks validation, grade calculation, analytics, bulk upload processing, password reset workflow |
| Data Access Layer | SQLAlchemy models and relationships |
| Database Layer | SQLite for local development and PostgreSQL for production |

### Request Flow

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'actorBkg': '#dbeafe', 'actorBorder': '#2563eb', 'actorTextColor': '#111827', 'signalColor': '#3558d7', 'signalTextColor': '#182033', 'activationBkgColor': '#eef4ff', 'activationBorderColor': '#7c3aed', 'fontFamily': 'Arial' }}}%%
sequenceDiagram
    participant User
    participant Browser
    participant Flask
    participant Auth as Flask-Login
    participant DB as SQLAlchemy/Database

    User->>Browser: Open portal and submit request
    Browser->>Flask: HTTP request
    Flask->>Auth: Check login/session/role
    Auth-->>Flask: Access allowed or denied
    Flask->>DB: Query or update data
    DB-->>Flask: Return records
    Flask->>Browser: Render Jinja template
    Browser-->>User: Display dashboard/result/page
```

### Role-Based Access Architecture

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#eef4ff', 'primaryTextColor': '#182033', 'lineColor': '#3558d7', 'fontFamily': 'Arial' }}}%%
flowchart TD
    Login[Login] --> Role{User Role}
    Role --> Admin[Admin Dashboard]
    Role --> Teacher[Teacher Dashboard]
    Role --> Faculty[Faculty Dashboard]
    Role --> Student[Student Dashboard]

    Admin --> Users[User Management]
    Admin --> Subjects[Subject Management]
    Admin --> Results[Result Management]
    Admin --> Notices[Notice Board]
    Admin --> Passwords[Password Requests]
    Admin --> Analytics[Analytics]

    Teacher --> Upload[Upload Marks]
    Teacher --> Analytics
    Teacher --> Results

    Faculty --> Notices
    Faculty --> Analytics

    Student --> MyResult[My Result Card]
    Student --> Profile[Profile]
    Student --> StudentNotices[View Notices]

    classDef entry fill:#dbeafe,stroke:#2563eb,color:#111827,stroke-width:2px
    classDef decision fill:#fef3c7,stroke:#f59e0b,color:#111827,stroke-width:2px
    classDef admin fill:#fee2e2,stroke:#dc2626,color:#111827,stroke-width:2px
    classDef teacher fill:#e0e7ff,stroke:#4f46e5,color:#111827,stroke-width:2px
    classDef faculty fill:#dcfce7,stroke:#16a34a,color:#111827,stroke-width:2px
    classDef student fill:#f3e8ff,stroke:#7c3aed,color:#111827,stroke-width:2px
    classDef module fill:#f8fafc,stroke:#94a3b8,color:#111827,stroke-width:1.5px

    class Login entry
    class Role decision
    class Admin,Users,Subjects,Results,Passwords admin
    class Teacher,Upload teacher
    class Faculty,Notices faculty
    class Student,MyResult,Profile,StudentNotices student
    class Analytics module
```

### Database Architecture

Main SQLAlchemy models:

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#eef4ff', 'primaryTextColor': '#182033', 'lineColor': '#3558d7', 'entityBkg': '#dbeafe', 'entityBorder': '#2563eb', 'fontFamily': 'Arial' }}}%%
erDiagram
    USER ||--o{ RESULT : has
    SUBJECT ||--o{ RESULT : contains
    USER ||--o{ NOTICE : creates
    USER ||--o{ PASSWORD_RESET_REQUEST : requests

    USER {
        int id PK
        string name
        string email
        string password
        string role
        boolean active
        string roll_no
        int semester
        string branch
    }

    SUBJECT {
        int id PK
        string name
        string code
        int semester
        int max_marks
        int credits
    }

    RESULT {
        int id PK
        int student_id FK
        int subject_id FK
        float marks
        float internal
        string exam_year
        int uploaded_by FK
    }

    NOTICE {
        int id PK
        string title
        text body
        string category
        string visibility
        string audience
        string priority
        string status
        boolean pinned
    }

    PASSWORD_RESET_REQUEST {
        int id PK
        int user_id FK
        string email
        text message
        string status
        datetime requested_at
        datetime resolved_at
    }
```

### Result Calculation Architecture

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#eef4ff', 'primaryTextColor': '#182033', 'lineColor': '#3558d7', 'fontFamily': 'Arial' }}}%%
flowchart LR
    I[Internal Marks] --> T[Total Obtained Marks]
    E[External Marks] --> T
    T --> P[Percentage Calculation]
    M[Subject Max Marks] --> P
    P --> G[Grade Assignment]
    G --> R[Result Card + Analytics]

    classDef input fill:#dbeafe,stroke:#2563eb,color:#111827,stroke-width:2px
    classDef total fill:#ffedd5,stroke:#f97316,color:#111827,stroke-width:2px
    classDef calc fill:#fef3c7,stroke:#f59e0b,color:#111827,stroke-width:2px
    classDef grade fill:#f3e8ff,stroke:#7c3aed,color:#111827,stroke-width:2px
    classDef output fill:#dcfce7,stroke:#16a34a,color:#111827,stroke-width:2px

    class I,E,M input
    class T total
    class P calc
    class G grade
    class R output
```

Calculation logic:

```text
Total Obtained = Internal Marks + External Marks
Subject Percentage = Total Obtained / Subject Max Marks * 100
Overall Percentage = Sum of Total Obtained / Sum of Max Marks * 100
```

### Deployment Architecture

For production, the local SQLite database should be replaced with PostgreSQL and the Flask app should be hosted on a public server.

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#eef4ff', 'primaryTextColor': '#182033', 'lineColor': '#3558d7', 'fontFamily': 'Arial' }}}%%
flowchart LR
    User[Student / Admin / Faculty] --> Domain[Public Domain / HTTPS]
    Domain --> Web[Flask App Server\nGunicorn / Hosting Platform]
    Web --> PG[(PostgreSQL Database)]
    Web --> Static[Static Assets\nCSS / JS / Images]

    classDef user fill:#fef3c7,stroke:#f59e0b,color:#111827,stroke-width:2px
    classDef domain fill:#dbeafe,stroke:#2563eb,color:#111827,stroke-width:2px
    classDef server fill:#e0e7ff,stroke:#4f46e5,color:#111827,stroke-width:2px
    classDef db fill:#dcfce7,stroke:#16a34a,color:#111827,stroke-width:2px
    classDef static fill:#cffafe,stroke:#0891b2,color:#111827,stroke-width:2px

    class User user
    class Domain domain
    class Web server
    class PG db
    class Static static
```

Recommended deployment platforms:

- Render
- Railway
- PythonAnywhere
- VPS server
- College server
- PostgreSQL providers such as Neon, Supabase, Railway, or Render PostgreSQL

### SQLite To PostgreSQL Migration Architecture

```mermaid
%%{init: {'theme': 'base', 'themeVariables': { 'primaryColor': '#eef4ff', 'primaryTextColor': '#182033', 'lineColor': '#3558d7', 'fontFamily': 'Arial' }}}%%
flowchart LR
    S[(Existing SQLite\ninstance/mca_portal.db)] --> M[migrate_sqlite_to_postgres.py]
    M --> P[(PostgreSQL Database)]
    P --> F[Flask App using DATABASE_URL]

    classDef sqlite fill:#fef3c7,stroke:#f59e0b,color:#111827,stroke-width:2px
    classDef script fill:#dbeafe,stroke:#2563eb,color:#111827,stroke-width:2px
    classDef postgres fill:#dcfce7,stroke:#16a34a,color:#111827,stroke-width:2px
    classDef app fill:#e0e7ff,stroke:#4f46e5,color:#111827,stroke-width:2px

    class S sqlite
    class M script
    class P postgres
    class F app
```

The app uses:

```text
DATABASE_URL=postgresql://username:password@host:port/database_name
```

If `DATABASE_URL` is not set, the app falls back to SQLite for local development.

## Project Structure

```text
MCA_RESULT_MANAGEMENT_SYSTEM/
|-- app.py
|-- requirements.txt
|-- migrate_sqlite_to_postgres.py
|-- POSTGRESQL_SETUP.md
|-- start_ngrok.bat
|-- templates/
|-- static/
|-- instance/
|-- uploads_tmp/
`-- presentation_assets/
```

## Installation

1. Clone the repository:

```bash
git clone <your-repository-url>
cd MCA_RESULT_MANAGEMENT_SYSTEM
```

2. Create and activate a virtual environment:

```bash
python -m venv venv
venv\Scripts\activate
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Run the application:

```bash
python app.py
```

5. Open in browser:

```text
http://127.0.0.1:5000
```

## Default Local Admin

For local development, the app creates a default admin account:

```text
Email: aniketnihal05@gmail.com
Password: 123456
```

Change this before production deployment.

## PostgreSQL Setup

The app supports PostgreSQL using the `DATABASE_URL` environment variable.

Example:

```powershell
$env:DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/mca_portal"
python app.py
```

To migrate existing SQLite data into PostgreSQL:

```powershell
$env:DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/mca_portal"
python migrate_sqlite_to_postgres.py
```

More details are available in:

```text
POSTGRESQL_SETUP.md
```

## Main Modules

### Admin

- Manage users
- Manage subjects
- View analytics
- Upload marks
- Publish notices
- Resolve forgot password requests
- Delete duplicate result entries

### Teacher

- Upload marks
- View student results
- View analytics
- Manage result entries

### Faculty

- View students
- View analytics
- Publish academic notices

### Student

- View dashboard
- View personal result card
- View notices
- Manage profile

## Screenshots

Screenshots used for the project presentation are available in:

```text
presentation_assets/
```

## Presentation

A detailed PowerPoint presentation is included:

```text
MCA_Result_Portal_Presentation.pptx
```

It explains the project overview, problem statement, objectives, modules, database design, PostgreSQL migration, security, deployment, and future scope.

## Future Enhancements

- Add PWA support for installable mobile/desktop app experience
- Add PDF result card export
- Add email/SMS notifications
- Add audit logs for admin actions
- Add CGPA and semester-wise reports
- Add hosted PostgreSQL backups

## Author

**Aniket Nihal**

## License

This project is created for academic learning and MCA department-level result management.

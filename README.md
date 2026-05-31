# MCA-Result-Portal
Built an MCA Result Portal - Academic Management System using Python Flask, SQLAlchemy, PostgreSQL/SQLite, HTML, CSS, Bootstrap, and JavaScript
<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=32&duration=2800&pause=2000&color=6366F1&center=true&vCenter=true&width=600&lines=🎓+MCA+Result+Portal;Academic+Result+Management" alt="Typing SVG" />

<br/>

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)
![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chartdotjs&logoColor=white)

<br/>

> 🏫 A full-stack **Academic Result Management System** built for MCA departments — centralizing student results, analytics, notices, and administrative workflows in one clean web application.

<br/>

[![License: Academic](https://img.shields.io/badge/License-Academic-blueviolet?style=flat-square)](LICENSE)
[![Status: Active](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)]()
[![Made with ❤️](https://img.shields.io/badge/Made%20with-❤️-red?style=flat-square)]()

</div>

---

## 📌 Table of Contents

- [✨ Overview](#-overview)
- [🚀 Key Features](#-key-features)
- [🛠 Tech Stack](#-tech-stack)
- [📁 Project Structure](#-project-structure)
- [⚙️ Installation](#️-installation)
- [🗄️ PostgreSQL Setup](#️-postgresql-setup)
- [🧩 Modules](#-modules)
- [📐 Marks Calculation](#-marks-calculation)
- [🔮 Future Enhancements](#-future-enhancements)
- [👨‍💻 Author](#-author)

---

## ✨ Overview

The **MCA Result Portal** helps academic departments manage results and communication efficiently. It supports secure login, role-based access, result cards, bulk uploads, analytics, and a full notice board — all in a modern, responsive interface.

---

## 🚀 Key Features

<table>
<tr>
<td>

### 🔐 Authentication & Roles
- Secure login with email/name + password
- Role-based dashboards for **Admin**, **Teacher**, **Faculty**, **Student**
- Forgot password workflow handled by admin

</td>
<td>

### 📊 Results & Analytics
- Subject-wise marks, grade, percentage & pass/fail
- Performance analytics with ranking & grade distribution
- Bulk marks upload via CSV / Excel template

</td>
</tr>
<tr>
<td>

### 🗂️ Management
- Subject add, edit & delete
- User add, edit, activate/deactivate & delete
- Duplicate result entry cleanup

</td>
<td>

### 📢 Notice Board
- Events, R&D news, publication status
- Circulars, placements, projects & timetable updates

</td>
</tr>
</table>

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|------------|
| ⚙️ Backend | Python Flask |
| 🗃️ ORM | SQLAlchemy |
| 🔑 Authentication | Flask-Login |
| 🗄️ Database | SQLite (dev) / PostgreSQL (prod) |
| 🎨 Frontend | HTML, CSS, Bootstrap, JavaScript |
| 🎯 Icons | Font Awesome |
| 📈 Charts | Chart.js |

---

## 📁 Project Structure

```
MCA_RESULT_MANAGEMENT_SYSTEM/
├── 📄 app.py
├── 📄 requirements.txt
├── 📄 migrate_sqlite_to_postgres.py
├── 📄 POSTGRESQL_SETUP.md
├── 📄 start_ngrok.bat
├── 📂 templates/
├── 📂 static/
├── 📂 instance/
├── 📂 uploads_tmp/
└── 📂 presentation_assets/
```

---

## ⚙️ Installation

```bash
# 1️⃣ Clone the repository
git clone <your-repository-url>
cd MCA_RESULT_MANAGEMENT_SYSTEM

# 2️⃣ Create & activate virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # Linux/macOS

# 3️⃣ Install dependencies
pip install -r requirements.txt

# 4️⃣ Run the app
python app.py
```

🌐 Open in browser: `http://127.0.0.1:5000`

> **🔑 Default Admin (Local Dev)**
>
> | Field | Value |
> |-------|-------|
> | Email | `aniketnihal05@gmail.com` |
> | Password | `123456` |
>
> ⚠️ **Change credentials before production deployment!**

---

## 🗄️ PostgreSQL Setup

```powershell
# Set the DATABASE_URL environment variable
$env:DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/mca_portal"

# Run the application
python app.py

# Migrate existing SQLite data to PostgreSQL
python migrate_sqlite_to_postgres.py
```

📄 Detailed guide available in `POSTGRESQL_SETUP.md`

---

## 📐 Marks Calculation

```
╔══════════════════════════════════════════════════════════╗
║                                                          ║
║   Total Marks  =  Internal Marks + External Marks        ║
║                                                          ║
║   Percentage   =  Total Marks Obtained                   ║
║                   ─────────────────────  × 100           ║
║                      Maximum Marks                       ║
║                                                          ║
╚══════════════════════════════════════════════════════════╝
```

---

## 🧩 Modules

<details>
<summary>🔴 <strong>Admin</strong> — Click to expand</summary>

- Manage all users (add, edit, activate/deactivate, delete)
- Manage subjects
- View performance analytics
- Upload bulk marks
- Publish notices
- Resolve forgot password requests
- Delete duplicate result entries

</details>

<details>
<summary>🟠 <strong>Teacher</strong> — Click to expand</summary>

- Upload marks
- View student results
- View analytics
- Manage result entries

</details>

<details>
<summary>🟡 <strong>Faculty</strong> — Click to expand</summary>

- View students
- View analytics
- Publish academic notices

</details>

<details>
<summary>🟢 <strong>Student</strong> — Click to expand</summary>

- View personal dashboard
- View personal result card
- View notices
- Manage profile

</details>

---

## 🔮 Future Enhancements

| # | Enhancement |
|---|-------------|
| 📱 | PWA support for installable mobile/desktop app |
| 📄 | PDF result card export |
| 📧 | Email/SMS notifications |
| 🔍 | Audit logs for admin actions |
| 📊 | CGPA and semester-wise reports |
| 💾 | Hosted PostgreSQL automatic backups |

---

## 📊 Project Presentation

A detailed PowerPoint presentation (`MCA_Result_Portal_Presentation.pptx`) covers:

> Project Overview • Problem Statement • Objectives • Modules • Database Design • PostgreSQL Migration • Security • Deployment • Future Scope

Screenshots are available in `presentation_assets/`.

---

## 👨‍💻 Author

<div align="center">

**Aniket Nihal**

*This project is created for academic learning and MCA department-level result management.*

---

⭐ **If you found this project useful, please give it a star!** ⭐

</div>

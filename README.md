<div align="center">

# 🏥 Ask Your Doctor
### Online Doctor Appointment Booking System

[![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)](https://www.java.com)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=spring-boot&logoColor=white)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React.js-20232A?style=flat-square&logo=react&logoColor=61DAFB)](https://reactjs.org)
[![MySQL](https://img.shields.io/badge/MySQL-00000F?style=flat-square&logo=mysql&logoColor=white)](https://www.mysql.com)
[![REST API](https://img.shields.io/badge/REST_API-009688?style=flat-square)](https://restfulapi.net)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-563D7C?style=flat-square&logo=bootstrap&logoColor=white)](https://getbootstrap.com)

> A full-stack healthcare web application that enables patients to discover doctors, schedule appointments, and manage their complete consultation history through a seamless digital experience.

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Architecture](#-architecture)
- [Database Schema](#-database-schema)
- [Getting Started](#-getting-started)
- [API Reference](#-api-reference)
- [Screenshots](#-screenshots)
- [Future Enhancements](#-future-enhancements)
- [Author](#-author)

---

## 🔭 Overview

Ask Your Doctor is a full-stack healthcare appointment platform built as part of the PG-DAC curriculum at IACSD, Pune. The application addresses a real-world need: making it simple for patients to find the right doctor and book appointments without the friction of phone calls and paperwork.

The platform separates patient and administrative concerns cleanly — patients can search, book, and track their appointments, while the backend services handle scheduling logic, data validation, and persistence through a well-structured REST API layer.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🔍 **Doctor Discovery** | Search and filter doctors by specialization, name, or availability |
| 📅 **Appointment Booking** | Schedule new appointments with date and time selection |
| 📋 **Appointment History** | View all past and upcoming consultations in one place |
| 👨‍⚕️ **Doctor Profiles** | Detailed profiles with specialization, contact, and availability |
| 🏥 **Patient Management** | Manage patient information and medical interaction history |
| 📱 **Responsive Design** | Mobile-friendly UI built with Bootstrap for all screen sizes |
| 🔗 **REST API Architecture** | Clean API layer decoupling frontend and backend completely |

---

## 🛠️ Tech Stack

### Backend
| Technology | Version | Purpose |
|-----------|---------|---------|
| Java | 11+ | Core language |
| Spring Boot | 2.x | Application framework |
| Spring MVC | — | MVC architecture and routing |
| Spring Data JPA / JDBC | — | Database interaction layer |
| RESTful Web Services | — | API communication standard |
| J2EE / Jakarta EE | — | Enterprise application layer |
| Maven | 3.6+ | Build and dependency management |

### Frontend
| Technology | Purpose |
|-----------|---------|
| React.js | Component-based UI framework |
| JavaScript (ES6+) | Client-side interactivity |
| HTML5 | Semantic page structure |
| CSS3 | Custom styling |
| Bootstrap | Responsive grid and components |

### Database & DevTools
| Tool | Purpose |
|------|---------|
| MySQL 8.0+ | Relational database |
| Postman | API testing and documentation |
| Git / GitHub | Version control |
| Spring Tool Suite (STS) | Backend IDE |
| VS Code | Frontend IDE |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   PRESENTATION LAYER                    │
│                     React.js Frontend                   │
│         Components  →  State  →  API Calls              │
│              (localhost:3000)                           │
└───────────────────────────┬─────────────────────────────┘
                            │ HTTP / REST API (JSON)
┌───────────────────────────▼─────────────────────────────┐
│                  APPLICATION LAYER                      │
│                Spring Boot Backend                      │
│  REST Controllers → Service Layer → Repository Layer   │
│               (localhost:8080)                         │
└───────────────────────────┬─────────────────────────────┘
                            │ JDBC / Spring Data JPA
┌───────────────────────────▼─────────────────────────────┐
│                   DATA LAYER                            │
│                  MySQL Database                         │
│         patients | doctors | appointments               │
└─────────────────────────────────────────────────────────┘
```

---

## 🗄️ Database Schema

```sql
-- Core Tables

CREATE TABLE patients (
    id          INT PRIMARY KEY AUTO_INCREMENT,
    name        VARCHAR(100) NOT NULL,
    email       VARCHAR(100) UNIQUE NOT NULL,
    phone       VARCHAR(15),
    created_at  TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE doctors (
    id              INT PRIMARY KEY AUTO_INCREMENT,
    name            VARCHAR(100) NOT NULL,
    specialization  VARCHAR(100) NOT NULL,
    email           VARCHAR(100) UNIQUE NOT NULL,
    phone           VARCHAR(15),
    available       BOOLEAN DEFAULT TRUE
);

CREATE TABLE appointments (
    id              INT PRIMARY KEY AUTO_INCREMENT,
    patient_id      INT NOT NULL,
    doctor_id       INT NOT NULL,
    appointment_dt  DATETIME NOT NULL,
    status          ENUM('PENDING','CONFIRMED','CANCELLED','COMPLETED') DEFAULT 'PENDING',
    notes           TEXT,
    created_at      TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (patient_id) REFERENCES patients(id),
    FOREIGN KEY (doctor_id)  REFERENCES doctors(id)
);
```

---

## 🚀 Getting Started

### Prerequisites

Make sure you have installed:
- **Java** 11 or higher
- **Node.js** 16 or higher & npm
- **MySQL** 8.0 or higher
- **Maven** 3.6 or higher
- **Git**

### 1. Clone the Repository

```bash
git clone https://github.com/OMKARRAJMANE1/Ask-Your-Doctor.git
cd Ask-Your-Doctor
```

### 2. Database Setup

```sql
-- Create the database
CREATE DATABASE ask_your_doctor;
USE ask_your_doctor;

-- Tables will be created automatically via Spring Boot on first run
-- (if spring.jpa.hibernate.ddl-auto=update is configured)
```

### 3. Backend Configuration

Edit `src/main/resources/application.properties`:

```properties
# Database
spring.datasource.url=jdbc:mysql://localhost:3306/ask_your_doctor?useSSL=false&serverTimezone=UTC
spring.datasource.username=your_mysql_username
spring.datasource.password=your_mysql_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

# Server
server.port=8080
```

### 4. Run the Backend

```bash
# From the root project directory
./mvnw spring-boot:run

# OR using Maven directly
mvn spring-boot:run
```

✅ Backend running at `http://localhost:8080`

### 5. Run the Frontend

```bash
# Navigate to the frontend folder
cd frontend

# Install dependencies
npm install

# Start development server
npm start
```

✅ Frontend running at `http://localhost:3000`

---

## 📡 API Reference

### Doctor Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/doctors` | Get all doctors |
| `GET` | `/api/doctors/{id}` | Get doctor by ID |
| `GET` | `/api/doctors/specialization/{spec}` | Filter by specialization |
| `POST` | `/api/doctors` | Add a new doctor |
| `PUT` | `/api/doctors/{id}` | Update doctor info |
| `DELETE` | `/api/doctors/{id}` | Remove a doctor |

### Appointment Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/appointments` | Book an appointment |
| `GET` | `/api/appointments/patient/{id}` | Get patient's appointments |
| `GET` | `/api/appointments/doctor/{id}` | Get doctor's appointments |
| `PUT` | `/api/appointments/{id}` | Update appointment status |
| `DELETE` | `/api/appointments/{id}` | Cancel appointment |

### Patient Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/patients/register` | Register a new patient |
| `GET` | `/api/patients/{id}` | Get patient details |
| `PUT` | `/api/patients/{id}` | Update patient info |

---

## 📸 Screenshots

> 🚧 Screenshots will be added soon. Run the app locally to see the UI!

To add your own:
1. Run the app locally
2. Take screenshots of key pages (home, doctor search, booking form, dashboard)
3. Save them to `docs/screenshots/`
4. Update this section with the paths

---

## 🔮 Future Enhancements

- [ ] **JWT Authentication** — Secure login for patients and doctors
- [ ] **Spring Security** — Role-based access control (Patient / Doctor / Admin)
- [ ] **Email Notifications** — Appointment confirmation and reminders
- [ ] **Search & Filter** — Advanced doctor search with multiple filter criteria
- [ ] **Doctor Ratings** — Patient-submitted reviews after consultations
- [ ] **Payment Integration** — Consultation fee processing
- [ ] **Video Consultation** — Integrated telemedicine feature
- [ ] **Docker** — Containerized deployment
- [ ] **AWS / Azure Deployment** — Cloud hosting
- [ ] **Unit Tests** — JUnit + Mockito test coverage

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the project
2. Create your feature branch: `git checkout -b feature/AmazingFeature`
3. Commit your changes: `git commit -m 'Add AmazingFeature'`
4. Push to the branch: `git push origin feature/AmazingFeature`
5. Open a Pull Request

---

## 👨‍💻 Author

**Omkar Rajmane**

- 🌐 GitHub: [@OMKARRAJMANE1](https://github.com/OMKARRAJMANE1)
- 💼 LinkedIn: [omkar-rajmane-6509512a4](https://linkedin.com/in/omkar-rajmane-6509512a4)
- 📧 Email: [omkarmrajmane1@gmail.com](mailto:omkarmrajmane1@gmail.com)
- 📍 Location: Pune, India

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

<div align="center">
  <p>Made with ❤️ by Omkar Rajmane · PG-DAC, IACSD Pune 2024</p>
  <p>
    <a href="https://github.com/OMKARRAJMANE1/Ask-Your-Doctor/stargazers">⭐ Star this repo if you found it helpful!</a>
  </p>
</div>

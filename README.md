# MediCare - Clinic Management & Appointment System

MediCare is a comprehensive healthcare platform built with **ASP.NET Core MVC** and **N-Tier Architecture** to streamline clinic management, doctor schedules, and patient appointments.

---

## Architecture
The system follows **N-Tier Architecture** for clean separation of concerns:
- **`MediCare.Web`**: Presentation Layer (ASP.NET Core MVC)
- **`MediCare.Services`**: Business Logic Layer
- **`MediCare.Data`**: Data Access Layer (Entity Framework Core)

---

## Key Technologies & Patterns
- **Framework:** ASP.NET Core MVC
- **ORM & DB:** Entity Framework Core & SQL Server
- **Security:** ASP.NET Core Identity (Roles: Admin, Doctor, Patient)
- **Design Patterns:** Repository Pattern, Unit of Work, Dependency Injection

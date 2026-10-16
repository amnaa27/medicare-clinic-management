# MediCare: Clinic Management & Appointment System
## 3. Requirements Gathering

**Program:** DEPI | **Document status:** Submission for 16 Oct 2026

Priority legend (MoSCoW): **M** = Must have, **S** = Should have, **C** = Could have.

---

## 3.1 Stakeholder Analysis

| Stakeholder | Type | Description | Needs and Expectations |
|---|---|---|---|
| Patient | Primary user | Books appointments and accesses personal medical information | Search doctors, book/cancel/reschedule, view appointment history, access medical records and prescriptions, update personal and medical history, download documents, receive reminders, manage notification preferences |
| Doctor | Primary user | Medical professional who manages schedules and patients | Manage working hours and vacation days, confirm or reject appointments, view daily and weekly schedule, access patient information and history, write medical records and prescriptions, print prescriptions |
| Administrator | Primary user | Manages the clinic system and its data | Approve doctor registrations, manage doctors, patients and specializations, manage clinic settings, view and manage all appointments, view analytics and reports, export reports |
| Twilio | External service | SMS provider | Deliver SMS appointment reminders, including 24 hours before the appointment |
| SendGrid | External service | Email provider | Deliver email notifications and appointment reminders |
| Development team and lecturer | Project stakeholders | Build, review and grade the project | Clear documentation, maintainable code, working demo |

> Twilio and SendGrid are external service providers, not human users.

---

## 3.2 User Stories

### Patient

| ID | User Story | Priority |
|---|---|---|
| US-P01 | As a patient, I want to register and log in so that I can use the system securely. | M |
| US-P02 | As a patient, I want to search for doctors by specialization, location and availability so that I can find a suitable doctor. | M |
| US-P03 | As a patient, I want to see a doctor's free time slots on a calendar and book one so that I can schedule my visit. | M |
| US-P04 | As a patient, I want to cancel or reschedule my appointment so that I can change my plans. | M |
| US-P05 | As a patient, I want to view my upcoming appointments and appointment history so that I can keep track of my visits. | M |
| US-P06 | As a patient, I want to be notified when my appointment is confirmed or rejected so that I know its status. | M |
| US-P07 | As a patient, I want to access my medical records so that I can review my medical information. | M |
| US-P08 | As a patient, I want to view my prescriptions and prescription history so that I can review issued medication. | M |
| US-P09 | As a patient, I want to update my personal information, allergies and medical history so that my profile is current. | M |
| US-P10 | As a patient, I want to download my medical documents so that I keep copies of them. | S |
| US-P11 | As a patient, I want to receive SMS and email reminders so that I do not miss appointments. | M |
| US-P12 | As a patient, I want to customize my notification preferences so that I choose how I am notified. | S |

### Doctor

| ID | User Story | Priority |
|---|---|---|
| US-D01 | As a doctor, I want to register and wait for admin approval so that my account is verified. | M |
| US-D02 | As a doctor, I want to manage my working hours and vacation days so that patients only book when I am available. | M |
| US-D03 | As a doctor, I want to view my daily and weekly appointments in calendar and list views so that I can organize my day. | M |
| US-D04 | As a doctor, I want to confirm or reject appointment requests so that I control my schedule. | M |
| US-D05 | As a doctor, I want to be notified instantly when a new appointment is booked so that I can respond quickly. | M |
| US-D06 | As a doctor, I want quick access to patient information and history so that I can prepare for the visit. | M |
| US-D07 | As a doctor, I want to record diagnosis, symptoms and treatment notes for each visit so that medical records are complete. | M |
| US-D08 | As a doctor, I want to upload test results, X-rays and documents to a patient record so that all information is in one place. | S |
| US-D09 | As a doctor, I want to create digital prescriptions with medication, dosage and frequency so that instructions are clear and stored. | M |
| US-D10 | As a doctor, I want to print prescriptions in a print-friendly format so that I can give printed copies. | S |
| US-D11 | As a doctor, I want to access prescription history so that I can review earlier treatment. | S |

### Administrator

| ID | User Story | Priority |
|---|---|---|
| US-A01 | As an administrator, I want to approve doctor registrations so that only verified doctors are active. | M |
| US-A02 | As an administrator, I want to add and update doctor profiles so that doctor information is accurate. | M |
| US-A03 | As an administrator, I want to manage patients and their access so that accounts can be administered. | M |
| US-A04 | As an administrator, I want to manage specializations and clinic settings so that the configuration is maintained. | M |
| US-A05 | As an administrator, I want to view and manage all appointments so that I oversee clinic activity. | M |
| US-A06 | As an administrator, I want to view monthly appointment statistics so that I monitor activity over time. | S |
| US-A07 | As an administrator, I want to see the most popular doctors and specializations so that I understand demand. | S |
| US-A08 | As an administrator, I want to see patient demographics and trends so that I understand the patient population. | S |
| US-A09 | As an administrator, I want revenue reports and financial summaries so that I review the clinic's finances. | S |
| US-A10 | As an administrator, I want to export reports to PDF or Excel so that I can save and share them. | S |

### System and Notifications

| ID | User Story | Priority |
|---|---|---|
| US-N01 | As a patient, I want an SMS reminder 24 hours before my appointment so that I remember the visit. | M |
| US-N02 | As a patient, I want appointment notifications by email so that I receive information electronically. | M |
| US-N03 | As a system operator, I want reminders to be scheduled automatically so that no manual work is needed per appointment. | M |
| US-N04 | As a user, I want real-time in-app notifications so that I see updates without refreshing the page. | M |

---

## 3.3 Use Cases

The five core use cases below cover the main flows of the system. The remaining features are described by the user stories (3.2) and functional requirements (3.4).

### UC-01: Search Doctors and Book Appointment

| Field | Description |
|---|---|
| Actor | Patient |
| Precondition | Patient is logged in |
| Main flow | 1. Patient searches and filters doctors. 2. Patient selects a doctor and a free slot. 3. System checks for conflicts and saves the appointment as "Pending". 4. System notifies the doctor. |
| Alternative flow | Slot already taken: system asks the patient to choose another slot |
| Postcondition | Appointment is saved and the slot is reserved |

### UC-02: Cancel or Reschedule Appointment

| Field | Description |
|---|---|
| Actor | Patient |
| Precondition | Patient has an upcoming appointment |
| Main flow | 1. Patient selects the appointment and chooses cancel or reschedule. 2. For rescheduling, patient picks a new free slot. 3. System updates the appointment, frees the old slot and notifies the doctor. |
| Alternative flow | New slot unavailable: system asks for another slot |
| Postcondition | Appointment is cancelled or moved |

### UC-03: Confirm or Reject Appointment

| Field | Description |
|---|---|
| Actor | Doctor |
| Precondition | A pending appointment request exists |
| Main flow | 1. Doctor reviews the request on the dashboard. 2. Doctor confirms or rejects it. 3. System updates the status and notifies the patient. |
| Alternative flow | Rejected: the slot is freed |
| Postcondition | Status is "Confirmed" or "Cancelled" |

### UC-04: Create Medical Record and Issue Prescription

| Field | Description |
|---|---|
| Actor | Doctor |
| Precondition | An appointment exists for the patient |
| Main flow | 1. Doctor enters symptoms, diagnosis and treatment notes, and uploads test results if needed. 2. Doctor adds medications with dosage and frequency. 3. System saves both and offers a print-friendly prescription. |
| Alternative flow | Missing required field: system shows a validation error |
| Postcondition | Record and prescription appear in the patient's history |

### UC-05: Approve Doctor Registration

| Field | Description |
|---|---|
| Actor | Admin |
| Precondition | A doctor registration is pending |
| Main flow | 1. Admin opens the pending doctors list. 2. Admin reviews the details and approves or rejects. 3. System activates or declines the account and notifies the doctor. |
| Alternative flow | Rejected: the doctor cannot log in |
| Postcondition | Doctor account is active or declined |

---

## 3.4 Functional Requirements

### Authentication and User Management

| ID | Requirement | Role | Priority | Related Stories |
|---|---|---|---|---|
| FR-01 | The system shall allow Patients and Doctors to register with role-specific validated data. | Patient, Doctor | M | US-P01, US-D01 |
| FR-02 | The system shall provide login and logout using ASP.NET Identity. | All | M | US-P01 |
| FR-03 | The system shall support three roles (Patient, Doctor, Admin) and restrict functions by role. | All | M | US-P01 |
| FR-04 | Doctor accounts shall stay inactive until approved by the Admin. | Admin, Doctor | M | US-A01, US-D01 |
| FR-05 | The Admin shall be able to activate, deactivate and manage patient and doctor accounts. | Admin | M | US-A03 |

### Doctor Listing and Profiles

| ID | Requirement | Role | Priority | Related Stories |
|---|---|---|---|---|
| FR-06 | The system shall list active doctors with specialization, consultation fee and profile image. | Patient | M | US-P02 |
| FR-07 | The system shall allow searching and filtering doctors by specialization, location and availability. | Patient | M | US-P02 |
| FR-08 | The Admin shall be able to add and edit doctor profiles. | Admin | M | US-A02 |
| FR-09 | The Admin shall be able to manage the list of specializations. | Admin | M | US-A04 |

### Schedules and Availability

| ID | Requirement | Role | Priority | Related Stories |
|---|---|---|---|---|
| FR-10 | A doctor shall be able to set working days, working hours and slot length. | Doctor | M | US-D02 |
| FR-11 | A doctor shall be able to add vacation days and block time ranges. | Doctor | M | US-D02 |
| FR-12 | The system shall generate free slots from working hours, excluding booked and blocked times. | System | M | US-P03 |

### Appointments

| ID | Requirement | Role | Priority | Related Stories |
|---|---|---|---|---|
| FR-13 | The system shall display available time slots in an interactive calendar (FullCalendar.js). | Patient | M | US-P03 |
| FR-14 | A patient shall be able to book an appointment by selecting a date and a free slot. | Patient | M | US-P03 |
| FR-15 | The system shall prevent double-booking of the same doctor and time, including simultaneous requests. | System | M | US-P03 |
| FR-16 | A patient shall be able to cancel an upcoming appointment, which frees the slot. | Patient | M | US-P04 |
| FR-17 | A patient shall be able to reschedule an upcoming appointment to another free slot. | Patient | M | US-P04 |
| FR-18 | Appointments shall have a status: Pending, Confirmed, Completed or Cancelled. | System | M | US-D04 |
| FR-19 | A doctor shall be able to confirm or reject appointment requests. | Doctor | M | US-D04 |
| FR-20 | A patient shall see upcoming appointments and appointment history. | Patient | M | US-P05 |
| FR-21 | A doctor shall see daily and weekly appointments in calendar and list views. | Doctor | M | US-D03 |
| FR-22 | The Admin shall be able to view, filter and manage all appointments. | Admin | M | US-A05 |

### Real-Time Notifications

| ID | Requirement | Role | Priority | Related Stories |
|---|---|---|---|---|
| FR-23 | The system shall notify the doctor in real time (SignalR) when an appointment is booked. | Doctor | M | US-D05, US-N04 |
| FR-24 | The system shall notify the patient in real time when an appointment is confirmed or rejected. | Patient | M | US-P06, US-N04 |
| FR-25 | The system shall send reminders before scheduled appointments. | Patient | M | US-N01 |

### Medical Records

| ID | Requirement | Role | Priority | Related Stories |
|---|---|---|---|---|
| FR-26 | A doctor shall be able to create a medical record per visit with symptoms, diagnosis and treatment notes. | Doctor | M | US-D07 |
| FR-27 | A doctor shall be able to upload test results, X-rays and documents to a record. | Doctor | S | US-D08 |
| FR-28 | A doctor shall be able to view a patient's complete medical history and basic information. | Doctor | M | US-D06 |
| FR-29 | A patient shall be able to view their medical records and download their documents. | Patient | M | US-P07, US-P10 |

### Prescriptions

| ID | Requirement | Role | Priority | Related Stories |
|---|---|---|---|---|
| FR-30 | A doctor shall be able to create a digital prescription with medication name, dosage and frequency. | Doctor | M | US-D09 |
| FR-31 | The system shall provide a print-friendly prescription view. | Doctor | S | US-D10 |
| FR-32 | A doctor and the patient shall be able to view prescription history. | Doctor, Patient | M | US-D11, US-P08 |

### External Notifications

| ID | Requirement | Role | Priority | Related Stories |
|---|---|---|---|---|
| FR-33 | The system shall send SMS appointment reminders through Twilio. | Patient | M | US-N01 |
| FR-34 | The system shall send email notifications through SendGrid. | Patient | M | US-N02 |
| FR-35 | The system shall automatically schedule reminders 24 hours before each appointment. | System | M | US-N03 |
| FR-36 | A patient shall be able to set notification preferences (SMS, email). | Patient | S | US-P12 |

### Patient Profile

| ID | Requirement | Role | Priority | Related Stories |
|---|---|---|---|---|
| FR-37 | A patient shall be able to update personal information, allergies and medical history. | Patient | M | US-P09 |

### Admin Dashboard, Analytics and Reports

| ID | Requirement | Role | Priority | Related Stories |
|---|---|---|---|---|
| FR-38 | The Admin shall be able to manage clinic settings. | Admin | S | US-A04 |
| FR-39 | The system shall show monthly appointment statistics in charts (Chart.js). | Admin | S | US-A06 |
| FR-40 | The system shall show the most popular doctors and specializations. | Admin | S | US-A07 |
| FR-41 | The system shall show patient demographics and trends. | Admin | S | US-A08 |
| FR-42 | The system shall show revenue reports and financial summaries. | Admin | S | US-A09 |
| FR-43 | The Admin shall be able to export reports to PDF and Excel. | Admin | S | US-A10 |

### User Interface

| ID | Requirement | Role | Priority |
|---|---|---|---|
| FR-44 | The interface shall provide a dark/light mode toggle. | All | C |

---

## 3.5 Non-Functional Requirements

> Numeric targets are the team's proposed values and are consistent with the KPIs in the Project Planning document.

| ID | Category | Requirement | Measure / Target |
|---|---|---|---|
| NFR-01 | Performance | Core pages (login, doctor search, booking) shall respond quickly. | Less than 2 s with 100 concurrent users |
| NFR-02 | Performance | Large lists shall use server-side paging and filtering. | Page size limited, indexes on foreign keys |
| NFR-03 | Security | Passwords shall be stored as salted hashes through ASP.NET Identity, with a minimum password policy. | Minimum 8 characters, mixed types |
| NFR-04 | Security | Role checks shall be enforced on the server for every action. | A patient cannot open another patient's data, even by typing a URL |
| NFR-05 | Security | The system shall be protected against SQL injection, XSS and CSRF, and validate all input on the server. | OWASP Top 10 review with no open critical issues |
| NFR-06 | Privacy | The site shall run over HTTPS only; patient data shall not appear in URLs or logs. | HTTPS enforced, log review |
| NFR-07 | Security | Sessions shall time out after inactivity. | Timeout configured (for example 30 minutes) |
| NFR-08 | Security | Secrets (API keys, connection strings) shall not be stored in the repository. | User secrets and environment variables |
| NFR-09 | Reliability | The system shall target high availability after deployment. | 99.5% uptime |
| NFR-10 | Reliability | Database backups shall be taken regularly and a restore procedure documented. | Daily backups, one test restore |
| NFR-11 | Reliability | Unexpected errors shall show a generic message and be logged; a failed booking shall not leave partial data. | Transactions through Unit of Work |
| NFR-12 | Data Integrity | Double-booking shall be blocked at database level. | Concurrency test ends with exactly one successful booking |
| NFR-13 | Data Integrity | Doctors and patients with appointments shall be deactivated, not deleted; appointment changes shall be logged. | Soft delete, audit fields |
| NFR-14 | Usability | The interface shall be responsive on desktop and mobile with clear validation messages. | Bootstrap 5, tested on Chrome, Edge and Firefox |
| NFR-15 | Usability / Accessibility | The interface shall meet basic accessibility practices. | Sufficient contrast, labels, keyboard navigation |
| NFR-16 | Maintainability | The three-layer structure shall be kept: no business rules or queries in `MediCare.Web`. | Code review checklist |
| NFR-17 | Maintainability | Core booking and scheduling rules shall be covered by unit tests. | At least 70% coverage of those rules |
| NFR-18 | Portability / Deployment | The system shall be deployable to Azure with an automated pipeline. | CI/CD runs on every merge to main |
| NFR-19 | Compatibility | External services shall be accessed through interfaces so they can be replaced or mocked. | Dependency Injection |

# 🏨 StayFlow

### Modern Hotel Booking & Management Platform

**StayFlow** is a full-stack hotel booking and management system that connects **guests, hotel managers, and administrators** through role-based dashboards and automated workflows.

It supports the complete hotel lifecycle — from **hotel discovery and room booking** to **booking management, cancellation requests, notifications, and email communication**.

---

## 🌟 Why StayFlow?

Most hotel booking applications focus only on the customer booking experience.

**StayFlow goes further.**

It provides separate workflows for:

- 👤 **Guests** — discover hotels, book rooms, manage reservations
- 🧑‍💼 **Managers** — manage properties, rooms, bookings, and cancellations
- 🛡️ **Admins** — manage the entire platform and its users

The system combines **authentication, role-based authorization, database management, booking workflows, notifications, and automated email communication** into one application.

---

## 🚀 Live Project

🔗 **Live Demo:** `Coming Soon`

🔗 **GitHub:** `YOUR_GITHUB_REPOSITORY_URL`

> Screenshots and live demo will be added here.

---

# ✨ Core Features

## 👤 Guest Experience

### 🏨 Discover Hotels
- Browse available hotels
- Search hotels
- Filter by location
- View hotel ratings
- View hotel descriptions and images
- Explore available rooms

### 🛏️ Room Booking
- Select check-in and check-out dates
- View room details
- View room price and amenities
- Book available rooms
- Automatically update room availability

### 📋 Reservation Management
- View current reservations
- View booking history
- Update booking dates
- Request cancellation
- Track booking status

### 🔔 Notifications
Guests receive notifications for important reservation events.

### 📧 Email Confirmation
After booking, StayFlow can automatically send a confirmation email containing:

- Booking ID
- Hotel
- Room
- Check-in date
- Check-out date
- Booking status

The project implements this booking workflow directly in the Flask application.

---

# 🧑‍💼 Manager Dashboard

Managers have their own dedicated management workflow.

### 🏨 Hotel Management
Managers can manage their assigned properties.

### 🛏️ Room Management

- Add rooms
- Edit rooms
- Delete rooms
- Update room availability
- Manage room types
- Manage pricing
- Manage amenities
- Manage room images

### 📋 Booking Management

Managers can:

- View reservations
- Monitor booking status
- Update booking status
- Review guest information

### ❌ Cancellation Management

Guests can submit cancellation requests.

Managers can then:

```text
Pending
   ↓
Manager Review
   ↓
 ┌───────────────┐
 │               │
Approve        Reject
 │               │
 ↓               ↓
Cancelled      Rejected
 │
 ↓
Room Available
```

When a cancellation is approved, StayFlow updates the booking and makes the room available again.

---

# 🛡️ Admin Dashboard

The administrator has platform-level control.

### Admin capabilities include:

- 👥 User management
- 🏨 Hotel management
- 🧑‍💼 Manager management
- 🛏️ Room management
- 📋 Booking management
- ❌ Cancellation monitoring
- 🔗 Hotel-manager assignment
- 🔔 System notifications
- 📊 Platform-level monitoring

Managers can also be assigned to individual hotels, allowing responsibility to be separated between properties.

---

# 🔐 Authentication & Role-Based Access

StayFlow uses **Supabase Authentication** with application-level roles.

### Supported roles

```text
┌──────────────┐
│     ADMIN    │
└──────┬───────┘
       │
       ├── Platform Management
       │
       ▼
┌──────────────┐
│   MANAGER    │
└──────┬───────┘
       │
       ├── Property Management
       │
       ▼
┌──────────────┐
│    GUEST     │
└──────────────┘
       │
       └── Hotel Booking
```

Public registration is restricted to the **Guest** role, while privileged users are created through server-side administrative operations.

Supported roles are explicitly validated as:

```python
admin
manager
guest
```



---

# 🏗️ Architecture

```text
                         ┌────────────────────┐
                         │      USERS         │
                         │ Guest / Manager     │
                         │       / Admin      │
                         └─────────┬──────────┘
                                   │
                                   ▼
                         ┌────────────────────┐
                         │     Flask App      │
                         │   Python Backend    │
                         └─────────┬──────────┘
                                   │
             ┌─────────────────────┼─────────────────────┐
             │                     │                     │
             ▼                     ▼                     ▼
      ┌─────────────┐       ┌─────────────┐       ┌─────────────┐
      │  Supabase   │       │ PostgreSQL  │       │    SMTP     │
      │    Auth     │       │  Database   │       │   Email     │
      └─────────────┘       └─────────────┘       └─────────────┘
             │                     │                     │
             └─────────────────────┼─────────────────────┘
                                   │
                                   ▼
                         ┌────────────────────┐
                         │ Hotel Booking      │
                         │ Management System  │
                         └────────────────────┘
```

---

# 🔄 Complete Booking Workflow

```text
Guest
  │
  ▼
Browse Hotels
  │
  ▼
Select Hotel
  │
  ▼
View Rooms
  │
  ▼
Select Dates
  │
  ▼
Book Room
  │
  ▼
Booking Created
  │
  ├──────────────► Room → Unavailable
  │
  ├──────────────► Guest Notification
  │
  ├──────────────► Manager Notification
  │
  ├──────────────► Admin Notification
  │
  └──────────────► Confirmation Email
```

This is implemented as a complete application workflow rather than simply storing a booking record. The booking operation also updates room availability and triggers notifications/email communication.

---

# 📧 Automated Email System

StayFlow includes an SMTP email service for application events.

### Supported email events

| Event | Recipient |
|---|---|
| Booking confirmed | Guest |
| New booking | Manager |
| Booking update | Guest |
| Cancellation requested | Manager |
| Cancellation decision | Guest |
| Hotel assignment | Manager |
| Admin event | Administrator |
| SMTP test | Configured recipient |

The email service generates structured HTML emails and supports asynchronous delivery. 

---

# 🗄️ Database

The system uses **PostgreSQL through Supabase**.

Major application entities include:

```text
Users
  │
  ├── Admin
  ├── Manager
  └── Guest

Hotels
  │
  └── Rooms

Bookings
  │
  └── Guest + Room + Hotel

Cancellation Requests

Notifications
```

The application uses `psycopg` for PostgreSQL connectivity and Supabase for authentication/services.

---

# 🛠️ Technology Stack

### Backend

- Python
- Flask

### Database

- PostgreSQL
- Supabase

### Authentication

- Supabase Auth
- JWT
- Flask Sessions

### Frontend

- HTML
- CSS
- JavaScript
- Jinja Templates

### Email

- SMTP
- HTML Email Templates

### Other

- Pillow
- Werkzeug
- python-dotenv
- Git
- GitHub

---

# 📂 Project Structure

```text
StayFlow/
│
├── app.py
├── database.py
├── stayflow_auth.py
├── auth_tools.py
├── email_service.py
├── mail_test.py
├── seed_demo_data.py
├── requirements.txt
│
├── templates/
│   ├── home.html
│   ├── login.html
│   ├── register.html
│   ├── guest_dashboard.html
│   ├── manager_dashboard.html
│   ├── admin_dashboard.html
│   └── ...
│
├── static/
│   ├── css/
│   └── js/
│
├── uploads/
│   └── hotel-images/
│
├── supabase/
│   └── schema.sql
│
├── .env.example
├── .gitignore
└── README.md
```

---

# 💻 Installation

## 1. Clone

```bash
git clone https://github.com/YOUR_USERNAME/stayflow.git
cd stayflow
```

## 2. Create Virtual Environment

### Windows

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

## 3. Install Dependencies

```bash
python -m pip install -r requirements.txt
```

The project uses Flask, PyJWT, Werkzeug, Pillow, Psycopg, Supabase, and python-dotenv.

---

# ⚙️ Environment Configuration

Create:

```text
.env
```

Example:

```env
DATABASE_URL=your_database_url

SUPABASE_URL=your_supabase_url
SUPABASE_ANON_KEY=your_anon_key
SUPABASE_SERVICE_ROLE_KEY=your_service_role_key

SESSION_SECRET=your_session_secret
JWT_SECRET=your_jwt_secret

SMTP_HOST=your_smtp_host
SMTP_PORT=587
SMTP_USERNAME=your_email
SMTP_APP_PASSWORD=your_app_password
MAIL_FROM=your_email
```

### ⚠️ Important

Never commit:

```text
.env
```

to GitHub.

Use `.env.example` for sharing the required variable names without exposing credentials.

---

# 🗃️ Database Setup

Run the SQL schema provided in:

```text
supabase/schema.sql
```

Then configure:

```env
DATABASE_URL=...
```

The seed script requires the database URL and expects the Supabase schema to be initialized first.

---

# 🌱 Seed Demo Data

Run:

```bash
python seed_demo_data.py
```

The script can create demo hotels, rooms, and authentication users.

Example properties:

```text
StayFlow Grand
Hyderabad

StayFlow Bay
Visakhapatnam

StayFlow Residency
Vijayawada
```



The seed operation is designed to be idempotent for the named demo hotels and room numbers.

---

# ▶️ Run the Application

```bash
python app.py
```

Open:

```text
http://127.0.0.1:5000
```

---

# 🧪 SMTP Testing

After configuring SMTP:

```bash
python mail_test.py your-email@example.com
```

The script checks whether SMTP is configured and sends a test email.

---

# 🔒 Security

StayFlow follows several security practices:

- Role-based access control
- Server-side privileged authentication operations
- Environment-based secret management
- Secure file names for uploads
- File-type validation
- Protected admin/manager routes
- HTTP-only session cookies
- Guest-only public registration
- Supabase authentication

The Supabase service-role key is used only for server-side administrative authentication operations.

---



# 📈 Project Highlights

| Area | Implementation |
|---|---|
| Authentication | Supabase Auth |
| Authorization | Role-based access |
| Backend | Flask |
| Database | PostgreSQL |
| Cloud Backend | Supabase |
| Booking | Complete booking workflow |
| Cancellation | Manager approval workflow |
| Notifications | In-app notifications |
| Email | SMTP automation |
| Images | Secure upload handling |
| Admin | Platform management |
| Manager | Property management |
| Guest | Reservation management |

---

# 🎯 Engineering Highlights

### 1. Role-Based Architecture

Different users receive different capabilities instead of using a single generic dashboard.

### 2. Real Business Workflow

Booking affects room availability, notifications, manager actions, and email communication.

### 3. Multi-Level Notification System

Important events can notify the relevant guest, manager, and administrator.

### 4. Cancellation Approval Flow

Cancellation is treated as a workflow requiring manager review rather than immediately deleting a booking.

### 5. External Service Integration

The application integrates:

```text
Flask
   +
Supabase Auth
   +
PostgreSQL
   +
SMTP
```

### 6. Idempotent Demo Seeding

Demo data can be seeded repeatedly without creating duplicate demo hotels and room numbers.

---

# 🚧 Future Improvements

- 💳 Payment gateway integration
- 📅 Date-range based room availability
- ⭐ Guest reviews and ratings
- 🔎 Advanced hotel search
- 📊 Advanced analytics
- ☁️ Cloud image storage
- 🔐 Password reset
- 🔑 Two-factor authentication
- 🐳 Docker support
- 🧪 Automated unit/integration tests
- 🚀 CI/CD pipeline
- 📱 Improved mobile experience
- 📖 API documentation

---

# 📚 Learning Outcomes

Building StayFlow provided practical experience with:

```text
Python
   ↓
Flask
   ↓
Authentication
   ↓
Authorization
   ↓
PostgreSQL
   ↓
Supabase
   ↓
CRUD Operations
   ↓
Booking Workflows
   ↓
Notifications
   ↓
Email Automation
   ↓
File Uploads
   ↓
Production-style Application Structure
```

---

# 👩‍💻 Author

## Prathibha Nattha

**B.Tech Computer Science & Engineering**

### Areas of Interest

`Software Engineering` · `Full-Stack Development` · `Backend Development` · `AI/ML`

---

# ⭐ If You Like This Project

If you find **StayFlow** useful or interesting:

⭐ Star the repository  
🍴 Fork the project  
🐛 Report issues  
💡 Suggest improvements

---

## 📄 License

This project is developed for **educational and portfolio purposes**.

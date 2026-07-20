# Integrated Waste Management Project Management System

## Software Architecture & Technical Specification

> Version 1.0

---

# Table of Contents

1. System Architecture
2. User Roles
3. User Flow
4. Project Workflow
5. Geofencing Workflow
6. Live Tracking Workflow
7. Notification Workflow
8. Admin Dashboard
9. Manager Dashboard
10. Backend Folder Structure
11. Database Design
12. API Modules
13. Development Roadmap
14. Recommended Tech Stack
15. Security
16. Deployment
17. Maintenance & Scalability

---

# 1. System Architecture

```text
                    Users
      ┌────────────────────────────────┐
      │ Field Worker (Expo Mobile App) │
      │ Manager (Expo Mobile App)      │
      │ Admin Panel (React + Vite)     │
      └───────────────┬────────────────┘
                      │
                HTTPS / REST API
                WebSockets
                      │
          ┌───────────▼────────────┐
          │ Node.js + Express API  │
          │ Authentication         │
          │ Business Logic         │
          │ Geofencing             │
          │ GPS Tracking           │
          │ Reports                │
          │ Notifications          │
          └───────────┬────────────┘
                      │
          ┌───────────▼────────────┐
          │      Supabase          │
          │ PostgreSQL             │
          │ Auth                   │
          │ Storage                │
          │ Realtime               │
          └───────────┬────────────┘
                      │
      Firebase Cloud Messaging (FCM)
```

Architecture uses a shared Express backend with Supabase as the managed backend platform for PostgreSQL, Authentication, Storage and Realtime.

# 2. User Roles

## Admin
- Manage managers
- Manage field workers
- Create projects
- Assign managers
- Monitor live GPS
- Analytics
- Reports
- Settings

## Manager
- Manage assigned projects
- Assign jobs
- Track workers
- Verify completed work
- Generate reports

## Field Worker
- Login
- View assigned jobs
- GPS navigation
- Geofence check-in/out
- Upload photos
- Add notes
- Complete jobs

# 3. User Flow

```text
Login
↓
View Assigned Jobs
↓
Navigate to Site
↓
Enter Geofence
↓
Check In
↓
Start Work
↓
Upload Photos
↓
Update Progress
↓
Complete Job
↓
Check Out
↓
Manager Review
```

# 4. Project Workflow

```text
Admin Creates Project
↓
Assign Manager
↓
Create Jobs
↓
Assign Worker
↓
Worker Accepts Job
↓
Travelling
↓
Arrived
↓
In Progress
↓
Completed
↓
Manager Verification
↓
Project Closed
```

# 5. Geofencing Workflow

```text
Worker Starts Shift
↓
GPS Tracking Enabled
↓
Location Updates
↓
Enter Geofence
↓
Allow Check-in
↓
Leave Geofence?
├── No
└── Yes
     ↓
Manager Notification
```

# 6. Live Tracking Workflow

```text
Worker Starts Shift
↓
Location Updates
↓
Express API
↓
Supabase PostgreSQL
↓
Supabase Realtime
↓
Manager Dashboard
```

# 7. Notification Workflow

```text
Job Assigned
↓
Push Notification
↓
Worker Accepts
↓
Manager Notified
↓
Job Completed
↓
Admin Notified
```

Additional notifications:
- New Project
- Worker Arrived
- Worker Left Geofence
- Photo Uploaded
- Daily Reminder
- GPS Alert
- Work Completed

# 8. Admin Dashboard

- Total Projects
- Active Projects
- Total Managers
- Total Workers
- Workers Online
- Live GPS Map
- Jobs Today
- Completed Jobs
- Pending Jobs
- Delayed Jobs
- GPS Alerts
- Employee Performance
- Daily & Monthly Reports

# 9. Manager Dashboard

- Assigned Projects
- Today's Jobs
- Assigned Workers
- Live Worker Locations
- Completed Jobs
- Pending Jobs
- Missed Check-ins
- Uploaded Photos
- Progress Overview

# 10. Backend Folder Structure

```text
backend/
├── config/
├── middleware/
├── routes/
├── controllers/
├── services/
├── models/
├── auth/
├── users/
├── roles/
├── projects/
├── jobs/
├── tasks/
├── tracking/
├── geofencing/
├── attendance/
├── uploads/
├── notifications/
├── reports/
├── analytics/
├── settings/
├── utils/
└── server.js
```

# 11. Database Design

Core tables:
- users
- roles
- projects
- jobs
- tasks
- job_locations
- worker_locations
- attendance
- comments
- uploads
- notifications
- reports

# 12. API Modules

- Authentication
- Users
- Projects
- Jobs
- Tasks
- GPS Tracking
- Geofencing
- Attendance
- Reports
- Notifications
- File Uploads

# 13. Development Roadmap

## Phase 1
- Authentication
- User Roles
- Project Management
- Job Assignment
- Worker App
- GPS Tracking
- Geofencing
- Photo Upload
- Admin Dashboard
- Manager Dashboard
- Reports

## Phase 2
- Push Notifications
- Attendance
- Activity Logs
- Offline Sync
- Signature Capture
- Advanced Reports

## Phase 3
- AI Route Optimization
- Vehicle Tracking
- Heat Maps
- QR Codes
- Multi-company Support
- Predictive Analytics

# 14. Recommended Tech Stack

| Layer | Technology |
|---|---|
| Mobile | Expo (React Native) |
| Admin | React + Vite |
| Backend | Node.js + Express |
| Database | Supabase PostgreSQL |
| ORM | Prisma |
| Auth | Supabase Auth |
| Storage | Supabase Storage |
| Maps | Google Maps SDK |
| Realtime | Supabase Realtime |
| Validation | Zod |
| State | Zustand |
| API | REST + WebSockets |
| Deployment | Docker, Nginx, Vercel |

# 15. Security

- JWT Authentication
- Role-based authorization
- HTTPS
- Input validation with Zod
- Row Level Security where applicable
- Audit logging

# 16. Deployment

- Backend: Docker + Nginx
- Admin: Vercel
- Database/Auth/Storage: Supabase
- Mobile: Google Play & Apple App Store

# 17. Maintenance & Scalability

- Modular Express architecture
- Horizontal API scaling
- Background jobs
- Monitoring & logging
- Automated backups
- CI/CD pipeline

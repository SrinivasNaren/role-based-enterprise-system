# Role-Based Enterprise Task & Workflow Management System

---

## 1. Project Overview

### Goal of the Assignment

The goal of this project is to design and build an **enterprise-grade role-based system** similar to what is used internally by real companies. The system focuses not just on CRUD operations, but on **security, access control, scalability, and clean architecture**.

This application allows an organization to:

* Create departments and workflows
* Assign tasks and manage posts
* Control access using roles and permissions (RBAC)
* Track user actions and system activity
* Secure all APIs using JWT authentication

This project is intentionally designed to reflect **how senior engineers think before writing code**.

---

## 2. Why This Project Is Powerful

Most beginner projects focus only on:

* Login
* Simple dashboards
* CRUD APIs

This project goes deeper and demonstrates:

* Single login system for all roles
* Role-based redirection
* Permission-based UI rendering
* Backend-enforced authorization
* Token lifecycle handling
* Real enterprise workflows

Recruiters can clearly see:

* How the system is designed
* Why each decision was taken
* How the project scales

---

## 3. Core Concepts Used

### 3.1 RBAC (Role-Based Access Control)

RBAC ensures that users can only access what they are allowed to.

* Role = High-level identity (Admin, Manager, Employee, Viewer)
* Permission = Fine-grained action (create, read, update, delete)

Roles define **who you are**.
Permissions define **what you can do**.

---

### 3.2 Departments

Departments represent logical groups inside an organization.

Example:

* Engineering
* HR
* Finance

Departments help in:

* Assigning responsibilities
* Structuring workflows
* Reporting and analytics

---

### 3.3 Tasks & Workflows

* A **Task** is a unit of work assigned to a user
* A **Workflow** defines how tasks move from one state to another

Example workflow:

```
Created → In Progress → Review → Completed
```

---

### 3.4 Security Requirements

Security is treated as a **first-class feature**, not an afterthought.

* JWT-based authentication
* Access + Refresh token strategy
* Backend permission validation
* Account disable handling
* Token expiration handling

---

## 4. User Access Flow (Authentication & Authorization)

### 4.1 Single Login Page

All users log in from **one common login page**.
There are no separate login pages for different roles.

This reflects real enterprise systems.

---

### 4.2 What Happens After Login

1. User submits credentials
2. Backend validates credentials
3. JWT tokens are issued
4. Role & permissions are fetched from database
5. User is redirected based on role

---

### 4.3 Role-Based Redirection

| Role        | Redirected To      |
| ----------- | ------------------ |
| Super Admin | Admin Dashboard    |
| Manager     | Manager Dashboard  |
| Employee    | Employee Dashboard |
| Viewer      | Viewer Dashboard   |

---

### 4.4 JWT Expired Case

**When does JWT expire?**

* Token expiry time reached
* User logs out
* Token revoked

**Required Behavior:**

* Automatically log user out
* Redirect to login page
* Show message: "Session expired"

---

### 4.5 Account Disabled Case

**What does this mean?**

* Admin has disabled the user account

**Required Behavior:**

* Block all access
* Show "Account Disabled" message
* Do not allow token refresh

---

### 4.6 Where Role Logic Lives

* Role & permission logic lives in **Backend**
* Frontend only reads and reacts

This prevents security bypass.

---

## 5. User & Role Design

### 5.1 Purpose of User Table

The User table stores:

* Identity
* Role
* Permissions
* Account status

---

### 5.2 Sample User Table

| Name         | Role        | Permissions         | Status |
| ------------ | ----------- | ------------------- | ------ |
| Rahul Kumar  | Super Admin | Full Access         | Active |
| Priya Sharma | Manager     | Create / Update Own | Active |
| Rohan Verma  | Employee    | View / Create       | Active |
| Sai Teja     | Viewer      | View Only           | Active |

---

### 5.3 Role → Permission Mapping

* Roles have default permissions
* Permissions can be overridden per user
* Backend validates permission per API

---

## 6. Application Flow

### 6.1 Authentication Module

Features:

* Email / Password login
* Google OAuth login
* JWT access & refresh tokens
* Role stored in DB
* Permissions stored per user
* Password reset
* Automatic email notifications

Logic split:

* Backend: Validation, token generation, email
* Frontend: UI, routing, protected pages

---

### 6.2 Admin Workflow

Admin responsibilities:

* Manage users
* Assign permissions
* Enable/disable accounts
* Manage posts
* View analytics

Admin screens:

1. Dashboard
2. Author list
3. Add/Edit/Delete author
4. Permission assignment
5. Manage posts

---

### 6.3 Author Workflow

Author capabilities depend on permissions.

Screens:

* Author dashboard
* Create post
* Edit own post
* View allowed posts

If permission missing → "Access Denied"

---

## 7. Frontend Behavior Requirements

* Protected routes
* Dynamic menus based on permissions
* Global loader
* Error boundaries
* Proper logout
* Session expiration handling

---

## 8. Backend Behavior Requirements

* JWT-protected APIs
* RBAC middleware
* Token lifecycle handling
* Email delivery system
* Clean database schema

---

## 9. Phase-wise Execution Plan

### Phase 0 – Planning & Architecture

* Repo structure
* Tech stack decision
* Documentation

### Phase 1 – Authentication

* Backend auth APIs
* Frontend login
* JWT handling

### Phase 2 – RBAC & Permissions

* Role-permission mapping
* Authorization middleware
* Permission-based UI

### Phase 3 – Admin Features

* User management
* Permission control

### Phase 4 – Author Features

* Post CRUD
* Ownership checks

### Phase 5 – Dashboards & Analytics

* Metrics
* Charts

### Phase 6 – Email & Password Reset

* Forgot password
* Email notifications

### Phase 7 – Polish & Deployment

* UI cleanup
* Security review
* Deployment

---

## 10. Final Note

This documentation exists to show **how the system was thought through before coding**.

The code is only an implementation of this thinking.

That is what makes this project enterprise-level.

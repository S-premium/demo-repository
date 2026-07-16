# Public Library System - Core Navigation & System Flow

This repository shows the step-by-step logic, security gates, and Role-Based Access Control (RBAC) layers used in our Public Library Management System demo.

---

## System Logic Pipeline

### Phase 1: The Public Landing Gate (Welcome Page)
* **Guest Access (Unauthenticated):** Visitors can only click "Explore Books" to view titles on the Browse Page. They are restricted to read-only access and cannot borrow, reserve, or view other system features.
* **Registration Layer:** To unlock membership, a guest clicks "Sign Up". They must pass a security CAPTCHA (solving either a math problem or a Philippine History trivia question) to block automated bot accounts.
* **Approval Lock:** Successfully registered accounts are automatically set to `PENDING` status in the database. The user is blocked from logging in until an Admin manually reviews and switches their account to `ACTIVE`.

### Phase 2: Two-Factor Authentication Gateway
* **Credential Match:** Active users enter their username and password at the Login Page.
* **MFA Verification:** Upon matching credentials, the system dispatches a secure One-Time Password (OTP) to the user's registered Gmail. 
* **Expiration Timer:** The user must accurately input the OTP within a strict **5-minute expiration window** before the token becomes invalid.

### Phase 3: Role-Based Routing (RBAC Dashboard Split)
Once the OTP is verified, the system checks the account's database role and routes the user to their isolated dashboard:

#### A. Role: MEMBER (Dashboard)
* **Books Module:** Search titles, browse categories, borrow books, and build a personal favorites list.
* **Borrowed Dropdown:** Track active loans, check pending borrow requests, and fill out a printable Renewal Form (routed directly to the admin for validation).
* **Library Calendar:** View upcoming library calendar events, announcements and holidays.
* **Account Settings:** Update personal details, change security passwords, or enter the "Danger Zone" to request account deactivation/deletion (requires admin approval).

#### B. Role: LIBRARIAN (Staff Dashboard)
* **Book Management:** Full CRUD operations over library assets. Staff can manually input book data or use the automated **ISBN Fetch tool** to auto find book details.
* **Borrowing Management:** Review member histories, process daily returns, handle renewals, and flag assets as *Damaged* or *Lost*.
* **Staff Tools:** Write and pin community announcements, view dashboard user analytics, and export the entire physical inventory data into a **CSV file**.

#### C. Role: ADMIN (Full Authority)
* **System Overview:** Real-time visibility into overall platform metrics, system health charts, live online tracking variables, and stock of books indicators.
* **Account Requests Management:** Manually review, approve, or reject pending sign-ups, renewal forms, and user profile deletions.
* **User Governance:** Full database provisioning to create, activate, block, or delete any Borrower, Librarian, or Admin profile.
* **Manual Borrowing Form Workflow:** A dedicated administrative fallback path used to log walk-in transactions manually. The admin searches for the specific member profile, populates the borrowed book fields and uploads a scanned copy or picture of the physical paper receipt in **PNG format** straight to the database records.# Welcome to your organization's demo respository
This code repository (or "repo") is designed to demonstrate the best GitHub has to offer with the least amount of noise.

The repo includes an `index.html` file (so it can render a web page), two GitHub Actions workflows, and a CSS stylesheet dependency.

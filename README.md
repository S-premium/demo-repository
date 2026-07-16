#  Public Library System - Demo Workflow & Navigation Manual

Welcome to the **Demo Repository** for the Public Library System. This repository serves as the visual and functional mapping center for our capstone presentation. It tracks the complete user journey, system logic, and Role-Based Access Control (RBAC) structures that govern our live application layers.


## Interactive System Flowchart

Below is the architectural map of our system navigation. It visualizes how an incoming user moves from unauthenticated public viewing up to their strictly defined role environment.

```mermaid
graph TD
    Start[START: Welcome Page] --> Guest[Guest Mode: Browse Catalog]
    Start --> SignUp[Sign Up Gate]
    
    SignUp --> Captcha[CAPTCHA: Math/PH History]
    Captcha --> Pending[Status: PENDING]
    Pending --> AdminApprove{"Admin Approves?"}
    
    AdminApprove -->|No| Reject[Account Rejected]
    AdminApprove -->|Yes| Active[Status: ACTIVE]
    
    Active --> Login[Login Page]
    Login --> OTP[Email OTP Gateway: 5-Min Limit]
    OTP --> RBAC{"RBAC Router"}
    
    RBAC -->|Role: Member| Member[Member Dashboard]
    RBAC -->|Role: Librarian| Lib[Librarian Dashboard]
    RBAC -->|Role: Admin| Admin[Admin Command Center]
    
    subgraph "Member Dashboard"
        Member --> M1[Browse/Borrow Books]
        Member --> M2[Submit Renewals]
        Member --> M3[Print Library Card]
    end
    
    subgraph "Librarian Dashboard"
        Lib --> L1[Book CRUD / ISBN Fetch]
        Lib --> L2[Check-ins & Returns]
        Lib --> L3[Export CSV Inventory]
    end
    
    subgraph "Admin Dashboard"
        Admin --> A1[Manage Account Statuses]
        Admin --> A2[Manual Borrow Cash + PNG]
        Admin --> A3[Direct DB Controls]
    end

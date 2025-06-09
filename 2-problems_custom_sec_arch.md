# Enterprise Application Identity Fragmentation

In large enterprises:

- Applications are developed and deployed independently.
- Each web application stores **user identities locally** in its **own database**.
- Users end up with **multiple credentials**, **roles**, and **identities**, spread across apps.

This creates a fractured identity model. For example:

- **User1** is in *Database 1* and *Database 2*
- **User2** is in *Database 3* and *Database 4*
- **User3** is in *Database 2* and *Database 4*

Each user has different passwords and potentially different roles across apps. These apps do not coordinate authentication or provisioning.

---

## 📉 Problems with This Architecture

1. **Duplicated Identity**  
   Each application stores identity data independently, leading to inconsistent identity states.

2. **Too Many Passwords**  
   Users must manage separate passwords per app, increasing cognitive load and the likelihood of insecure practices.

3. **Decentralized Provisioning**  
   Applications must implement user creation, deletion, and role management—even though this is not core to their business logic.

4. **Unmanageable Deprovisioning**  
   Removing a user from all systems (e.g., when they leave the company) is manual, error-prone, and scales poorly.

5. **No Single Sign-On (SSO)**  
   Each app requires a separate login, severely impacting user experience and operational security.

6. **MFA Becomes App-Specific**  
   Implementing Multi-Factor Authentication (MFA) in each app is redundant and increases development complexity.

7. **Security Risks – Credential Exposure**  
   Passwords are handled by each application. Developers may inadvertently log or expose credentials, dramatically increasing attack surface.

---

## 🔍 Design Insight

> This design is not scalable, secure, or manageable.

Applications are being forced to act as **identity providers**, managing the full identity lifecycle when they should be focused on **business logic**. The lack of centralized identity control leads to operational overhead, inconsistent security practices, and user frustration.

---

## ✅ First Fix: Centralize Identity

The logical next step is to **centralize identity and access management (IAM)** in the enterprise
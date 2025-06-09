# Enterprise LDAP Security Architecture (Active Directory Integration)

## 🏗️ Updated Architecture Overview

```
+--------+        +---------+        +------------------+        +--------------+
|  User  | -----> | Browser | -----> |  Web Application | -----> | App Database |
+--------+        +---------+        +------------------+        +--------------+
                                        |          |
                                        | LDAP/636 |
                                        v          v
                              +-------------------------+
                              |   Active Directory (AD) |
                              | - User Credentials       |
                              | - Groups                |
                              +-------------------------+

                               +------------------------+
                               | Identity Provisioning  |
                               | Client (Admin Tools)   |
                               +------------------------+
```

---

## 🧩 Component Responsibilities

| Component                 | Responsibility                                                                  |
|---------------------------|---------------------------------------------------------------------------------|
| Web Application           | Business logic, UI, session creation, calling AD for authentication             |
| Application Database      | Stores app-specific data (not identity)                                         |
| Active Directory (LDAP)   | Centralized identity store: users, groups, credentials                          |
| Identity Provisioning     | Adds/removes users, resets passwords, manages groups                            |

---

## 🔐 Authentication Flow

1. **User visits web application**.
2. No active session is found → Login screen shown.
3. User submits username and password.
4. Web app calls Active Directory (via LDAP over port 636) to validate credentials.
5. If valid:
   - A session is created on the server.
   - A session cookie is sent to the user's browser.
6. The UI is tailored based on user’s group membership (from AD).
7. User interacts with authorized features.
8. On logout, session and cookie are destroyed.

---

## 📉 Key Improvements Over Custom Architecture

- ✅ **Single Identity**: Users use their enterprise credentials to access applications.
- ✅ **Password Consolidation**: One password for login to all enterprise services.
- ✅ **Centralized Provisioning**: Admins manage identity through AD tools, not custom app code.
- ✅ **Simplified Deprovisioning**: Disabling a user in AD cuts access to all connected apps.

---

## ⚙️ Provisioning Made Simple

Provisioning is handled by **Identity Provisioning Clients**, not the app itself.

Example actions:
- Create users/groups
- Assign users to groups
- Reset passwords
- Disable users

---

## 🚪 Deprovisioning Example

When an employee leaves:
- The admin disables the account in Active Directory.
- All app access is instantly revoked—no app-specific cleanup needed.

---

## ⚠️ Caveats

While significantly better than custom auth, LDAP integration still has some limitations:
- Web apps still handle session and role enforcement.
- Group-role mapping must be implemented per application.
- MFA, SSO, and audit logging require further architectural upgrades.

---

## 🧠 Summary

> “Moving authentication out of the application and into Active Directory simplifies management, strengthens security, and improves user experience.”
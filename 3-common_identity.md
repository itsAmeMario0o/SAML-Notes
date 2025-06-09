# Centralized Identity: The Case for a Common Identity Service

## Centralized Identity Store
```         
          +------------------+             
          |  Identity Store  | 
          +------------------+  
                   |           
        +-----------------------+
        |  User1   |   u1p      |
        |  User2   |   u2p      |
        |  User3   |   u3p      |
        +-----------------------+
```
## Application Architecture with Centralized Identity
```  
          +--------------------+             +--------------------+
          |  Identity Service  | ----------- |   Identity Store   |
          +--------------------+             +--------------------+
                    |
     +--------------+--------------+
     |                             |
+------------+               +------------+ 
| Web App 1  |               | Web App n  | 
+------------+               +------------+ 
      |                            |
      v                            v 
+-------------+             +-------------+
| Database 1  |             | Database 2  | 
+-------------+             +-------------+ 
```

## ✅ Benefits of a Common Identity Service

### Centralization

All user authentication is delegated to a **central identity service** that holds:

- Username
- Hashed Passwords
- First Name, Last Name, Email
- Phone Number, Picture
- Groups (used for role mapping)
- Manager, Department ID, etc.

This **decouples** identity from each application.

### Unified Authentication Workflow

- Every **Web Application** queries the **Identity Service** for login validation.
- Once authenticated, the app can request additional **user attributes** (like roles or group memberships).
- Identity and access control logic is removed from business logic.

---

## 🔐 What the Identity Service Stores

| Field              | Purpose                                |
|--------------------|----------------------------------------|
| User Credentials   | Username and hashed password           |
| First Name         | Personal identification                |
| Last Name          | Personal identification                |
| Email              | Communication and recovery             |
| Phone Number       | Contact method                         |
| Picture            | Optional profile enhancement           |
| Groups             | Role mapping mechanism for applications|
| Manager            | Org chart and delegation logic         |

> Groups can be mapped to application-specific roles.

---

## 🛠️ Capabilities of an Identity Service

- **Provisioning**: Add new users, set initial credentials, assign to groups.
- **Deprovisioning**: Revoke access, remove from group mappings.
- **Password Management**: Support reset flows, expiration policies, and credential rotation.
- **Self-Service**: Allow users to manage their own attributes (e.g., password change).

---

## 🏢 Real-World Enterprise Integration

In most organizations, a system like **Active Directory** already acts as the identity provider.

- When an employee joins, they’re provisioned in Active Directory.
- The same **enterprise credentials** are used to log into the network and (ideally) all enterprise apps.
- **Single Sign-On (SSO)** becomes possible across apps by federating authentication with the central identity provider.

---

## 📌 Key Insight

> Applications should not be in the business of managing identities.

Instead, they should **delegate** all identity and access operations to a centralized system designed for security, auditability, and lifecycle management.
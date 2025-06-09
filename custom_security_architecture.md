# SAML-Notes
SAML 2.0 and Identity Notes

## Custom Security Architecture

```
         +----------------------------+
         |      Security Layers       |
         +----------------------------+
         | ✅ Identity                |
         | ✅ Authentication (AuthN)  |
         | ✅ Authorization (AuthZ)   |
         | ✅ Identity Provisioning   |
         +----------------------------+
```

## Key Components

- **Identity**: Represents the digital identity of users, services, or systems.
- **Authentication (AuthN)**: Validates that the entity is who they claim to be (e.g., login with credentials or certificates).
- **Authorization (AuthZ)**: Determines what actions the authenticated entity is allowed to perform.
- **Identity Provisioning**: The process of creating, updating, and managing identity lifecycle across systems.

## Traditional Web Application Identity Flow

```
+--------+ +--------+ +-------------+ +-----------+ +-----------+
| User | -----> | Browser | -----> | Web App | -----> | Database |
|               | Chrome  |        | Business|        | App Data |
|                                  | Logic   |                   |
                                                      |+ User ID |
|                                  | + User         |            |
|                                  | Authentication |            |
+--------+ +--------+ +-------------+ +-----------+ +-----------+
```

### Explanation

In this traditional architecture:

- The **User** interacts with the application through a **web browser**.
- The **Web Application** acts as the main control point—it handles business logic, session management, and access control.
- **User identity** is stored in the **application’s database** alongside other application data.

### Implication

The burden of **authenticating and authorizing the user** falls entirely on the **web application**. This includes:

- Verifying credentials (e.g., username/password)
- Storing and retrieving user identity information from the local database

This model tightly couples identity with the application, making **identity verification an application-layer responsibility** and a bottleneck.

# Web App-Centric Identity and Authorization Flow

```
+--------+ +--------+ +-------------+ +-----------+ +-----------+
| User | -----> | Browser | -----> | Web App | -----> | Database |
|               | Chrome  |        | Business|        | App Data |
|                                  | Logic   |                   |
|                                                     |+ User ID |
|                                  | + User         |            |
|                                  | Authentication |            |
|                                                     | + User   |
|                                                     |  Roles   |
|                                  | + Identity     |            |
|                                  | Provisioning   |            |
+--------+ +--------+ +-------------+ +-----------+ +-----------+
```

### Process Overview

1. **User Login**:
   - The user submits login credentials via the browser.
   - The **Web Application** validates the credentials against stored identity data in the **Database**.

2. **Session Establishment**:
   - If successful, the application creates a **server-side session object**.
   - A **cookie** is sent to the user's browser—this cookie holds a session ID that maps to the server's session object.

3. **Subsequent Requests**:
   - The browser presents the cookie automatically.
   - The Web Application uses the cookie to find the session object and validate the user’s identity and **roles**.

4. **Access Control**:
   - Role-based logic is applied server-side to determine which data/views the user can access.

5. **Logout**:
   - The session object is invalidated.
   - The browser cookie is cleared, terminating the authenticated session.

---

### Identity Provisioning

> How are users and roles created?

This is handled through **identity provisioning**, which includes:

- Creating and updating user accounts.
- Assigning roles (permissions and access scope).
- Managing the full lifecycle of digital identities (creation, modification, deactivation).

Provisioning can be done manually (admin input), programmatically (e.g. APIs), or through federation/integration with an external identity provider.

---

### Summary

- Identity authentication + authorization logic is embedded in the application.
- The app is responsible for maintaining **both user trust and session state**.
- Cookies and sessions form the bridge between **client-side continuity** and **server-side access control**.


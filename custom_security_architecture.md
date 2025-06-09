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
| User | -----> | Browser| -----> | Web App | -----> | Database |
|               | Chrome |        | Business|        | App Data |
|                                 | Logic   |        |+ User ID |
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

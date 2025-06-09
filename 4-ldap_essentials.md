# Directory Services & LDAP Integration

## What Are Directory Services?

Directory services store information about enterprise resources including:

- Employees (users)
- Groups
- Machines
- Printers
- Access permissions

The most common enterprise-grade directory service is **Microsoft Active Directory**. Other examples include:

- Novell Directory Service (NDS)
- OpenLDAP

---

## Why Active Directory?

When a new employee joins, administrators provision their profile in Active Directory, including:

- First name, last name, email
- Username and password
- Group memberships

These groups represent **access privileges** across the enterprise. This centralized control:

- Simplifies provisioning and deprovisioning
- Centralizes group-based access control

---

## How Is Data Structured?

Entities in a directory service are stored in a **tree-like hierarchy**, similar to a file system.

## Why LDAP?

LDAP (Lightweight Directory Access Protocol) is the **standard protocol** for accessing directory services. It ensures:

- **Vendor neutrality**
- **Standardized access**
- **Language support across ecosystems**

LDAP is supported by:

- Java (LDAP client libraries)
- .NET
- Python
- Go
- Many others

This enables seamless integration with Active Directory and other directory services using a single access method.

---

## LDAP Hierarchical Directory Structure
```  
                        +-------------+            
                        |     ORG     | 
                        +-------------+            
                               |
                    +----------+----------+
                    |                     |
                +------------+      +------------+ 
                |  OU = US   |      | OU = EMEA  | 
                +------------+      +------------+ 
                      |                      |  
       +-----------------+                +--------------+
       |                 |                |              |
+----------+    +----------+       +----------+     +----------+
| CN = Eng |    | CN = Mkt |       | CN = QA  |     | CN = Fin |
+----------+    +----------+       +----------+     +----------+     
```

## LDAP Naming Components: `O`, `OU`, `CN`, and `DN`

### 🔹 `O` – **Organization**
- Represents the **top-level entity**, typically the company or enterprise.
- Often used as the LDAP root in non-domain-based DITs (Directory Information Trees).

---

### 🔹 `OU` – **Organizational Unit**
- Logical subdivisions **within the organization**, used to group related objects.
- Common examples: locations, departments, teams, or categories like `Users` or `Groups`.
- Can be nested to reflect hierarchy (e.g., region → department → team).

---

### 🔹 `CN` – **Common Name**
- Refers to a **specific object** in the directory—typically a user, group, device, or printer.
- This is the **leaf node** in most directory structures.

---

### 🔹 `DN` – **Distinguished Name**
- A **unique, fully-qualified path** to an object in the directory tree.
- Constructed by chaining the CN, OU(s), and O or domain components together.
- Example:

```
CN=Super Mario,OU=Game,OU=JPN,O=Nintendo
```

This DN uniquely identifies “Super Mario” as a user under the “Game” unit in the “JPN” unit of Nintendo.

---

### 🧠 Think of it Like a File Path

If LDAP were a filesystem:

```
O=Nintendo
 └── OU=JPN
      └── OU=Game
           └── CN=Super Mario
```

Each entity is made up of **key-value attributes**:

| Attribute     | Example        |
|---------------|----------------|
| `givenName`   | Bob            |
| `mail`        | bob@company.com|
| `department`  | Engineering    |

Different object classes (like users or printers) support different attributes.

---

### LDAP Characteristics

| Property             | Value         |
|----------------------|---------------|
| Protocol             | TCP           |
| Non-SSL Port         | 389           |
| SSL Port             | 636           |
| Encoding             | BER (Binary)  |
| Not an HTTP API      | TCP-based     |
| Operations Modeled   | CRUD + Bind   |

---

## LDAP Operations

```  
+-------------+  -- LDAP Operation -->  +-------------+        +-------------+
| Application |                         |  Directory  | ______ |  Directory  |
|             |                         |  Service    |        |  Database   |
+-------------+  <----- Response ----   +-------------+        +-------------+
```

| Operation | Description                                     |
|-----------|-------------------------------------------------|
| `bind`    | Authenticate and establish session              |
| `search`  | Query for users, groups, or other entities      |
| `add`     | Create new user or group                        |
| `delete`  | Remove user or group                            |
| `modify`  | Update entity attributes                        |
| `unbind`  | End session                                     |

> Think of `bind` as the login handshake and `unbind` as logout.

---

## Developer Notes

- Unlike JDBC, LDAP includes both the **API** and **wire-level protocol**
- The **same LDAP client** can connect to **any** directory service supporting LDAP v3
- Developers don’t need to understand the underlying BER encoding—LDAP libraries abstract that

### Example

If your enterprise moves from Novell Directory Services to Active Directory:

✅ **No code change needed** if using LDAP  
✅ Just point to the new directory host

---

## Why This Matters for Security Architecture

- Eliminates identity duplication
- Supports centralized role/group management
- Enables single sign-on (SSO) and MFA support
- Integrates directly into enterprise-grade directory infrastructure

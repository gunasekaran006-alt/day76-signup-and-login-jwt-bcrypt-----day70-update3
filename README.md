Authentication System Complete - Login Pipeline & JWT Architecture

A fully-featured Node.js & Express authentication backend built as part of the MERN Stack specialization. This iteration (Update 3) implements the secure user login gateway, cryptographic password evaluation using `bcryptjs`, and stateless session management via JSON Web Tokens (JWT).

---

## 🚀 Features

- **Robust Login Pipeline:** Authenticates users via secure email lookups and cryptographic credential matching.
- **Bcrypt Password Comparison:** Safely evaluates plain-text login inputs against database-hashed credentials using `bcrypt.compare()`.
- **Stateless JWT Generation:** Issues encrypted, time-bound access tokens signed with a server-side secret containing non-sensitive user metadata (Payload).
- **DNS Resolution Optimization:** Integrates native `dns.setServers()` configuration in the application core to mitigate ISP-level resolution faults with MongoDB Atlas SRV layers.
- **Remediated Registration Leaks:** Enhanced security boundary filters to ensure hashed credentials are never exposed in JSON responses.

---

## 🛠️ Tech Stack

- **Runtime & Core Framework:** Node.js & Express.js (v5.2.1)
- **Database Wrapper:** Mongoose (v9.7.3)
- **Token Security:** JsonWebToken (v9.0.3)
- **Cryptography Engine:** Bcryptjs (v3.0.3)

---

## 📁 Project Directory Layout

```text
├── config/
│   └── dbconnection.config.js   # Async MongoDB Atlas deployment configuration
├── controllers/
│   └── tasks.controller.js      # Task resource managers
├── models/
│   ├── tasks.model.js           # Schema for multi-state task objects
│   └── users.model.js           # Schema for user identity storage
├── routes/
│   ├── task.route.js            # Router pathways for core task metrics
│   └── user.route.js            # Router pathways for signup and login controllers
├── security/
│   └── authentication.security.js # Core logic for registration encryption & token issue
├── .env                         # Critical configuration values (Port, DB URI, JWT Secret)
├── main.js                      # Central execution controller & custom DNS registry
└── package.json                 # Dependency version manifests

```

---

## ⚙️ Configuration Setup

Append the newly introduced secret variable into your local `.env` file structure:

```env
port=8080
atlasport=mongodb+srv://<user>:<password>@cluster.mongodb.net/app-db
jwt_secret=your_super_secure_unpredictable_string_key

```

---

## 🔌 API Gateway Specifications

### Authentication Routes (`/user`)

| Method | Endpoint | Context Requirement | JSON Payload Schema | Expected Output | Status |
| --- | --- | --- | --- | --- | --- |
| **POST** | `/user/register` | Sign up context | `{ username, email, password }` | `{ message, user: { username, email } }` | `201 Created` |
| **POST** | `/user/login` | Session creation context | `{ email, password }` | `{ message, token }` | `200 OK` |

> 🔑 **Token Expiry Clause:** Every generated token has a strict mathematical lifetime of **24 hours** (`expiresIn: '24h'`). Post-expiration, endpoints will systematically drop access authentication.

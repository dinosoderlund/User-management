# User Management Database

A secure and optimized database for user management with support for:

- Registration & verification
- Login & account lockout
- Password reset
- Role management
- Login attempt logging

The project uses SQL Server, Python, and Azure Blob Storage to demonstrate a complete mini-pipeline.

---

## Features

### SQL
- Tables for users, roles, login attempts, and password resets
- Passwords are hashed using SHA2_256 + a unique salt for increased security
- Stored procedures for registration, login (with account lockout after 3 failed attempts), verification, and password reset
- Views for analyzing the most recent logins per user and login attempts per IP

### Python
- `login_attempts.py` → generates 800 fake login attempts
- `export_to_csv.py` → exports data from SQL to CSV
- `upload_to_blob.py` → uploads CSV to Azure Blob Storage

### Azure
- Secure cloud storage, secrets managed with `.env`

---

## Getting Started

1. Clone the repo
2. Create a `.env` file with your Azure connection string
3. Run the scripts in order:
   - `login_attempts.py`
   - `export_to_csv.py`
   - `upload_to_blob.py`

---

## Planned Features

- Upgrade password hashing to bcrypt or Argon2
- Add a REST API layer using FastAPI
- Containerize the project with Docker
- Deploy to Azure (Azure SQL + Azure Functions)
- Add a monitoring dashboard for login attempts and suspicious activity
- CI/CD pipeline with GitHub Actions
# User Management Database

A secure and optimized database for user management built in SQL Server,
with a cloud pipeline using Azure Blob Storage and Azure Data Factory.

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
- Blob Storage for secure cloud storage, secrets managed with `.env`
- Azure Data Factory pipeline that automatically processes uploaded files
- Storage event trigger that activates the pipeline when a new file is uploaded

## Getting Started

1. Clone the repo
2. Create a `.env` file with your Azure connection string:
```
AZURE_STORAGE_CONNECTION_STRING=your-connection-string-here
```
3. Install dependencies:
```
pip install faker pypyodbc python-dotenv azure-storage-blob
```
4. Run the scripts in order:
```
python login_attempts.py
python export_to_csv.py
python upload_to_blob.py
```

## Azure Pipeline

The ADF pipeline triggers automatically when a file is uploaded to Blob Storage:
```
upload_to_blob.py → user-data/login_attempts.csv → ADF trigger → user-data/processed/login_attempts_processed.csv
```

## Planned Features
- Upgrade password hashing to bcrypt or Argon2
- REST API layer using FastAPI
- Containerize with Docker
- Deploy to Azure (Azure SQL + Azure Functions)
- Monitoring dashboard for login attempts and suspicious activity
- CI/CD pipeline with GitHub Actions
<div align="center">
<img src="frontend/src/assets/VXDF logo.png" alt="VXDF Logo" width="200"/>
</div>

# VXDF: Validated eXploitable Data Flow

![Build](https://img.shields.io/badge/build-passing-brightgreen)
![License](https://img.shields.io/badge/license-Apache%202.0-blue)
![Frontend](https://img.shields.io/badge/frontend-React%2FTS-blue)
![Backend](https://img.shields.io/badge/backend-Python%2FFlask-yellow)

---

## 🖼️ Demo

<img src="frontend/src/assets/dashboard.png" alt="VXDF Dashboard" width="100%" style="border-radius:8px;box-shadow:0 2px 8px #0002;"/>

*VXDF Dashboard*

---

> **VXDF (Validated eXploitable Data Flow)** is a next-generation security validation platform for verifying, validating, and reporting on security findings from any scanner.

---

## 📑 Table of Contents
- [Overview](#overview)
- [Screenshots](#screenshots)
- [Architecture](#architecture)
- [Key Features](#key-features)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Running the Application](#running-the-application)
- [Dynamic Configuration](#dynamic-configuration)
- [Documentation](#documentation)
- [License](#license)
- [Author](#author)

---

## 📝 Overview
VXDF Validate helps security professionals validate findings from any scanner, automate exploitability checks, and generate standardized, actionable reports. The platform is fully API-driven, highly modular, and features a beautiful, modern UI.



---

## 🏗️ Architecture

![VXDF Architecture](docs/screenshots/architecture.png)



---

## ✨ Key Features
- **Dynamic, API-driven UI**: All data, navigation, and alerts are fetched from APIs or config files.
- **Modern Dashboard**: Beautiful charts, animated stats, and glassmorphism design.
- **Modular Sidebar**: Navigation is fully dynamic and easily configurable.
- **File Upload & Parsing**: Supports SARIF, JSON, CSV, and more.
- **Automated Validation**: Exploitability checks for each finding.
- **Standardized Reporting**: VXDF format for easy integration and compliance.
- **Responsive & Accessible**: Works on all modern browsers and devices.

---

## 📁 Project Structure

```
vxdf/
├── api/                # Backend API and core functionality
│   ├── core/           # Core validation engine
│   ├── models/         # Data models
│   ├── parsers/        # Input format parsers
│   └── validators/     # Vulnerability validators
├── config/             # Configuration files
│   └── config.json     # Main application configuration
├── data/               # Database and data files
│   └── vxdf_validate.db # SQLite database
├── docs/               # Documentation
├── frontend/           # React/TypeScript frontend
│   ├── src/            # Frontend source code
│   ├── package.json    # NPM dependencies
│   └── vite.config.ts  # Frontend configuration
├── logs/               # Log files
│   ├── backend.log     # Backend log output
│   └── frontend.log    # Frontend log output
├── scripts/            # Application scripts
│   ├── start-all.sh    # Start both backend and frontend
│   ├── stop-all.sh     # Stop all services
│   ├── start.sh        # Start just the backend
│   └── start-frontend.sh # Start just the frontend
├── test-data/          # Sample data for testing
│   └── sample-sarif.json # Example SARIF file
├── tests/              # Test scripts and utilities
├── venv/               # Python virtual environment (created on first run)
├── LICENSE             # License file
├── Makefile            # Make targets for common operations
├── README.md           # This file
└── requirements.txt    # Python dependencies (symlink to api/requirements.txt)
```

### Key Configuration Files

- `api/requirements.txt` - Backend Python dependencies
- `frontend/vite.config.ts` - Frontend configuration, including API proxy settings
- `config/config.json` - Application configuration
- `data/vxdf_validate.db` - SQLite database (created on first run)

### Important Paths

- Backend API: http://localhost:6789
- Frontend UI: http://localhost:3000
- Log files: `logs/backend.log` and `logs/frontend.log`

---

## 🚀 Installation

### Prerequisites
- Python 3.9+
- Node.js 16+ and npm
- Git

### Setup
```bash
git clone https://github.com/your-username/vxdf.git
cd vxdf
pip install -r requirements.txt
cd frontend
npm install
cd ..
```

---

## ▶️ Running the Application

### Quick Start

The easiest way to start the application is to use the single script:

```bash
# Start both backend and frontend with one command
./scripts/start-all.sh

# To stop all services
./scripts/stop-all.sh
```

The backend will be available at http://localhost:6789 and the frontend at http://localhost:3000.

### Individual Services

You can also start the services separately if needed:

```bash
# Start just the backend API
./scripts/start.sh

# In a separate terminal, start just the frontend
./scripts/start-frontend.sh
```

### Manual Setup

If you prefer to set up the application manually:

#### Backend

1. Create a virtual environment:
```bash
python3 -m venv venv
source venv/bin/activate
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Initialize the database (if it doesn't exist):
```bash
python3 api/load_sarif_to_db.py
```

4. Start the API server:
```bash
python3 api/main.py
```

#### Frontend

1. Navigate to the frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

---

## ⚙️ Dynamic Configuration
- **Sidebar navigation**: Driven by `frontend/src/config/sidebarConfig.ts` (or API in future)
- **Dashboard data**: All stats, charts, and tables are fetched from the backend API
- **Branding**: Logo and product name are configurable
- **Alerts/Notifications**: (Planned) Will be fetched from API

---

## 📚 Documentation
- [Startup Guide](docs/STARTUP.md)
- [API Documentation](docs/API.md)
- [VXDF Format](docs/Validated%20Exploitable%20Data%20Flow%20(VXDF)%20Format%20MD.md)

---

## 🔧 Avoiding Common Issues

1. **Import Order**: Always import models in the correct order to avoid circular imports:
   - First import database modules
   - Then import model classes

2. **Database Connection**: Ensure the database file (`data/vxdf_validate.db`) is accessible and correctly initialized.

3. **API Port**: The API runs on port 6789 by default. Make sure this port is available.

4. **Frontend Proxy**: The frontend uses a proxy to communicate with the API. Check `frontend/vite.config.ts` if you change the API port.

---

## ❓ Troubleshooting

If you encounter issues:

1. **Reset the database**:
```bash
rm data/vxdf_validate.db
python3 api/load_sarif_to_db.py
```

2. **Check logs**:
```bash
tail -f logs/backend.log
tail -f logs/frontend.log
```

3. **Verify API is accessible**:
```bash
curl http://localhost:6789/api/stats
```

4. **Clear temporary files**:
```bash
rm -rf logs/*.log
rm -f .vxdf_pids
```

5. **Fix port conflicts**:
```bash
lsof -ti:6789,3000 | xargs kill -9
```

---

## 🛠️ Makefile
A `Makefile` is provided for easy startup and health checks:

- `make dev` — Start both backend and frontend in dev mode.
- `make check` — Run health checks to ensure both servers are up and API endpoints respond.

---

## 📝 License

This project is licensed under the Apache License 2.0 — see the [LICENSE](./LICENSE) file for details.

---

## 👤 Author
Mihir Shah <mihirshah@vxdf.org>

---

## 👥 Contributing
Please read [CONTRIBUTING.md](CONTRIBUTING.md) and [INSTALLATION.md](INSTALLATION.md) for details on our code of conduct and the process for submitting pull requests. 
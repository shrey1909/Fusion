# Setting Up Fusion Locally with VS Code — Step-by-Step Guide

This guide walks you through setting up the **FusionIIIT** project on your local machine using **Visual Studio Code (VS Code)**.

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Install VS Code](#2-install-vs-code)
3. [Install Recommended VS Code Extensions](#3-install-recommended-vs-code-extensions)
4. [Fork and Clone the Repository](#4-fork-and-clone-the-repository)
5. [Open the Project in VS Code](#5-open-the-project-in-vs-code)
6. [Create and Activate a Virtual Environment](#6-create-and-activate-a-virtual-environment)
7. [Install Python Dependencies](#7-install-python-dependencies)
8. [Set Up PostgreSQL Database](#8-set-up-postgresql-database)
9. [Run Database Migrations](#9-run-database-migrations)
10. [Run the Development Server](#10-run-the-development-server)
11. [Docker-Based Setup (Alternative)](#11-docker-based-setup-alternative)
12. [Set Up Debugging in VS Code](#12-set-up-debugging-in-vs-code)
13. [Troubleshooting](#13-troubleshooting)

---

## 1. Prerequisites

Make sure the following are installed on your system before proceeding.

### Python 3.8

- **Ubuntu/Debian:**
  ```bash
  sudo apt update
  sudo apt install python3.8 python3.8-venv python3.8-dev python3-pip
  ```
- **Windows:**
  Download Python 3.8 from [python.org](https://www.python.org/downloads/release/python-383/) and install it.
  > **Important:** Check the box **"Add Python 3.8 to PATH"** during installation.
- **macOS:**
  ```bash
  brew install python@3.8
  ```

Verify the installation:
```bash
python3 --version
# or on Windows:
python --version
```

### Git

- **Ubuntu/Debian:** `sudo apt install git`
- **Windows:** Download from [git-scm.com](https://git-scm.com/download/win)
- **macOS:** `brew install git` or install Xcode Command Line Tools

Verify:
```bash
git --version
```

### PostgreSQL

- **Ubuntu/Debian:**
  ```bash
  sudo apt install postgresql postgresql-contrib libpq-dev
  ```
- **Windows:** Download from [postgresql.org](https://www.postgresql.org/download/windows/)
- **macOS:**
  ```bash
  brew install postgresql
  brew services start postgresql
  ```

### Build Tools (Ubuntu/Debian only)

```bash
sudo apt install build-essential
```

---

## 2. Install VS Code

Download and install VS Code from the official website:
👉 [https://code.visualstudio.com/](https://code.visualstudio.com/)

Choose the installer for your operating system (Windows, macOS, or Linux).

> **WSL Users (Windows):** If you are using Windows Subsystem for Linux, also install the [WSL extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) and follow the [VS Code WSL guide](https://code.visualstudio.com/docs/remote/wsl).

---

## 3. Install Recommended VS Code Extensions

Open VS Code and install the following extensions from the Extensions sidebar (`Ctrl+Shift+X`):

| Extension | Purpose |
|-----------|---------|
| [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) | Python language support, IntelliSense, linting, debugging |
| [Pylance](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance) | Fast Python language server |
| [Django](https://marketplace.visualstudio.com/items?itemName=batisteo.vscode-django) | Django template syntax highlighting and snippets |
| [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) | Enhanced Git integration |
| [SQLTools](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools) | Database management within VS Code |
| [WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) | **(Windows WSL users only)** Remote development in WSL |

---

## 4. Fork and Clone the Repository

1. Go to [https://github.com/FusionIIIT/Fusion](https://github.com/FusionIIIT/Fusion) and click **Fork** (top-right corner).
2. Open a terminal (or the VS Code integrated terminal with `` Ctrl+` ``) and clone your fork:
   ```bash
   git clone https://github.com/<your_username>/Fusion.git
   cd Fusion
   ```
3. Add the original repository as the upstream remote:
   ```bash
   git remote add upstream https://github.com/FusionIIIT/Fusion.git
   ```

---

## 5. Open the Project in VS Code

You can open the project folder in VS Code using either of these methods:

- **From the terminal** (inside the `Fusion` directory):
  ```bash
  code .
  ```
- **From VS Code:** Go to **File → Open Folder** and select the `Fusion` directory.

---

## 6. Create and Activate a Virtual Environment

Open the VS Code integrated terminal (`` Ctrl+` ``):

- **Ubuntu/macOS:**
  ```bash
  python3 -m venv env
  source env/bin/activate
  ```
- **Windows PowerShell:**
  ```powershell
  python -m venv env
  .\env\Scripts\Activate.ps1
  ```
  > **Note:** If you get a script execution error on Windows, run:
  > ```powershell
  > Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
  > ```
- **Windows Command Prompt:**
  ```cmd
  python -m venv env
  env\Scripts\activate.bat
  ```

### Select the Python Interpreter in VS Code

1. Press `Ctrl+Shift+P` to open the Command Palette.
2. Type **"Python: Select Interpreter"** and select it.
3. Choose the interpreter from your virtual environment (e.g., `./env/bin/python` or `.\env\Scripts\python.exe`).

---

## 7. Install Python Dependencies

With the virtual environment activated, run:

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

This installs all required packages including Django, PostgreSQL adapter, Django REST Framework, and more.

---

## 8. Set Up PostgreSQL Database

### Start PostgreSQL

- **Ubuntu/Debian:**
  ```bash
  sudo service postgresql start
  ```
- **macOS (Homebrew):**
  ```bash
  brew services start postgresql
  ```
- **Windows:** PostgreSQL runs as a service automatically after installation.

### Create the Database and User

Open the PostgreSQL shell:

- **Ubuntu/Debian:**
  ```bash
  sudo -u postgres psql
  ```
- **Windows/macOS:**
  ```bash
  psql -U postgres
  ```

Run the following SQL commands inside the `psql` prompt:

```sql
CREATE DATABASE fusionlab;
CREATE USER fusion_admin WITH PASSWORD 'hello123';
GRANT ALL PRIVILEGES ON DATABASE fusionlab TO fusion_admin;
ALTER USER fusion_admin CREATEDB;
\q
```

> **Note:** The database name (`fusionlab`), user (`fusion_admin`), and password (`hello123`) match the values in the project's development settings. Do not change them unless you also update `FusionIIIT/Fusion/settings/development.py`.

### (Optional) Import a Database Dump

If you have a database dump file provided by your team:

```bash
psql -U fusion_admin -d fusionlab < path/to/your/db_dump.sql
```

---

## 9. Run Database Migrations

Navigate to the Django project directory and apply migrations:

```bash
cd FusionIIIT
python manage.py migrate
```

If you need to create new migration files (after model changes):

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## 10. Run the Development Server

From inside the `FusionIIIT` directory:

```bash
python manage.py runserver
```

Open your browser and go to: **[http://localhost:8000](http://localhost:8000)**

To stop the server, press `Ctrl+C` in the terminal.

---

## 11. Docker-Based Setup (Alternative)

If you prefer using Docker instead of installing PostgreSQL locally:

### Prerequisites

- Install [Docker](https://docs.docker.com/get-docker/)
- Install [Docker Compose](https://docs.docker.com/compose/install/)

### Run with Docker

From the project root directory:

```bash
docker-compose up
```

This starts both the PostgreSQL database and the Django development server. Access the app at **[http://localhost:8000](http://localhost:8000)**.

To import a database dump into the Docker container:

```bash
docker exec -i fusion_db_1 psql -U fusion_admin -d fusionlab < path/to/your/db_dump.sql
```

To stop the containers:

```bash
docker-compose down
```

---

## 12. Set Up Debugging in VS Code

### Create a Launch Configuration

1. Click the **Run and Debug** icon in the sidebar (or press `Ctrl+Shift+D`).
2. Click **"create a launch.json file"** and select **Django**.
3. If the file is not auto-generated, create `.vscode/launch.json` manually with the following content:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Django: Runserver",
            "type": "debugpy",
            "request": "launch",
            "program": "${workspaceFolder}/FusionIIIT/manage.py",
            "args": ["runserver"],
            "django": true,
            "justMyCode": true
        }
    ]
}
```

4. Set breakpoints by clicking in the gutter next to any line number.
5. Press `F5` to start the server in debug mode.

---

## 13. Troubleshooting

### `psycopg2` installation fails

Install the PostgreSQL development libraries first:

```bash
# Ubuntu/Debian
sudo apt install libpq-dev python3-dev

# macOS
brew install postgresql
```

Then re-run `pip install -r requirements.txt`.

### Port 8000 already in use

Another process is using port 8000. Either stop that process or run Django on a different port:

```bash
python manage.py runserver 8001
```

### `ModuleNotFoundError` when running the server

Make sure your virtual environment is activated. You should see `(env)` at the beginning of your terminal prompt. If not, activate it again (see [Step 6](#6-create-and-activate-a-virtual-environment)).

### Database connection errors

- Verify PostgreSQL is running: `sudo service postgresql status` (Ubuntu) or `brew services list` (macOS).
- Verify the database and user exist by connecting: `psql -U fusion_admin -d fusionlab`.
- Make sure the credentials in `FusionIIIT/Fusion/settings/development.py` match your PostgreSQL setup.

### Windows: `Activate.ps1` cannot be loaded

Run the following in PowerShell as Administrator:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### Migrations fail with errors

If migrations fail, try resetting them:

```bash
python manage.py migrate --run-syncdb
```

Or if you have a database dump, drop and recreate the database:

```sql
-- In psql as postgres user
DROP DATABASE fusionlab;
CREATE DATABASE fusionlab;
GRANT ALL PRIVILEGES ON DATABASE fusionlab TO fusion_admin;
```

Then import your dump or re-run migrations.

---

## Summary of Commands

| Step | Command |
|------|---------|
| Clone | `git clone https://github.com/<your_username>/Fusion.git && cd Fusion` |
| Create venv | `python3 -m venv env` |
| Activate venv (Ubuntu/macOS) | `source env/bin/activate` |
| Activate venv (Windows) | `.\env\Scripts\Activate.ps1` |
| Install dependencies | `pip install -r requirements.txt` |
| Run migrations | `cd FusionIIIT && python manage.py migrate` |
| Start server | `python manage.py runserver` |
| Docker start | `docker-compose up` |
| Open in browser | [http://localhost:8000](http://localhost:8000) |

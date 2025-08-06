
# 🏥 OnlyMedChoice – Full Stack Healthcare Provider Search App

A modern full-stack healthcare platform that allows users to find doctors and specialists. Supports filtering by specialty, location, gender, insurance, and more.

---

## 📌 Table of Contents

1. [Project Overview](#project-overview)
2. [Project Structure](#project-structure)
3. [Getting Started (Dev Setup)](#getting-started-dev-setup)
4. [Backend Guide (Flask)](#backend-guide-flask)
5. [Frontend Guide (React + Vite)](#frontend-guide-react--vite)
6. [Docker Guide](#docker-guide)
7. [Environment Configuration](#environment-configuration)
8. [NER + Provider Search Flow](#ner--provider-search-flow)
9. [Production Notes](#production-notes)
10. [Troubleshooting](#troubleshooting)

---

## 📖 Project Overview

**OnlyMedChoice** is a full-stack healthcare search engine that allows patients to:

- Search for providers
- View provider details, addresses, ratings, languages, and plans
- Filter search by specialty, gender, insurance, and more
- Admin portal for management (in progress)

**Tech Stack:**
- **Frontend:** React, TypeScript, Vite
- **Backend:** Python, Flask, SQLAlchemy, spaCy
- **Database:** PostgreSQL (or SQLite in dev)
- **Deployment:** Docker + docker-compose

---

## 📁 Project Structure

```
OnlyMedChoice/
│
├── backend/ # Flask Backend
│ ├── app.py # Main Flask app
│ ├── models.py # Database models
│ ├── config.py # Configuration
│ ├── requirements.txt # Python dependencies
│ ├── Dockerfile # Backend Dockerfile
│ └── .dockerignore
│
├── src/ # React + TypeScript + Vite Frontend
│ ├── assets/logo.png
│ ├── admin/pages/Configure.tsx
│ ├── admin/pages/LoginPage.tsx
│ ├── admin/pages/SignupPage.tsx
│ ├── app/components/FilterSidebar.tsx
│ ├── app/components/Footer.tsx
│ ├── app/components/Header.tsx
│ ├── app/components/ProviderCard.tsx
│ ├── app/components/ProviderProfile.tsx
│ ├── app/components/SearchBar.tsx
│ ├── hooks/useProviderSearch.ts
│ ├── types/provider.ts
│ ├── config/uiConfig.ts
│ ├── App.tsx
│ ├── main.tsx
│ ├── index.css
│ ├── Dockerfile # Frontend Dockerfile (Vite Dev)
│ └── .dockerignore
│
├── package.json
├── tsconfig.json
├── vite.config.ts
├── tailwind.config.js
└── docker-compose.yml # Dev setup with hot reload



```

---

## 🚀 Getting Started (Dev Setup)

### 🔧 Prerequisites

- Docker & Docker Compose installed
- Python 3.10+ (for local backend)
- Node.js 18+ (for frontend)

---

### 🐳 Start Using Docker Compose

```bash
docker-compose up --build
```

Runs:
- Flask API at `http://localhost:5000`
- React frontend at `http://localhost:5173`

---

### 🧪 Manual Setup (without Docker)

#### 1. Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate        # or venv\Scripts\activate on Windows
pip install -r requirements.txt
python -m spacy download en_core_web_sm
python app.py
```

#### 2. Frontend

```bash
cd src
npm install
npm run dev
```

---

## 🔧 Backend Guide (Flask)

### 🔗 API Routes

| Route                     | Method | Description                              |
|--------------------------|--------|------------------------------------------|
| `/`                      | GET    | Health check                             |
| `/api/providers`         | GET    | All providers                            |
| `/config`                | GET    |Get the latest brand logo config                     |
| `/config`                |POST, PUT    | Create or update brand logo config       |

---

## 🎨 Frontend Guide (React + Vite)

### 🔧 Components

| File                         | Role                             |
|-----------------------------|----------------------------------|
| `SearchBar.tsx`             | Search input bar                 |
| `ProviderCard.tsx`          | Display provider summary         |
| `ProviderProfile.tsx`       | Full provider details            |
| `FilterSidebar.tsx`         | Search filters                   |
| `useProviderSearch.ts`      | Hook for calling backend search  |


## 🎨 Tailwind Configuration

Tailwind CSS is already integrated with **Vite + React**.

---

### 1️⃣ `tailwind.config.js`

```js
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {
      colors: {
        primary: '#0ea5e9',  // Sky blue for healthcare branding
        secondary: '#10b981', // Green accents
      },
      borderRadius: {
        '2xl': '1rem',
      },
    },
  },
  plugins: [],
}
```

### 2️⃣ `index.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

/* Custom smooth transitions */
* {
  @apply transition-all duration-200;
}
```

## 🧪 Running Locally

```bash
cd src
npm run dev
```

Frontend runs on:  
📍 `http://localhost:5173`

```bash
cd backend
python app.py
```

Backend runs on:  
📍 `http://localhost:5000`



---

## 🐳 Docker Guide

### docker-compose.yml Highlights

```yaml
services:
  backend:
    build: ./backend
    ports:
      - "5000:5000"
  frontend:
    build: ./src
    ports:
      - "5173:5173"
```

### Run All Services

```bash
docker-compose up --build
```

---

## ⚙️ Environment Configuration

### 🔧 `backend/config.py`

```python
import os
SQLALCHEMY_DATABASE_URI = 'postgresql://<username>:<password>@localhost/<dbname>'
SQLALCHEMY_TRACK_MODIFICATIONS = False

```








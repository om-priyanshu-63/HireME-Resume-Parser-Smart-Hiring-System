# HireME — Resume Parser & Smart Hiring System

> 🤖 AI-powered full-stack resume parsing, job matching, and candidate management system for HR professionals.

---

## 🚀 Quick Start

### Prerequisites
- Python 3.9+ installed
- pip package manager
- **MongoDB** installed and running on `localhost:27017`
  - [Download MongoDB Community](https://www.mongodb.com/try/download/community)

### Option 1 — Double-click to run
```
Double-click: setup_and_run.bat
```

### Option 2 — Manual setup
```bash
cd backend
python -m venv venv
venv\Scripts\activate.bat          # Windows
# source venv/bin/activate         # Mac/Linux

pip install -r requirements.txt
python -m spacy download en_core_web_sm

python app.py
```

Then open: **http://localhost:5000**

**Default login:** `admin` / `admin123`

---

## 🏗️ Project Structure

```
Resume Parser/
├── backend/
│   ├── app.py              # Flask entry point
│   ├── config.py           # Configuration (MongoDB URI)
│   ├── requirements.txt    # Python dependencies
│   ├── models/
│   │   └── database.py     # MongoDB data access layer (User, Job, Resume)
│   ├── routes/
│   │   ├── auth.py         # Login / Register / Logout
│   │   ├── resume.py       # Upload / Parse / Match / Export
│   │   ├── jobs.py         # Job CRUD
│   │   └── analytics.py    # Dashboard data (aggregation pipelines)
│   ├── services/
│   │   ├── parser.py       # NLP resume parsing
│   │   ├── matcher.py      # TF-IDF matching
│   │   └── exporter.py     # CSV / Excel export
│   └── uploads/            # Uploaded resume files
├── frontend/
│   ├── index.html          # Main SPA
│   ├── login.html          # Login page
│   ├── css/main.css        # Design system
│   └── js/
│       ├── app.js          # Application logic
│       ├── api.js          # API layer
│       ├── charts.js       # Chart.js visualizations
│       └── upload.js       # Drag & drop upload
├── setup_and_run.bat       # One-click Windows setup
└── README.md
```

---

## ✨ Features

### 📄 Resume Parsing
- Supports **PDF**, **DOCX**, and **TXT** formats
- Extracts: Name, Email, Phone, Skills, Education, Experience
- Uses **spaCy NLP** + regex for entity extraction
- 100+ technical skills recognized

### 🎯 Job Matching
- **TF-IDF + Cosine Similarity** for text matching (40% weight)
- **Skill overlap** comparison (45% weight)
- **Experience** validation (15% weight)
- Returns 0–100% composite match score

### 📊 Dashboard
- Hiring funnel visualization
- Score distribution chart
- Top skills bar chart
- Candidate status doughnut chart

### 👥 Candidate Management
- Sort by name, score, experience
- Filter by job, status, score range
- Search by name or email
- One-click shortlist / reject / reset

### 📈 Analytics
- Per-job average scores
- Top skills distribution
- Hiring funnel stages
- Shortlisted vs rejected stats

### 📤 Export
- Export to **CSV** or **Excel** (styled)
- Filter by job or status before export

### 💡 Resume Suggestions
- Missing sections detector
- Skill gap analysis vs job requirements
- Keyword and formatting tips

---

## 🔧 Tech Stack

| Layer | Technology |
|-------|-----------|
| Backend | Python Flask 3.0 |
| NLP | spaCy, NLTK |
| ML | scikit-learn (TF-IDF + Cosine Similarity) |
| PDF | pdfplumber + PyMuPDF |
| DOCX | python-docx |
| **Database** | **MongoDB via PyMongo** |
| Frontend | HTML5 + CSS3 + Vanilla JS |
| Charts | Chart.js 4 |
| Export | openpyxl |
| Auth | Flask-Login + Werkzeug |

---

## 🗄️ MongoDB Collections

| Collection | Description |
|-----------|-------------|
| `users` | User accounts (admin/hr) |
| `jobs` | Job descriptions with required skills |
| `resumes` | Parsed resume data with match scores |
| `counters` | Auto-increment ID sequences |

### Environment Variables (optional)

| Variable | Default | Description |
|----------|---------|-------------|
| `MONGO_URI` | `mongodb://localhost:27017/` | MongoDB connection string |
| `MONGO_DB_NAME` | `hireme_db` | Database name |
| `SECRET_KEY` | *(built-in)* | Flask session secret |

---

## 🔐 API Reference

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/login` | Login |
| POST | `/api/auth/register` | Register |
| POST | `/api/auth/logout` | Logout |
| GET  | `/api/jobs/` | List all jobs |
| POST | `/api/jobs/` | Create job |
| POST | `/api/resumes/upload` | Upload & parse resumes |
| GET  | `/api/resumes/` | List resumes (with filters) |
| PUT  | `/api/resumes/:id/status` | Update candidate status |
| GET  | `/api/resumes/export/csv` | Export as CSV |
| GET  | `/api/resumes/export/excel` | Export as Excel |
| GET  | `/api/analytics/summary` | Dashboard summary |
| GET  | `/api/analytics/score-distribution` | Score buckets |
| GET  | `/api/analytics/top-skills` | Most common skills |
| GET  | `/api/analytics/hiring-funnel` | Funnel stages |
| GET  | `/api/analytics/score-by-job` | Per-job stats |
| POST | `/api/seed-demo` | Seed demo data |

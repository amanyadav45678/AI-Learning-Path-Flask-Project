# 🎓 AI Learning Path — Flask Project

> **An intelligent, role-based e-learning platform** powered by Google Gemini AI and Firebase. Built for students and teachers with personalized quizzes, AI chatbot, learning path generation, and smart note analysis.

**Team:** Aman Kumar · Anshita Goel · Darpan Yaduvanshi  
**Institution:** UIC | **Mentor:** Mrs. Ashima Sood

---

## 📑 Table of Contents

1. [📖 Project Overview](#-project-overview)
2. [✨ Features](#-features)
3. [🏗️ Project Structure](#️-project-structure)
4. [⚙️ Setup & Installation](#️-setup--installation)
5. [🔐 Environment Configuration](#-environment-configuration)
6. [🔑 Authentication Flow](#-authentication-flow)
7. [👨‍🎓 Student Portal](#-student-portal)
8. [👩‍🏫 Teacher Portal](#-teacher-portal)
9. [🤖 AI & Machine Learning](#-ai--machine-learning)
10. [🗄️ Database Models](#️-database-models)
11. [📁 File Reference](#-file-reference)
12. [🌐 API Endpoints](#-api-endpoints)
13. [🧪 Demo Accounts](#-demo-accounts)
14. [⚠️ Common Problems & Fixes](#️-common-problems--fixes)

---

## 📖 Project Overview

**AI Learning Path** is a full-stack Flask web application that creates a personalized learning experience for both students and teachers. The platform uses:

- **Google Gemini AI** (`gemini-1.5-flash`) for dynamic quiz generation, AI chatbot, note analysis, and personalized learning paths.
- **Firebase Authentication** for secure Google Sign-In and phone OTP login.
- **Deep Learning (TensorFlow/Keras)** for skill-level prediction (Beginner → Expert) based on quiz performance.
- **SQLite** (via SQLAlchemy) for fast, local data persistence.
- **Role-Based Access Control** separating the student and teacher experiences completely.

---

## ✨ Features

### For Students 👨‍🎓
| Feature | Description |
|---|---|
| 🏠 **Dashboard** | Overview of scores, skill level, badges, and weak topics |
| 📚 **Subjects** | Browse available subjects filtered by class level |
| 🧪 **AI Quiz** | AI-generated MCQs (5 questions) per subject, class-level adjusted |
| 🗺️ **Learning Path** | AI-personalized step-by-step learning plan based on quiz scores |
| 📝 **Notes** | Upload notes (text files); AI summarizes and gives study tips |
| 💬 **AI Chatbot** | Ask any subject-specific doubt; Gemini AI answers step-by-step |
| 👤 **Profile** | View all quiz history, earned badges, and skill progression |

### For Teachers 👩‍🏫
| Feature | Description |
|---|---|
| 🏠 **Dashboard** | Overview of class performance metrics and teaching analytics |
| 🧑‍🤝‍🧑 **Students** | View and manage enrolled students |
| 🧪 **Quiz Manager** | View, review, and AI-auto-generate quizzes per subject |
| 📊 **Reports** | Student performance reports |
| 💬 **AI Chatbot** | Subject-specific AI assistant with teacher-mode context |
| 👤 **Profile** | Teacher profile with performance stats and badges |

### Platform-Wide 🌐
- 🔐 Email/Password login + Google Sign-In (Firebase)
- 🏅 Badge/Achievement system (Quiz Starter, Quiz Warrior, Perfect Score, etc.)
- 📈 Skill-level detection (Beginner / Intermediate / Advanced / Expert) via neural network
- 🔄 Automatic learning path updates after every quiz attempt

---

## 🏗️ Project Structure

```
ai-learning-flask/
│
├── 📄 app.py                        ← Main Flask application (all routes & blueprints)
├── 📄 genai_api.py                  ← Google Gemini AI integrations
├── 📄 firebase_init.py              ← Firebase Admin SDK initialization
├── 📄 models.py                     ← Top-level models (legacy)
├── 📄 requirements.txt              ← Python dependencies
├── 📄 .env.example                  ← Environment variable template
├── 📄 serviceAccountKey.json        ← Firebase Admin credentials (DO NOT COMMIT)
│
├── 📂 database/
│   ├── 📄 __init__.py
│   ├── 📄 models.py                 ← SQLAlchemy database models (User, Quiz, Notes, etc.)
│   └── 📄 seed_data.py              ← Pre-seeded questions, subjects & class levels
│
├── 📂 ml/
│   ├── 📄 __init__.py
│   └── 📄 deep_model.py             ← TensorFlow neural network (skill level prediction)
│
├── 📂 model/
│   └── 📄 skill_model.h5            ← Trained Keras model (auto-generated on first run)
│
├── 📂 templates/
│   ├── 📄 base.html                 ← Base layout template
│   ├── 📄 login.html                ← Login + Signup page (with Firebase Google Login)
│   ├── 📄 macros.html               ← Reusable Jinja2 macro components
│   │
│   ├── 📂 student/
│   │   ├── 📄 student_dashboard.html
│   │   ├── 📄 student_subjects.html
│   │   ├── 📄 student_quiz.html
│   │   ├── 📄 student_path.html
│   │   ├── 📄 student_notes.html
│   │   ├── 📄 student_chatbot.html
│   │   └── 📄 student_profile.html
│   │
│   └── 📂 teacher/
│       ├── 📄 teacher_dashboard.html
│       ├── 📄 teacher_students.html
│       ├── 📄 teacher_quiz.html
│       ├── 📄 teacher_reports.html
│       ├── 📄 teacher_chatbot.html
│       └── 📄 teacher_profile.html
│
├── 📂 static/
│   └── 📂 css/
│       └── 📄 style.css             ← Global stylesheet
│
└── 📂 instance/
    └── 📄 ai_learning.db            ← SQLite database (auto-created on first run)
```

---

## ⚙️ Setup & Installation

### Prerequisites
- Python 3.9 or higher
- `pip` package manager
- A Google Gemini API key → [Get yours here](https://aistudio.google.com/app/apikey)
- (Optional) Firebase project for Google Login → [Firebase Console](https://console.firebase.google.com/)

### Step 1 — Clone / Open the project
```bash
cd ai-learning-flask
```

### Step 2 — Create a virtual environment (recommended)
```bash
python -m venv .venv

# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate
```

### Step 3 — Install all dependencies
```bash
pip install -r requirements.txt
```

> 📦 See [`requirements.txt`](requirements.txt) for the full package list.

### Step 4 — Configure environment variables
```bash
# Copy the template
copy .env.example .env    # Windows
cp .env.example .env      # macOS/Linux

# Open .env and set your keys (see Environment Configuration below)
```

### Step 5 — Run the application
```bash
python app.py
```

### Step 6 — Open in browser
```
http://localhost:5000
```

> ✅ The SQLite database `instance/ai_learning.db` is **auto-created** on first run. You don't need to run any migration commands.

---

## 🔐 Environment Configuration

Copy [`.env.example`](.env.example) to `.env` and fill in your values:

```env
# Flask security key — change this to a long random string
SECRET_KEY=change-this-to-a-random-secret-key

# Google Gemini API Key — required for AI features
GEMINI_API_KEY=your-gemini-api-key-here

# Firebase config is handled in:
#   → login.html (JavaScript / client-side Firebase SDK)
#   → serviceAccountKey.json (Python / server-side Firebase Admin SDK)
```

| Variable | Required | Description |
|---|---|---|
| `SECRET_KEY` | ✅ Yes | Flask session security key |
| `GEMINI_API_KEY` | ✅ For AI features | Powers chatbot, quiz gen, notes analysis |
| `serviceAccountKey.json` | ✅ For Google Login | Firebase Admin SDK credentials file |

> ⚠️ **Never commit** `.env` or `serviceAccountKey.json` to a public repository. Add them to `.gitignore`.

---

## 🔑 Authentication Flow

The app supports two login methods:

### Method 1: Email & Password
```
User fills login form
        ↓
POST /login → app.py checks email + password hash in DB
        ↓
user.role == 'student' → redirect to /student/dashboard
user.role == 'teacher' → redirect to /teacher/dashboard
```

### Method 2: Google Sign-In (Firebase)
```
User clicks "Continue with Google"
        ↓
Firebase JS SDK opens Google popup → gets ID token
        ↓
POST /firebase-login → server checks if user exists in DB
        ↓
New user? → needs_info: true → show onboarding form (name, role, class)
        ↓
POST /firebase-register → create/update user in DB → login_user()
        ↓
redirect to /student/dashboard or /teacher/dashboard
```

### Role-Based Access Control
Each portal has a `before_request` guard that prevents cross-role access:

```python
# In student blueprint (app.py)
@student_bp.before_request
def student_auth():
    if not current_user.is_authenticated:
        return redirect(url_for('login'))
    if current_user.role != 'student':
        return redirect(url_for('teacher.dashboard'))
```

---

## 👨‍🎓 Student Portal

All student routes are registered under the `/student` URL prefix via a Flask Blueprint.

| Page | URL | Template File |
|---|---|---|
| Dashboard | `/student/dashboard` | [`student_dashboard.html`](templates/student/student_dashboard.html) |
| Subjects | `/student/subjects` | [`student_subjects.html`](templates/student/student_subjects.html) |
| Take Quiz | `/student/quiz/<subject>` | [`student_quiz.html`](templates/student/student_quiz.html) |
| Learning Path | `/student/path` | [`student_path.html`](templates/student/student_path.html) |
| Notes | `/student/notes` | [`student_notes.html`](templates/student/student_notes.html) |
| AI Chatbot | `/student/chatbot` | [`student_chatbot.html`](templates/student/student_chatbot.html) |
| Profile | `/student/profile` | [`student_profile.html`](templates/student/student_profile.html) |

---

## 👩‍🏫 Teacher Portal

All teacher routes are registered under the `/teacher` URL prefix via a Flask Blueprint.

| Page | URL | Template File |
|---|---|---|
| Dashboard | `/teacher/dashboard` | [`teacher_dashboard.html`](templates/teacher/teacher_dashboard.html) |
| Students | `/teacher/students` | [`teacher_students.html`](templates/teacher/teacher_students.html) |
| Quiz Manager | `/teacher/quiz/<subject>` | [`teacher_quiz.html`](templates/teacher/teacher_quiz.html) |
| Reports | `/teacher/reports` | [`teacher_reports.html`](templates/teacher/teacher_reports.html) |
| AI Chatbot | `/teacher/chatbot` | [`teacher_chatbot.html`](templates/teacher/teacher_chatbot.html) |
| Profile | `/teacher/profile` | [`teacher_profile.html`](templates/teacher/teacher_profile.html) |

---

## 🤖 AI & Machine Learning

### Google Gemini AI — [`genai_api.py`](genai_api.py)

All AI calls go through this module using `google-generativeai` with the `gemini-1.5-flash` model.

| Function | Purpose |
|---|---|
| `chatbot_reply_api(message, subject, role)` | Returns a step-by-step answer from Gemini for a student/teacher question |
| `generate_quiz_api(subject, class_level)` | Auto-generates 5 MCQs as a JSON array, difficulty-adjusted by class level |
| `analyze_notes_api(content)` | Summarizes uploaded notes and provides study tips |
| `generate_learning_path_ai(scores, class_level)` | Creates a personalized, prioritized learning plan |
| `call_general_ai(prompt, system)` | General-purpose Gemini API call used internally |

### Deep Learning Skill Predictor — [`ml/deep_model.py`](ml/deep_model.py)

A TensorFlow/Keras neural network that classifies a student's overall skill level.

```
Architecture:
  Input (6 subject scores)
      → Dense(64, ReLU) + BatchNorm + Dropout(0.3)
      → Dense(128, ReLU) + BatchNorm + Dropout(0.3)
      → Dense(64, ReLU)
      → Dense(32, ReLU)
      → Dense(4, Softmax)  ← Beginner / Intermediate / Advanced / Expert
```

| Function | Purpose |
|---|---|
| `predict_skill_level(scores_dict)` | Returns level name, confidence %, and probability for all 4 levels |
| `analyze_skills(quiz_results)` | Averages quiz scores per subject into a scores dictionary |
| `generate_learning_path(scores)` | Rule-based fallback path generator (used if AI call fails) |
| `calculate_points(quiz_results)` | Points system: 100pts (≥90%), 70pts (≥75%), 40pts (≥60%), 10pts (below) |
| `get_level_from_points(points)` | Maps points → Beginner/Intermediate/Advanced/Expert level label |
| `check_badges(quiz_results, existing)` | Awards achievement badges based on activity milestones |
| `train_and_save()` | Trains the model on synthetic data and saves to `model/skill_model.h5` |

> 🔄 If TensorFlow is not installed or no model file exists, the system automatically falls back to a simple rule-based skill predictor.

### Badge System 🏅

| Badge | Trigger |
|---|---|
| 🎯 Quiz Starter | Complete your first quiz |
| ⚔️ Quiz Warrior | Complete 5 quizzes |
| 🏆 Quiz Master | Complete 10 quizzes |
| 💯 Perfect Score | Score 100% on any quiz |
| 🌟 Tri-Master | Score ≥ 80% in 3 different subjects |

---

## 🗄️ Database Models

Defined in [`database/models.py`](database/models.py). The SQLite database is auto-created at `instance/ai_learning.db`.

### `User` Table
| Column | Type | Description |
|---|---|---|
| `id` | Integer (PK) | Auto-increment primary key |
| `name` | String(100) | Full name |
| `email` | String(120) | Unique email address |
| `password_hash` | String(200) | Werkzeug hashed password |
| `role` | String(10) | `'student'` or `'teacher'` |
| `subject` | String(100) | Teacher's subject specialty |
| `class_level` | String | Student's class (e.g. `Class 8`) |
| `points` | Integer | Accumulated gamification points |
| `level` | String(20) | Skill level label |
| `firebase_uid` | String(200) | Firebase UID for Google login |
| `created_at` | DateTime | Account creation timestamp |

### Other Tables
| Model | Table | Description |
|---|---|---|
| `QuizResult` | `quiz_results` | Stores score, total, percentage, and weak topics per quiz attempt |
| `LearningPath` | `learning_paths` | Stores the JSON learning path for each user (updated after each quiz) |
| `Badge` | `badges` | Achievement records with badge ID, name, and icon |
| `Note` | `notes` | User-uploaded notes with AI analysis |
| `AINote` | `ai_notes` | Cached AI-generated study notes per subject |
| `ChatMessage` | `chat_messages` | Full chatbot conversation history per user |

---

## 📁 File Reference

Quick links to every important file in the project:

### 🐍 Python Files
| File | Purpose |
|---|---|
| [`app.py`](app.py) | Main Flask app: all routes, auth, student blueprint, teacher blueprint |
| [`genai_api.py`](genai_api.py) | Google Gemini AI wrapper functions |
| [`firebase_init.py`](firebase_init.py) | Firebase Admin SDK setup and token verification |
| [`database/models.py`](database/models.py) | SQLAlchemy ORM models for all database tables |
| [`database/seed_data.py`](database/seed_data.py) | Pre-seeded quiz questions, subject list, and class-level mappings |
| [`ml/deep_model.py`](ml/deep_model.py) | Deep learning model: build, train, predict, badges, points |
| [`models.py`](models.py) | Legacy top-level models file (kept for reference) |
| [`fix_links.py`](fix_links.py) | Utility script to repair broken template links |
| [`fix_student_links.py`](fix_student_links.py) | Utility script to repair broken student template links |

### 🌐 HTML Templates
| File | Route It Serves |
|---|---|
| [`templates/login.html`](templates/login.html) | `/login` and `/signup` |
| [`templates/base.html`](templates/base.html) | Base layout inherited by all pages |
| [`templates/macros.html`](templates/macros.html) | Reusable Jinja2 component macros |
| [`templates/student/student_dashboard.html`](templates/student/student_dashboard.html) | `/student/dashboard` |
| [`templates/student/student_subjects.html`](templates/student/student_subjects.html) | `/student/subjects` |
| [`templates/student/student_quiz.html`](templates/student/student_quiz.html) | `/student/quiz/<subject>` |
| [`templates/student/student_path.html`](templates/student/student_path.html) | `/student/path` |
| [`templates/student/student_notes.html`](templates/student/student_notes.html) | `/student/notes` |
| [`templates/student/student_chatbot.html`](templates/student/student_chatbot.html) | `/student/chatbot` |
| [`templates/student/student_profile.html`](templates/student/student_profile.html) | `/student/profile` |
| [`templates/teacher/teacher_dashboard.html`](templates/teacher/teacher_dashboard.html) | `/teacher/dashboard` |
| [`templates/teacher/teacher_students.html`](templates/teacher/teacher_students.html) | `/teacher/students` |
| [`templates/teacher/teacher_quiz.html`](templates/teacher/teacher_quiz.html) | `/teacher/quiz/<subject>` |
| [`templates/teacher/teacher_reports.html`](templates/teacher/teacher_reports.html) | `/teacher/reports` |
| [`templates/teacher/teacher_chatbot.html`](templates/teacher/teacher_chatbot.html) | `/teacher/chatbot` |
| [`templates/teacher/teacher_profile.html`](templates/teacher/teacher_profile.html) | `/teacher/profile` |

### ⚙️ Config & Other Files
| File | Purpose |
|---|---|
| [`requirements.txt`](requirements.txt) | All Python package dependencies |
| [`.env.example`](.env.example) | Template for environment variable configuration |
| [`serviceAccountKey.json`](serviceAccountKey.json) | Firebase Admin credentials *(keep secret!)* |
| [`static/css/style.css`](static/css/style.css) | Global CSS styles |

---

## 🌐 API Endpoints

### Auth Endpoints
| Method | Endpoint | Description |
|---|---|---|
| `GET/POST` | `/login` | Email/password login |
| `GET` | `/signup` | Signup page |
| `POST` | `/register` | Create new user account |
| `POST` | `/firebase-login` | Google Sign-In (Firebase token check) |
| `POST` | `/firebase-register` | Complete onboarding for new Google users |
| `GET` | `/logout` | Log out current user |

### Student API Endpoints
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/student/api/generate-quiz?subject=X` | Fetch 5 AI-generated MCQs for subject X |
| `POST` | `/student/quiz/submit` | Submit quiz results, update progress & badges |
| `GET` | `/student/ai-notes/<subject>` | Fetch AI-generated study notes (cached) |
| `POST` | `/student/chatbot/send` | Send a message to the AI chatbot |

### Teacher API Endpoints
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/teacher/quiz/submit` | Submit teacher quiz attempt results |
| `GET` | `/teacher/ai-notes/<subject>` | Fetch AI-generated notes for a subject |
| `POST` | `/teacher/chatbot/send` | Send a message to the AI chatbot (teacher mode) |

---

## 🧪 Demo Accounts

You can create accounts through the signup form. For quick testing, register with these roles:

| Role | Signup as | Required Fields |
|---|---|---|
| 👨‍🎓 Student | Select **Student** role | Name, Email, Password, Class Level |
| 👩‍🏫 Teacher | Select **Teacher** role | Name, Email, Password, Subject |

> 💡 After signing up, the system auto-creates the database and immediately logs you into your role-specific dashboard.

---

## ⚠️ Common Problems & Fixes

| Problem | Root Cause | Fix |
|---|---|---|
| `ModuleNotFoundError: flask` | Dependencies not installed | Run `pip install -r requirements.txt` |
| Login page loops / doesn't redirect | Blueprint route name wrong | Check `url_for('student.dashboard')` in `app.py` |
| Teacher sees student dashboard | Role check missing | Verify `before_request` guard in teacher blueprint |
| AI chatbot returns "Add Gemini API key" | Missing API key | Set `GEMINI_API_KEY` in `genai_api.py` or `.env` |
| Google login fails with "unauthorized-domain" | Firebase domain not whitelisted | Add `localhost` to Firebase Console → Auth → Authorized Domains |
| `serviceAccountKey.json not found` | File missing or wrong path | Place the file in the same folder as `firebase_init.py` |
| DB errors on startup | Corrupt or outdated schema | Delete `instance/ai_learning.db` and restart `python app.py` |
| Quiz shows hardcoded questions | Gemini AI call failed | Check internet connection and verify Gemini API key is valid |
| TensorFlow not available warning | TF not installed | Install via `pip install tensorflow==2.16.1` or ignore (rule-based fallback runs automatically) |

---

## 🔧 Tech Stack Summary

| Layer | Technology |
|---|---|
| **Backend** | Python 3.x + Flask 3.0 |
| **Database** | SQLite via SQLAlchemy (Flask-SQLAlchemy) |
| **Authentication** | Flask-Login + Firebase Admin SDK |
| **AI / LLM** | Google Gemini (`gemini-1.5-flash`) via `google-generativeai` |
| **ML Model** | TensorFlow / Keras (skill level neural network) |
| **Frontend** | Jinja2 HTML templates + Vanilla CSS + JavaScript |
| **Google Login** | Firebase JS SDK (client) + Firebase Admin SDK (server) |

---

*Made with — Aman Yadav*

# ⚡ AI-Powered Maintenance Ticket Prioritization Agent

**Intelligent maintenance triage and dispatch for renewable energy infrastructure**

An end-to-end application that analyzes maintenance tickets, identifies potential failure categories, calculates priority scores, flags safety concerns, and recommends the appropriate engineering team.

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-REST%20API-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![SQLite](https://img.shields.io/badge/Database-SQLite-003B57?logo=sqlite&logoColor=white)](https://www.sqlite.org/)
[![AI](https://img.shields.io/badge/AI-Hybrid%20NLP%20%2B%20Rules-7C3AED)](#-how-the-ai-agent-works)
[![Tests](https://img.shields.io/badge/Testing-Pytest%20%2B%20E2E-2EA44F)](#-testing)

> **The problem:** Renewable energy operators receive maintenance alerts from sensors, SCADA systems, and technician inspections. When these alerts accumulate, critical equipment failures and safety risks can be overlooked.
>
> **The solution:** A centralized, AI-assisted dispatch dashboard that turns maintenance descriptions into actionable, prioritized work items.

**Live Demo:** Add your deployed Railway URL here after deployment.  
**GitHub Repository:** https://github.com/shivasai8009/ai-powered-maintenance-ticket-prioritization-agent

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Key Features](#-key-features)
- [Supported Assets](#-supported-assets)
- [Dashboard Experience](#-dashboard-experience)
- [How the AI Agent Works](#-how-the-ai-agent-works)
- [System Architecture](#-system-architecture)
- [Technology Stack](#-technology-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [API Documentation](#-api-documentation)
- [Testing](#-testing)
- [Evaluation](#-evaluation)
- [Deployment](#-deployment)
- [Engineering Decisions](#-engineering-decisions)
- [Future Improvements](#-future-improvements)
- [Author](#-author)

## 🎯 Project Overview

The AI-Powered Maintenance Ticket Prioritization Agent is a full-stack application built for renewable energy asset management and enterprise maintenance dispatch.

It combines natural language processing (NLP), domain-specific decision rules, priority scoring, and persistent ticket management to help maintenance teams identify which issues need attention first.

Given a maintenance description such as *"Solar inverter temperature is rising and the unit has tripped repeatedly"*, the system analyzes the text and generates a structured triage result containing:

- A predicted maintenance failure category.
- A quantitative priority score from 0 to 100.
- A severity classification.
- A probable root-cause assessment.
- Relevant safety warnings and precautions.
- A recommended engineering team for dispatch.
- A record that can be tracked through its maintenance lifecycle.

The application is designed as a practical demonstration of applied AI engineering, backend development, database persistence, API design, and interactive dashboard development.

## ✨ Key Features

### 🤖 Hybrid AI-Powered Triage

- Uses TF-IDF text vectorization and cosine similarity for text-based classification.
- Combines NLP results with deterministic, domain-specific maintenance rules.
- Generates priority scores using multiple risk factors.
- Identifies probable causes based on the ticket description and configured rules.
- Applies safety-related guardrails for relevant maintenance scenarios.

### 🚦 Multi-Factor Priority Scoring

Each ticket receives a score between 0 and 100 to support maintenance triage.

The configured scoring logic considers factors such as:

- Personnel and equipment safety.
- Potential financial impact.
- Operational downtime.
- Failure severity and urgency.

The score supports consistent prioritization; it is not a guarantee of actual failure probability or a substitute for an engineering risk assessment.

### 🛡️ Safety-Aware Recommendations

The system can flag relevant hazards and precautions, including electrical arc-flash risks and lockout/tagout considerations.

Safety alerts are decision-support recommendations. Actual work must follow applicable regulations, site-specific procedures, and qualified personnel's judgment.

### 🧰 Intelligent Dispatch Recommendations

Maintenance tickets can be routed to a suitable engineering team based on the detected issue and configured domain rules, helping organize work across specialized maintenance groups.

### 📊 Interactive Operations Dashboard

- KPI cards for maintenance workload and priority metrics.
- A centralized maintenance ticket queue.
- Quick filters for ticket categories and asset types.
- Ticket creation through AI-assisted triage.
- Workflow status updates.
- Metrics that reflect the current ticket data.

### 💾 Persistent Ticket Management

- SQLite database for ticket storage.
- CRUD operations for supported ticket workflows.
- Transactional database operations.
- Write-Ahead Logging (WAL) configuration where enabled.
- Automatic initialization and sample-data seeding when the database is empty.

### 🔌 REST API

- FastAPI-powered endpoints.
- JSON request and response handling.
- Interactive Swagger documentation.
- A health-check endpoint.
- API-level tests for key application workflows.

## ⚡ Supported Renewable Energy Assets

| Asset category | Example maintenance scenarios |
|---|---|
| Solar PV arrays | Inverter overheating, PV string faults |
| Wind turbine generators | Gearbox vibration, bearing temperature anomalies |
| Hydroelectric power | Turbine issues, spillway safety concerns |
| Substation and grid operations | Transformer faults, electrical protection alarms |
| Battery energy storage systems (BESS) | Battery temperature anomalies, storage-system alarms |

The application uses a curated dataset and configured rules. These examples describe the intended domain; they do not imply a live connection to real SCADA systems, physical equipment, or industrial control networks.

## 🖥️ Dashboard Experience

The application brings the maintenance workflow into one interface:

1. **Monitor:** Review ticket totals, active work, critical risks, and priority metrics.
2. **Analyze:** Enter or select a maintenance scenario for AI-assisted triage.
3. **Prioritize:** Review the suggested category, score, root cause, and safety warnings.
4. **Dispatch:** Review the recommended maintenance team.
5. **Track:** Save the ticket and update its workflow status from the queue.

The interface is designed to make the most important operational information easy to review without navigating through multiple pages.

> **Add a screenshot here:** Capture your running dashboard and save it as `docs/dashboard.png`. Then replace this note with:
>
> `![Maintenance Operations Dashboard](docs/dashboard.png)`

## 🧠 How the AI Agent Works

The application uses a **hybrid NLP and rule-based approach** rather than relying entirely on an external generative AI service.

### Processing pipeline

```text
Maintenance Ticket Description
              |
              v
       Text Preparation
              |
              v
  TF-IDF Vectorization and
   Cosine Similarity Analysis
              |
              v
   Domain-Specific Rule Engine
              |
              v
 Failure Category and Root Cause
              |
              v
 Priority Scoring and Safety Flags
              |
              v
     Team Recommendation
              |
              v
    Structured Triage Result
              |
              v
     SQLite Ticket Storage
              |
              v
      Dashboard and REST API
```

### Why combine NLP with domain rules?

**NLP provides text similarity.** TF-IDF represents ticket descriptions as numerical features, while cosine similarity compares text representations to help identify relevant failure categories.

**Rules provide explicit decision logic.** Configured rules can account for specific failure keywords, severity indicators, operational consequences, and safety conditions.

**The priority engine supports consistent decisions.** It combines configured risk factors into a score that helps dispatchers compare tickets.

**The backend persists the result.** The triage output can be stored and retrieved through the application's ticket-management workflow.

This design offers a lightweight, explainable alternative to depending entirely on an external LLM API. Its accuracy and safety depend on the quality of the dataset, similarity thresholds, rules, and evaluation process.

## 🏗️ System Architecture

The application follows a straightforward full-stack architecture.

| Layer | Responsibility |
|---|---|
| Frontend | Dashboard rendering, filters, KPI cards, and user interactions |
| FastAPI backend | HTTP routes, request handling, and application orchestration |
| AI triage engine | Text similarity, domain rules, priority scoring, and recommendations |
| Data layer | SQLite persistence, database initialization, and ticket operations |
| Test layer | Unit, API, database, and end-to-end verification |

### Request lifecycle

1. A dispatcher enters or selects a maintenance scenario.
2. The frontend sends a request to the FastAPI backend.
3. The backend invokes the triage logic.
4. The agent returns structured classification and prioritization results.
5. The application stores the ticket when the workflow calls for persistence.
6. The dashboard retrieves ticket data and displays the updated state.

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Python | Application and AI logic |
| FastAPI | Backend framework and REST APIs |
| Uvicorn | ASGI application server |
| scikit-learn / NLP utilities | Text vectorization and similarity analysis, where used by the implementation |
| SQLite | Relational data persistence |
| HTML, CSS, JavaScript | Interactive frontend |
| Pytest | Automated unit and integration testing |
| Git and GitHub | Version control and source-code hosting |
| Railway | Cloud deployment target |

The dependency list in `requirements.txt` is the source of truth for the project's installed Python libraries.

## 📁 Project Structure

```text
ai-powered-maintenance-ticket-prioritization-agent/
│
├── backend/
│   ├── __init__.py
│   ├── agent.py
│   ├── app.py
│   ├── config.py
│   ├── database.py
│   ├── schemas.py
│   └── data/
│       └── dataset_loader.py
│
├── data/
│   └── maintenance_tickets.csv
│
├── frontend/
│   ├── index.html
│   └── renewable_assets.png
│
├── tests/
│   ├── test_agent.py
│   ├── test_api.py
│   └── test_database.py
│
├── .gitignore
├── Procfile
├── requirements.txt
├── e2e_test.py
├── README.md
├── candidate_task.md
├── case_study.html
├── evaluation_rubric.md
└── submission_instructions.md
```

### Important modules

- `backend/agent.py` — core triage and prioritization logic.
- `backend/app.py` — FastAPI application and HTTP endpoints.
- `backend/config.py` — application configuration and database path.
- `backend/database.py` — SQLite database initialization and data operations.
- `backend/schemas.py` — request and response schemas.
- `backend/data/dataset_loader.py` — dataset loading utilities.
- `frontend/index.html` — dashboard interface.
- `data/maintenance_tickets.csv` — curated maintenance-ticket dataset.
- `tests/` — automated tests for agent logic, API routes, and database behavior.

## 🚀 Getting Started

### Prerequisites

- Python 3.10 or newer.
- Visual Studio Code or another Python-compatible editor.
- Git.
- A terminal such as PowerShell or Command Prompt.

### 1. Clone the repository

```bash
git clone https://github.com/shivasai8009/ai-powered-maintenance-ticket-prioritization-agent.git
cd ai-powered-maintenance-ticket-prioritization-agent
```

### 2. Create a virtual environment

**Windows PowerShell:**

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks environment activation, run the following in the current terminal session and retry:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

**Alternative — Windows Command Prompt:**

```bat
python -m venv .venv
.venv\Scripts\activate.bat
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Start the application

```bash
python -m uvicorn backend.app:app --host 127.0.0.1 --port 8000 --reload
```

### 5. Open the application

| Resource | URL |
|---|---|
| Dashboard | http://127.0.0.1:8000/ |
| Health check | http://127.0.0.1:8000/api/health |
| Swagger API documentation | http://127.0.0.1:8000/docs |
| ReDoc API documentation | http://127.0.0.1:8000/redoc |

Keep the terminal running while using the application. Press `Ctrl + C` to stop the development server.

> **Note:** The documented `.venv312` environment from an earlier local setup is machine-specific. Creating `.venv` as shown above is a portable option for a fresh installation.

## 🔌 API Documentation

FastAPI generates interactive API documentation from the registered application routes.

Open `http://127.0.0.1:8000/docs` after starting the application to inspect available endpoints, schemas, and supported operations.

Key endpoints include:

| Endpoint | Purpose |
|---|---|
| `GET /api/health` | Check application health |
| `GET /api/metrics` | Retrieve dashboard metrics |
| `GET /api/evaluation` | Retrieve available evaluation information |
| `/api/tickets...` | Ticket operations registered by the application |

The ticket endpoint family may include listing, creation, filtering, and workflow updates, depending on the routes implemented in `backend/app.py`.

## 🧪 Testing

Automated tests help verify the triage engine, database operations, and HTTP workflows.

Run the unit and integration tests:

```bash
python -m pytest tests/ -v
```

Run the end-to-end test script:

```bash
python e2e_test.py
```

The current project notes report:

- **13 pytest tests** covering agent logic, API behavior, and database functionality.
- **28 end-to-end checks** covering application workflows and API behavior.

These are the reported expected results, not a guarantee that every environment or future code change will produce the same outcome. Run both commands locally before presenting the results as verified.

## 📈 Model Evaluation

The project includes a curated benchmark dataset at `data/maintenance_tickets.csv`.

The current project notes report the following evaluation figures:

| Metric | Reported result |
|---|---:|
| Category classification accuracy | 100% (6 of 6 cases) |
| Severity classification accuracy | 83.3% (5 of 6 cases) |
| Inference latency | Under 45 ms per ticket |

### Interpreting the results

These figures describe a small benchmark, not broad real-world validation. A six-case evaluation is useful for an initial functional check but is insufficient to establish production-grade classification accuracy.

Latency depends on the environment, dataset, and measurement method. A reproducible performance claim should document the hardware, warm-up procedure, number of runs, and whether timing includes database and HTTP overhead.

Future evaluation should include a larger labeled dataset, per-category precision and recall, a confusion matrix, false-negative analysis for critical hazards, and performance testing under concurrent requests.

## ☁️ Deployment on Railway

The repository includes a `Procfile` for launching the FastAPI application:

```text
web: uvicorn backend.app:app --host 0.0.0.0 --port $PORT
```

### Deployment steps

1. Push the repository to GitHub.
2. Sign in to [Railway](https://railway.app/).
3. Create a new project and deploy from the GitHub repository.
4. Review the build and deployment logs.
5. Generate a public domain in the service's Networking settings.
6. Test the dashboard and health-check endpoint using the public URL.

For example:

```text
https://YOUR-RAILWAY-DOMAIN/
https://YOUR-RAILWAY-DOMAIN/api/health
https://YOUR-RAILWAY-DOMAIN/docs
```

Replace `YOUR-RAILWAY-DOMAIN` with the actual domain assigned to your service.

### Database persistence

SQLite is convenient for a self-contained demonstration, but a database file stored on an ephemeral deployment filesystem may be lost when the service is redeployed or its instance is replaced.

For persistent SQLite storage on Railway:

1. Add a persistent volume to the service and mount it at `/data`.
2. Configure the environment variable:

```text
DB_PATH=/data/maintenance.db
```

3. Confirm that `backend/config.py` reads `DB_PATH` from the environment.
4. Redeploy and verify that newly created tickets survive a restart.

A volume does not automatically redirect SQLite to the mounted directory. The database path must be configured explicitly. For a larger production deployment requiring multiple application instances, consider a managed PostgreSQL database.

## 💡 Engineering Decisions

### 1. Hybrid NLP instead of relying entirely on an LLM

TF-IDF similarity and explicit rules can run locally without requiring an external generative AI API. This reduces external service dependencies and makes the decision logic easier to inspect, although classification quality depends on the implementation and dataset.

### 2. SQLite for a lightweight prototype

SQLite avoids the need to provision a separate database server for local development. WAL mode, where configured, can improve reader/writer concurrency, but it does not eliminate SQLite's write-concurrency limitations.

### 3. FastAPI for backend development

FastAPI provides request validation, JSON serialization, and interactive API documentation, helping keep API behavior clear and testable.

### 4. A centralized dashboard for dispatch

The dashboard places workload metrics, ticket triage, and workflow tracking in one interface, making it easier to demonstrate the complete maintenance lifecycle.

### 5. Automated tests for confidence

Unit, integration, and end-to-end checks help catch regressions across the AI logic, persistence layer, and API. Passing tests increases confidence in tested behavior but does not prove the absence of defects.

## 🔮 Future Improvements

- Expand and validate the labeled maintenance-ticket dataset.
- Add per-category precision, recall, F1-score, and confusion-matrix reporting.
- Integrate real SCADA or IoT data through secure, authorized interfaces.
- Add role-based authentication and audit trails.
- Add structured logging, monitoring, and alerting.
- Introduce a managed relational database for larger deployments.
- Add confidence scores and a dispatcher review workflow for uncertain classifications.
- Benchmark inference latency and API throughput under realistic workloads.
- Add CI automation for tests and deployment checks.

## 👨‍💻 Author

**Shivasai Ankathi**

Full-Stack Developer | Python | Java | REST APIs | SQL | Applied AI

- **GitHub:** [shivasai8009](https://github.com/shivasai8009)
- **Project Repository:** [AI-Powered Maintenance Ticket Prioritization Agent](https://github.com/shivasai8009/ai-powered-maintenance-ticket-prioritization-agent)
- **LinkedIn:** [Connect on LinkedIn](https://www.linkedin.com/in/shivasai-ankathi/)

---

*Built as an applied AI and full-stack engineering project exploring intelligent maintenance triage, safety-aware decision support, and operational workflow management.*

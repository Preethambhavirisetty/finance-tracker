# 💰 Finance Tracker

![React](https://img.shields.io/badge/React_18-20232A?logo=react&logoColor=61DAFB)
![Flask](https://img.shields.io/badge/Flask_3-000000?logo=flask&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![CI](https://github.com/Preethambhavirisetty/finance-tracker/actions/workflows/ci.yml/badge.svg)

A personal finance tracker with user accounts, multiple finance profiles per user, and dashboards for income, expenses, budgets and categories.

## Features
- Register/login with hashed passwords and session-based auth
- Multiple profiles per user, each with its own transactions
- Income/expense tracking with categories, tags and accounts
- Budgets manager and category breakdown on the dashboard
- Stats cards with running balances and a filterable transaction list
- Docker Compose stack (frontend on nginx, Flask backend, Postgres) plus `make` helpers for backups and restores

## Screenshot
<!-- Add a dashboard screenshot: docs/screenshot.png -->
![Dashboard](docs/screenshot.png)

## Tech stack
| Layer | Tech |
|---|---|
| Frontend | React 18 (Create React App), React Router 6, Tailwind CSS, lucide-react |
| Backend | Flask 3, Flask-SQLAlchemy, Flask-CORS, gunicorn |
| Database | SQLite (dev) / PostgreSQL (Docker/production) |
| Ops | Docker, docker-compose, GitHub Actions, Render (`render.yaml`), EC2 scripts |

## Project structure
```
.
├── backend/            # Flask app (app.py, auth.py), Dockerfile, Procfile, requirements.txt
├── frontend/
│   ├── src/components/ # auth, dashboard, profile, settings, layout
│   ├── src/context/    # AuthContext
│   ├── src/utils/      # api client, validation
│   └── Dockerfile, nginx.conf
├── .github/workflows/  # ci.yml, docker-build.yml
├── docker-compose.yml  # db + backend + frontend
├── Makefile            # build/up/down/logs/backup/restore
├── render.yaml         # Render deployment
└── deploy-ec2.sh, start-backend.sh, start-frontend.sh
```

## Getting started

### Option 1: Docker (recommended)
```bash
git clone https://github.com/Preethambhavirisetty/finance-tracker.git
cd finance-tracker
cp env.example .env        # fill in values
make build && make up      # or: docker compose up -d
```
The frontend runs at http://localhost and the API at http://localhost:5001.

### Option 2: Local dev
```bash
# Backend
cd backend
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
python app.py              # http://localhost:5001

# Frontend (new terminal)
cd frontend
cp .env.example .env
npm install
npm start                  # http://localhost:3000
```

## Environment variables
**backend/.env**
| Var | Example | Purpose |
|---|---|---|
| `SECRET_KEY` | random string | Flask session signing |
| `DATABASE_URL` | `sqlite:///finance_tracker.db` | SQLAlchemy URL (Postgres in prod) |
| `FLASK_ENV` | `development` | Flask mode |
| `PORT` | `5001` | API port |
| `CORS_ORIGINS` | `http://localhost:3000` | Allowed origins (comma-separated) |

**frontend/.env**: `REACT_APP_API_URL=http://localhost:5001/api`

> The current README links to `DOCKER-QUICKSTART.md` and `DEPLOYMENT.md`, but neither file is in the repo. Add them or remove the links.

## Contributing
1. Fork the repo and create a branch: `git checkout -b feature/your-change`
2. Commit using [Conventional Commits](https://www.conventionalcommits.org/) (`feat: …`, `fix: …`)
3. Push and open a pull request against `main`

## License
No license file yet. Add one (MIT is a common choice) via **Add file → Create new file → `LICENSE` → Choose a license template**, then update this section.

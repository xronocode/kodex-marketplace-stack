# Kodex — Marketplace Prototype

Open-source marketplace prototype with Agentic Commerce layer.
Built AI-only using GRACE methodology.

## Stack

- Backend: Python 3.12 + FastAPI + SQLAlchemy 2.x async + PostgreSQL 16
- Frontend: Vue 3.5 + TypeScript + Vite + Feature-Sliced Design
- Storage: MinIO (S3-compatible)
- Infra: Docker Compose

## Quick start (single command)

Prerequisites: Docker Desktop, Git

```bash
# 1. Clone all three repos into the same parent directory
git clone <kodex-infra-url>
git clone <kodex-backend-url>
git clone <kodex-frontend-url>

# 2. Enter infra directory
cd kodex-infra

# 3. Copy environment config
cp .env.example .env

# 4. Start the full stack
docker compose up --build
```

Services start in order: PostgreSQL → MinIO → Backend → Frontend.
Wait ~30 seconds for all containers to become healthy.

## Access

| Service | URL |
|---|---|
| Frontend (catalog) | http://localhost:5173 |
| Backend API | http://localhost:8000 |
| API docs (Swagger) | http://localhost:8000/docs |
| Agent context | http://localhost:8000/v1/agent/context |
| llms.txt | http://localhost:8000/llms.txt |
| MinIO console | http://localhost:9001 |

## Seed data

On first run the backend seeds 110 products automatically.
All delivery dates fall within the current week.
Admin credentials are set in `.env` (default: admin / changeme_strong_password).

## Admin panel

Navigate to http://localhost:5173/admin/login
Use credentials from your `.env` file.

## Verify the stack

```bash
curl http://localhost:8000/health
# {"status":"ok","service":"kodex-backend"}

curl http://localhost:8000/v1/public/products?limit=3
# {"items":[...],"next_cursor":"..."}
```

## Shutdown

```bash
docker compose down          # stop containers
docker compose down -v       # stop + remove volumes (resets data)
```

## Repository structure

```
kodex-infra/      ← this repo — Docker Compose entry point
kodex-backend/    ← FastAPI backend
kodex-frontend/   ← Vue 3 frontend
```

## AI-only development

This project was built entirely using AI tools under human engineering
supervision. See `docs/ai/AI_WORKFLOW.md` in each repository for the
full methodology, tool log, and session exports.

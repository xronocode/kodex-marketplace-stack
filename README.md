# Kodex — AI-Ready Marketplace Platform

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Backend: FastAPI](https://img.shields.io/badge/Backend-FastAPI-green.svg)](https://fastapi.tiangolo.com/)
[![Frontend: Vue 3](https://img.shields.io/badge/Frontend-Vue_3-blue.svg)](https://vuejs.org/)
[![AI-Built](https://img.shields.io/badge/Built_With-AI-purple.svg)](https://github.com/xronocode)

> **Open-source marketplace prototype with Agentic Commerce layer**  
> Built entirely using AI tools under human engineering supervision with the **GRACE** methodology

## 🌟 What is Kodex?

Kodex is a **multi-merchant marketplace platform** with an **Agentic Commerce** layer that enables:

- 🛒 **Product Catalog** — Browse 100+ products with infinite scroll
- 🔍 **Natural Language Search** — "Show me cheap laptops delivered tomorrow"
- 🎤 **Voice Search** — Talk to find products (Web Speech API)
- 👨‍💼 **Admin Panel** — Full CRUD for products and offers
- 🤖 **AI-Ready** — Built-in `llms.txt`, agent context, structured capabilities

## 📦 Repository Structure

This is a **monorepo-style** project split into three repositories:

| Repository | Description |
|------------|-------------|
| **[marketplace-stack](https://github.com/xronocode/marketplace-stack)** | 🚀 **Start Here** — Docker Compose entry point |
| **[marketplace-backend](https://github.com/xronocode/marketplace-backend)** | FastAPI backend with async SQLAlchemy |
| **[marketplace-frontend](https://github.com/xronocode/marketplace-frontend)** | Vue 3 + TypeScript frontend (FSD architecture) |

## 🏁 Quick Start (Single Command)

### Prerequisites

- Docker Desktop (or Docker Engine + Docker Compose v2)
- Git

### Run the Full Stack

```bash
# 1. Clone all three repos into the same parent directory
git clone https://github.com/xronocode/marketplace-stack.git
git clone https://github.com/xronocode/marketplace-backend.git
git clone https://github.com/xronocode/marketplace-frontend.git

# 2. Enter the stack directory
cd marketplace-stack

# 3. Copy environment configuration
cp .env.example .env

# 4. Start the full stack
docker compose up --build
```

**Wait ~30 seconds** for all containers to become healthy.

## 🌐 Access Points

| Service | URL | Description |
|---------|-----|-------------|
| **Frontend** | http://localhost:5173 | Main catalog |
| **Backend API** | http://localhost:8000 | REST API |
| **Swagger UI** | http://localhost:8000/docs | Interactive API docs |
| **Agent Context** | http://localhost:8000/v1/agent/context | AI agent capabilities |
| **llms.txt** | http://localhost:8000/llms.txt | Machine-readable manifest |
| **MinIO Console** | http://localhost:9001 | Object storage UI |

**Admin Panel:** http://localhost:5173/admin/login  
**Default Credentials:** `admin` / `changeme_strong_password` (configure in `.env`)

## 🧪 Verify the Stack

```bash
# Health check
curl http://localhost:8000/health
# {"status":"ok","service":"kodex-backend"}

# Get products (cursor pagination)
curl http://localhost:8000/v1/public/products?limit=3
# {"items":[...],"next_cursor":"..."}

# Agent search (natural language)
curl -X POST http://localhost:8000/v1/agent/search \
  -H "Content-Type: application/json" \
  -d '{"query": "cheap laptops delivered tomorrow"}'
```

## 🗄 Seed Data

On first startup, the backend automatically seeds **110 products** with:

- Random names, descriptions, prices
- Dynamic delivery dates (current week only)
- Multiple offers per product
- Product images (stored in MinIO)

## 🛑 Shutdown

```bash
# Stop containers (preserves data)
docker compose down

# Stop + remove volumes (resets everything)
docker compose down -v
```

## 🏗 Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                     Docker Compose Stack                     │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  ┌──────────────────┐         ┌──────────────────┐          │
│  │   Frontend       │         │     Backend      │          │
│  │  Vue 3.5 + TS    │◄───────►│  FastAPI 0.115   │          │
│  │    (Port 5173)   │  HTTP   │    (Port 8000)   │          │
│  └──────────────────┘         └────────┬─────────┘          │
│                                        │                     │
│                              ┌─────────┴─────────┐          │
│                              │                   │          │
│                       ┌──────▼──────┐   ┌───────▼───────┐  │
│                       │  PostgreSQL │   │     MinIO     │  │
│                       │    (5432)   │   │    S3 (9000)  │  │
│                       │   Database  │   │ Object Store  │  │
│                       └─────────────┘   └───────────────┘  │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## 🤖 AI-Ready Features

Kodex is built for **Agentic Commerce** — AI agents can:

1. **Read Capabilities** — `GET /llms.txt` for machine-readable API description
2. **Get Context** — `GET /v1/agent/context` for structured capability JSON
3. **Search Naturally** — `POST /v1/agent/search` with natural language queries

### Example: Agent Search

```bash
curl -X POST http://localhost:8000/v1/agent/search \
  -H "Content-Type: application/json" \
  -d '{
    "query": "laptops under 50000 rubles with delivery this week",
    "filters": {
      "max_price": 50000,
      "delivery_days": 7
    }
  }'
```

## 📚 Documentation

### AI Development Methodology

This project was built using **GRACE** (Graph-RAG Anchored Code Engineering):

- **Contract-First** — Every module has a `MODULE_CONTRACT`
- **Semantic Markup** — `START_BLOCK_*` / `END_BLOCK_*` markers
- **Knowledge Graph** — `docs/knowledge-graph.xml` maps all modules
- **Verification-Driven** — `docs/verification-plan.xml` defines test strategy

See each repository's `docs/ai/` folder for:
- `AI_WORKFLOW.md` — Complete AI development log
- `PROMPTS.md` — Prompt library
- `SESSION_EXPORTS.md` — Cursor session exports

### Technical Documentation

| Document | Backend | Frontend | Stack |
|----------|---------|----------|-------|
| Requirements | [✓](https://github.com/xronocode/marketplace-backend/blob/main/docs/requirements.xml) | [✓](https://github.com/xronocode/marketplace-frontend/blob/main/docs/requirements.xml) | — |
| Technology | [✓](https://github.com/xronocode/marketplace-backend/blob/main/docs/technology.xml) | [✓](https://github.com/xronocode/marketplace-frontend/blob/main/docs/technology.xml) | — |
| Development Plan | [✓](https://github.com/xronocode/marketplace-backend/blob/main/docs/development-plan.xml) | [✓](https://github.com/xronocode/marketplace-frontend/blob/main/docs/development-plan.xml) | — |
| Knowledge Graph | [✓](https://github.com/xronocode/marketplace-backend/blob/main/docs/knowledge-graph.xml) | [✓](https://github.com/xronocode/marketplace-frontend/blob/main/docs/knowledge-graph.xml) | — |
| Verification Plan | [✓](https://github.com/xronocode/marketplace-backend/blob/main/docs/verification-plan.xml) | [✓](https://github.com/xronocode/marketplace-frontend/blob/main/docs/verification-plan.xml) | — |

## 🗺 Roadmap

### Phase 1 (Current) — Core Platform ✅

- [x] Browse catalog with infinite scroll
- [x] Product detail with sortable offers
- [x] Admin JWT authentication
- [x] Admin catalog CRUD with image upload
- [x] Seed script with Faker data
- [x] Agent search with NL parsing

### Phase 2 (Future) — Multi-Merchant

- [ ] Merchant self-service onboarding
- [ ] RBAC for merchant users
- [ ] Merchant-specific dashboards
- [ ] Advanced search (Elasticsearch)
- [ ] Order management
- [ ] Payment integration

### Phase 3 (Future) — Advanced Features

- [ ] Live recommendation engine
- [ ] Analytics dashboard
- [ ] Mobile app (React Native / Flutter)
- [ ] Multi-language support

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

### Why MIT License?

- ✅ **Permissive** — Allows commercial use, modification, and distribution
- ✅ **Simple** — Easy to understand and comply with
- ✅ **Widely Adopted** — Industry standard for open-source software
- ✅ **AI-Friendly** — Clear terms for AI training and derivative works
- ✅ **Community-Friendly** — Encourages adoption and contribution

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📞 Support

- **Issues:** [GitHub Issues](https://github.com/xronocode/marketplace-stack/issues)
- **Discussions:** [GitHub Discussions](https://github.com/xronocode/marketplace-stack/discussions)

## 🙏 Acknowledgments

- Built with **Cursor** AI IDE
- Powered by **GRACE** methodology (Graph-RAG Anchored Code Engineering)
- Human engineering supervision by **Mikhail Evdokimov**

---

**Made with ❤️ by AI + Human Collaboration**

*This project demonstrates the potential of AI-assisted software development under proper engineering governance.*

# CareerBlitz

A monorepo for the CareerBlitz job automation platform.

## Structure

```
jobautoapply/
├── .github/
│   └── workflows/          # CI/CD workflows
├── backend/                # Backend API service
│   ├── src/
│   │   ├── domain/         # Domain layer
│   │   ├── application/    # Application layer
│   │   ├── infrastructure/ # Infrastructure layer
│   │   └── presentation/   # Presentation layer
│   ├── tests/              # Backend tests
│   └── requirements.txt
├── frontend/               # Next.js frontend
│   ├── src/
│   ├── public/
│   └── package.json
├── scrapers/               # Job scraping services
│   ├── src/
│   └── requirements.txt
├── infrastructure/         # Infrastructure as code
│   ├── kubernetes/
│   ├── terraform/
│   └── docker-compose.prod.yml
└── docs/                   # Documentation
```

## Getting Started

### Prerequisites

- Python 3.9+
- Node.js 18+
- Docker and Docker Compose

### Environment Setup

1. Copy `.env.example` files to `.env` in each service directory:
   - `backend/.env.example` → `backend/.env`
   - `frontend/.env.example` → `frontend/.env.local`
   - `scrapers/.env.example` → `scrapers/.env`

2. Fill in the environment variables with your actual values.

### Development

```bash
# Backend
cd backend
pip install -r requirements.txt

# Frontend
cd frontend
npm install
npm run dev

# Scrapers
cd scrapers
pip install -r requirements.txt
```

## License

MIT


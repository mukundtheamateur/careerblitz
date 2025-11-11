# ElevateNova - jobautoapply
## AI-Powered Job Scraping and Auto-Apply Platform

**Authors:** Mukund & Shivam  
**Co-founders of ElevateNova**

---

## Preface

Welcome to the **CareerBlitz Prompt-Generator Book**—a comprehensive guide to building a production-ready, AI-powered job scraping and auto-apply platform from the ground up.

This book was born from our journey at **ElevateNova**, where we recognized the need for a systematic, scalable approach to building complex software systems. As co-founders, we've experienced firsthand the challenges of transforming an idea into a robust, production-ready product that can scale to serve millions of users. xz

### Our Vision

The modern job search process is broken. Job seekers spend countless hours manually searching through job boards, tailoring resumes, and submitting applications—often with little feedback. We envisioned a platform that could automate this entire process while maintaining the personalization and quality that makes each application stand out.

**CareerBlitz ** represents our solution: an intelligent system that continuously scrapes job listings, uses AI to match opportunities with candidates, generates tailored application materials, and automates the submission process—all while respecting legal boundaries and maintaining ethical standards.

### Why This Book?

During our development journey, we realized that building such a system requires more than just coding skills. It demands:

- **Architectural Excellence**: Clean Architecture and Domain-Driven Design principles to ensure maintainability and scalability
- **Production Readiness**: Security, monitoring, testing, and deployment strategies that work in real-world scenarios
- **Continuous Evolution**: Frameworks for adapting to market changes and business needs
- **Systematic Approach**: Step-by-step guidance that can be followed by both human engineers and AI co-developers

This book is our attempt to document not just *what* to build, but *how* to build it systematically, with every decision backed by best practices and real-world considerations.

### What You'll Learn

This book takes you through **22 comprehensive phases**, from initial project setup to scaling for millions of users:

1. **Foundation** (Phases 1-4): Project setup, domain design, database architecture, and core business logic
2. **Core Features** (Phases 5-11): Scraping infrastructure, AI matching, resume generation, auto-apply, and frontend
3. **Production** (Phases 12-18): Security, monitoring, performance optimization, deployment, and documentation
4. **Growth** (Phases 19-22): Product readiness, enhancement frameworks, SDLC methodology, and scaling strategies

Each phase contains detailed steps with:
- **Copy-paste ready prompts** for AI assistants or code generators
- **Verification procedures** to ensure quality at each step
- **CI/CD integration** for automated testing and deployment
- **Git commit messages** for proper version control

### Who Is This Book For?

- **Entrepreneurs** looking to build a job automation platform
- **Engineering Teams** seeking a systematic approach to complex system development
- **AI Co-developers** needing structured prompts and clear specifications
- **Students** learning enterprise software architecture and development practices
- **Product Managers** understanding the technical complexity of modern platforms

### Our Approach

We've designed this book to be:

- **Practical**: Every step is actionable and can be implemented immediately
- **Comprehensive**: Covers everything from code to infrastructure to business strategy
- **Scalable**: Architecture designed to grow from MVP to millions of users
- **Maintainable**: Clean code principles and documentation throughout
- **Adaptable**: Frameworks for evolving with market needs

### Acknowledgments

This book represents the collective knowledge gained from building production systems, learning from industry best practices, and iterating on real-world challenges. We're grateful to the open-source community, the software engineering community, and everyone who has contributed to the tools and methodologies that make modern software development possible.

### How to Use This Book

1. **Start at Phase 1**: Follow the phases sequentially for a complete build
2. **Use the Prompts**: Copy prompts directly into AI assistants or code generators
3. **Verify Each Step**: Don't skip verification—it ensures quality
4. **Adapt as Needed**: Use the frameworks in Phases 19-22 to customize for your needs
5. **Iterate Continuously**: Use the SDLC methodology (Phase 21) for ongoing development

### The Journey Ahead

Building a production-ready platform is a marathon, not a sprint. This book provides the roadmap, but success comes from:

- **Persistence**: Following through on each phase
- **Quality**: Not cutting corners on testing and security
- **Learning**: Adapting as you discover new requirements
- **Iteration**: Using feedback to continuously improve

We hope this book serves as your comprehensive guide to building not just a product, but a scalable, maintainable, and successful platform.

**Let's build something great together.**

---

**Mukund & Shivam**  
*Co-founders, ElevateNova*  
*2025*

---

**Project Goal:** Build a production-ready, scalable web application that continuously scrapes job listings from multiple sources every hour, uses AI to match jobs with user profiles, generates tailored resumes and cover letters, and automates the application process. The system must be designed using Clean Architecture and Domain-Driven Design principles to support millions of users with high availability, fault tolerance, and real-time job feed updates.

---

## System Architecture Overview

![System Architecture](system_architecture.png)

---

## Phase 1 – Project Setup & Infrastructure Foundation
*Goal: Initialize the repository structure, development environment, and foundational infrastructure components following Clean Architecture principles.*

### Step 1.1 – Initialize Git Repository and Project Structure

**prompt:**
```
Create a monorepo structure for CareerBlitz  with the following directory layout:

```
jobautoapply/
├── .github/
│   └── workflows/
├── backend/
│   ├── src/
│   │   ├── domain/
│   │   ├── application/
│   │   ├── infrastructure/
│   │   └── presentation/
│   ├── tests/
│   ├── requirements.txt
│   ├── Dockerfile
│   └── docker-compose.yml
├── frontend/
│   ├── src/
│   ├── public/
│   ├── package.json
│   ├── Dockerfile
│   └── next.config.js
├── scrapers/
│   ├── src/
│   ├── requirements.txt
│   └── Dockerfile
├── infrastructure/
│   ├── kubernetes/
│   ├── terraform/
│   └── docker-compose.prod.yml
├── docs/
├── .gitignore
├── README.md
└── docker-compose.yml
```

Initialize git repository, create all directories, add comprehensive .gitignore for Python, Node.js, Docker, IDEs (VSCode, PyCharm, IntelliJ), and OS files. Include .env.example files for each service with placeholder environment variables.
```

**verify the generated content:**
Run `git status`, `tree -L 3` (or `find . -type d -maxdepth 3`), and verify all directories exist. Check that .gitignore excludes common build artifacts, virtual environments, and IDE files.

**desired output to verify:**
Complete monorepo structure with all directories created, .gitignore properly configured, and initial commit made.

**CI/CD:**
Add GitHub Actions workflow `.github/workflows/validate-structure.yml` that checks directory structure exists and .gitignore is present:
```yaml
name: Validate Structure
on: [push, pull_request]
jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Check directory structure
        run: |
          test -d backend/src/domain && echo "✓ Domain layer exists"
          test -d frontend/src && echo "✓ Frontend exists"
          test -f .gitignore && echo "✓ .gitignore exists"
```

**git commit message:**
```
chore: initialize monorepo structure with clean architecture layout
```

---

### Step 1.2 – Setup Python Backend Environment

**prompt:**
```
Create a Python 3.11+ virtual environment setup for the backend service. Generate requirements.txt with:
- FastAPI 0.104+
- Pydantic 2.5+
- SQLAlchemy 2.0+
- Alembic for migrations
- pytest, pytest-asyncio, pytest-cov for testing
- black, flake8, mypy for code quality
- python-dotenv for environment management
- uvicorn[standard] for ASGI server

Create a Makefile with commands: `make install`, `make test`, `make lint`, `make format`, `make run`. Add a .python-version file specifying Python 3.11. Create backend/.env.example with database URLs, Redis URLs, API keys placeholders.
```

**verify the generated content:**
Run `cd backend && python -m venv venv && source venv/bin/activate && pip install -r requirements.txt && python -c "import fastapi; print('OK')"`. Check Makefile commands work.

**desired output to verify:**
Virtual environment created, all dependencies installed successfully, FastAPI importable, Makefile commands execute without errors.

**CI/CD:**
Add step to GitHub Actions that installs Python 3.11, creates venv, installs dependencies, and runs `make lint`:
```yaml
- name: Setup Python
  uses: actions/setup-python@v4
  with:
    python-version: '3.11'
- name: Install dependencies
  run: |
    cd backend
    python -m pip install --upgrade pip
    pip install -r requirements.txt
- name: Lint
  run: cd backend && make lint
```

**git commit message:**
```
chore(backend): setup Python environment with FastAPI and development tools
```

---

### Step 1.3 – Setup Node.js Frontend Environment

**prompt:**
```
Create a Next.js 14+ project with TypeScript, TailwindCSS, and essential dependencies:
- next@14
- react@18, react-dom@18
- typescript@5
- tailwindcss@3, postcss, autoprefixer
- @tanstack/react-query for data fetching
- zustand for state management
- axios for HTTP client
- react-hook-form, zod for form validation
- shadcn/ui components

Configure next.config.js for production optimizations. Create package.json with scripts: dev, build, start, lint, test. Add .eslintrc.json, .prettierrc, tsconfig.json with strict TypeScript settings. Create frontend/.env.example with API base URL placeholder.
```

**verify the generated content:**
Run `cd frontend && npm install && npm run build`. Verify TypeScript compiles, TailwindCSS is configured, and Next.js builds successfully.

**desired output to verify:**
Next.js project initialized, all dependencies installed, TypeScript configuration valid, build completes without errors.

**CI/CD:**
Add GitHub Actions step:
```yaml
- name: Setup Node.js
  uses: actions/setup-node@v3
  with:
    node-version: '20'
    cache: 'npm'
    cache-dependency-path: frontend/package-lock.json
- name: Install and build
  run: |
    cd frontend
    npm ci
    npm run build
```

**git commit message:**
```
chore(frontend): initialize Next.js 14 project with TypeScript and TailwindCSS
```

---

### Step 1.4 – Setup Docker Development Environment

**prompt:**
```
Create docker-compose.yml in root with services:
- postgres:15-alpine (with init scripts)
- redis:7-alpine
- rabbitmq:3-management
- backend (build from backend/Dockerfile)
- frontend (build from frontend/Dockerfile)
- scrapers (build from scrapers/Dockerfile)

Configure networks, volumes for data persistence, environment variables. Create Dockerfiles for each service with multi-stage builds, health checks, and non-root users. Add docker-compose.override.yml.example for local overrides. Include wait-for-it.sh script for service dependencies.
```

**verify the generated content:**
Run `docker-compose up -d` and verify all containers start. Check `docker-compose ps` shows all services healthy. Test database connection: `docker-compose exec postgres psql -U postgres -c "SELECT version();"`.

**desired output to verify:**
All Docker containers start successfully, services are healthy, database is accessible, Redis and RabbitMQ respond to connections.

**CI/CD:**
Add Docker build and test step:
```yaml
- name: Build Docker images
  run: docker-compose build
- name: Test containers
  run: |
    docker-compose up -d
    sleep 10
    docker-compose ps
    docker-compose down
```

**git commit message:**
```
chore: add Docker Compose setup for local development environment
```

---

### Step 1.5 – Setup CI/CD Pipeline Foundation

**prompt:**
```
Create GitHub Actions workflow `.github/workflows/ci.yml` with:
- Matrix strategy for Python 3.11, 3.12
- Jobs: lint-backend, test-backend, lint-frontend, test-frontend, build-docker
- Caching for pip and npm dependencies
- Parallel job execution
- Artifact uploads for test reports
- Docker image building and pushing to GitHub Container Registry
- Conditional deployment on main branch

Add workflow for pull requests that runs all checks. Create .github/workflows/codeql.yml for security scanning. Add dependabot.yml for dependency updates.
```

**verify the generated content:**
Push to a branch and verify GitHub Actions runs. Check that all jobs complete, artifacts are uploaded, and Docker images are built.

**desired output to verify:**
CI pipeline triggers on push, all jobs pass, Docker images build successfully, test reports are generated.

**CI/CD:**
This step creates the CI/CD infrastructure itself. Verify by checking Actions tab in GitHub repository.

**git commit message:**
```
ci: setup GitHub Actions workflow for continuous integration
```

---

### Step 1.6 – Add Legal Compliance & Robots.txt Checker

**prompt:**
```
Create a robots.txt compliance checker module in backend/src/infrastructure/scraping/compliance.py:

- Function to fetch and parse robots.txt from target domains
- User-agent checking against robots.txt rules
- Rate limiting compliance (Crawl-delay parsing)
- ToS acknowledgment system that logs user acceptance
- Database table `scraping_compliance` with fields: domain, robots_txt_content, last_checked, is_allowed, crawl_delay
- Background job to periodically check robots.txt for all target domains
- Integration with scraper framework to respect robots.txt before scraping

Create migration for compliance table. Add configuration for default user-agent and crawl delays.
```

**verify the generated content:**
Run unit tests: `pytest backend/tests/test_compliance.py`. Test with real domains: `python -c "from backend.src.infrastructure.scraping.compliance import check_robots_txt; print(check_robots_txt('https://www.indeed.com'))"`.

**desired output to verify:**
Robots.txt checker successfully parses rules, database table created, compliance checks work for multiple domains, ToS logging functional.

**CI/CD:**
Add test step:
```yaml
- name: Test compliance checker
  run: |
    cd backend
    pytest tests/test_compliance.py -v
```

**git commit message:**
```
feat: add robots.txt compliance checker and ToS acknowledgment system
```

---

## Phase 2 – Domain-Driven Design & Clean Architecture Setup
*Goal: Establish domain models, bounded contexts, and clean architecture layers with proper dependency inversion.*

### Step 2.1 – Define Domain Bounded Contexts

**prompt:**
```
Create domain bounded context structure in backend/src/domain/:

```
domain/
├── job/
│   ├── __init__.py
│   ├── entities.py (Job, Company, Location)
│   ├── value_objects.py (JobId, Salary, JobHash)
│   ├── repositories.py (JobRepository interface)
│   └── services.py (JobMatchingService interface)
├── user/
│   ├── __init__.py
│   ├── entities.py (User, UserProfile, Resume)
│   ├── value_objects.py (UserId, Email, PasswordHash)
│   ├── repositories.py (UserRepository interface)
│   └── services.py (UserService interface)
├── scraper/
│   ├── __init__.py
│   ├── entities.py (ScraperConfig, ScrapeResult, ScrapeJob)
│   ├── value_objects.py (Source, ScrapeStatus)
│   ├── repositories.py (ScrapeJobRepository interface)
│   └── services.py (ScraperOrchestrator interface)
├── application/
│   ├── __init__.py
│   ├── entities.py (Application, ApplicationStatus)
│   ├── value_objects.py (ApplicationId, CoverLetter, TailoredResume)
│   ├── repositories.py (ApplicationRepository interface)
│   └── services.py (ApplicationService interface)
└── shared/
    ├── __init__.py
    ├── domain_events.py (DomainEvent base class)
    └── exceptions.py (DomainException base classes)
```

Define abstract base classes for entities (with id, created_at, updated_at), value objects (immutable), and repository interfaces. Use Protocol for type hints. Add domain events infrastructure.
```

**verify the generated content:**
Run `python -c "from backend.src.domain.job.entities import Job; from backend.src.domain.shared.domain_events import DomainEvent; print('OK')"`. Check that all interfaces are properly typed with Protocol.

**desired output to verify:**
All domain modules importable, entities and value objects defined, repository interfaces use Protocol, domain events infrastructure in place.

**CI/CD:**
Add type checking:
```yaml
- name: Type check domain layer
  run: |
    cd backend
    mypy src/domain --strict
```

**git commit message:**
```
feat(domain): define bounded contexts and core domain entities
```

---

### Step 2.2 – Implement Domain Entities with Rich Behavior

**prompt:**
```
Implement rich domain entities in backend/src/domain/job/entities.py:

- Job entity with methods: is_expired(), calculate_match_score(profile), mark_as_applied(), update_embedding(embedding)
- Company entity with methods: normalize_name(), get_domain()
- Location entity with methods: normalize(), get_coordinates(), is_remote()

Use Pydantic for validation. Entities should be immutable where possible. Add domain events: JobCreated, JobExpired, JobApplied. Implement value objects with validation (e.g., Salary must be positive, Email must be valid format).

Create unit tests for each entity method in backend/tests/domain/test_job_entities.py.
```

**verify the generated content:**
Run `pytest backend/tests/domain/ -v`. Test entity methods: `python -c "from backend.src.domain.job.entities import Job; j = Job(...); print(j.is_expired())"`.

**desired output to verify:**
All entity methods work correctly, domain events are emitted, value objects validate input, unit tests pass with >90% coverage.

**CI/CD:**
```yaml
- name: Test domain entities
  run: |
    cd backend
    pytest tests/domain/ -v --cov=src/domain --cov-report=term-missing
```

**git commit message:**
```
feat(domain): implement rich domain entities with business logic
```

---

### Step 2.3 – Setup Application Layer (Use Cases)

**prompt:**
```
Create application layer structure in backend/src/application/:

```
application/
├── job/
│   ├── use_cases/
│   │   ├── get_job_by_id.py
│   │   ├── search_jobs.py
│   │   ├── match_jobs_for_user.py
│   │   └── get_job_feed.py
│   └── dto.py (JobDTO, JobSearchFilters)
├── user/
│   ├── use_cases/
│   │   ├── register_user.py
│   │   ├── upload_resume.py
│   │   ├── update_profile.py
│   │   └── get_user_profile.py
│   └── dto.py (UserDTO, ResumeDTO)
├── scraper/
│   ├── use_cases/
│   │   ├── trigger_scrape.py
│   │   ├── get_scrape_status.py
│   │   └── list_scrape_history.py
│   └── dto.py (ScrapeJobDTO)
└── application/
    ├── use_cases/
    │   ├── generate_resume.py
    │   ├── generate_cover_letter.py
    │   ├── submit_application.py
    │   └── track_application_status.py
    └── dto.py (ApplicationDTO)
```

Each use case should be a class with a single `execute()` method. Use dependency injection for repositories. Return DTOs, not domain entities. Add error handling and logging.
```

**verify the generated content:**
Create integration test: `pytest backend/tests/application/test_job_use_cases.py`. Verify use cases can be instantiated and executed with mock repositories.

**desired output to verify:**
All use cases are importable, execute methods work with dependency injection, DTOs are properly serialized, integration tests pass.

**CI/CD:**
```yaml
- name: Test application layer
  run: |
    cd backend
    pytest tests/application/ -v
```

**git commit message:**
```
feat(application): implement use cases for job, user, scraper, and application domains
```

---

### Step 2.4 – Setup Infrastructure Layer Interfaces

**prompt:**
```
Create infrastructure layer structure in backend/src/infrastructure/:

```
infrastructure/
├── database/
│   ├── __init__.py
│   ├── session.py (SQLAlchemy session factory)
│   ├── base.py (Base model)
│   └── repositories/
│       ├── job_repository.py (implements JobRepository)
│       ├── user_repository.py (implements UserRepository)
│       └── application_repository.py (implements ApplicationRepository)
├── cache/
│   ├── __init__.py
│   └── redis_client.py (Redis connection pool)
├── messaging/
│   ├── __init__.py
│   └── rabbitmq_client.py (RabbitMQ publisher/consumer)
├── storage/
│   ├── __init__.py
│   └── s3_client.py (S3 file upload/download)
├── ai/
│   ├── __init__.py
│   ├── embedding_service.py (OpenAI/SBERT embeddings)
│   └── llm_service.py (OpenAI GPT for resume/cover letter)
└── scraping/
    ├── __init__.py
    ├── base_scraper.py (Abstract base scraper)
    └── proxy_manager.py (Proxy rotation)
```

Implement repository adapters that convert between domain entities and database models. Use dependency injection container (e.g., dependency-injector). Add connection pooling, retry logic, and error handling.
```

**verify the generated content:**
Test database connection: `python -c "from backend.src.infrastructure.database.session import get_session; session = next(get_session()); print('OK')"`. Test Redis: `python -c "from backend.src.infrastructure.cache.redis_client import redis_client; redis_client.ping()"`.

**desired output to verify:**
All infrastructure components connect successfully, repositories implement domain interfaces, dependency injection works, connection pooling active.

**CI/CD:**
```yaml
- name: Test infrastructure connections
  run: |
    docker-compose up -d postgres redis
    sleep 5
    cd backend
    pytest tests/infrastructure/ -v
```

**git commit message:**
```
feat(infrastructure): setup database, cache, messaging, and storage adapters
```

---

### Step 2.5 – Setup Presentation Layer (API)

**prompt:**
```
Create FastAPI presentation layer in backend/src/presentation/:

```
presentation/
├── __init__.py
├── api/
│   ├── __init__.py
│   ├── v1/
│   │   ├── __init__.py
│   │   ├── routes/
│   │   │   ├── jobs.py
│   │   │   ├── users.py
│   │   │   ├── applications.py
│   │   │   └── scrapers.py
│   │   └── dependencies.py (DI container setup)
│   └── middleware.py (CORS, logging, error handling)
├── schemas/
│   ├── job_schemas.py (Pydantic request/response models)
│   ├── user_schemas.py
│   └── application_schemas.py
└── main.py (FastAPI app initialization)
```

Implement REST endpoints with proper status codes, request validation, response serialization. Add OpenAPI documentation. Use dependency injection for use cases. Add authentication middleware (JWT). Include rate limiting and request logging.
```

**verify the generated content:**
Start API: `cd backend && uvicorn src.presentation.main:app --reload`. Test endpoints: `curl http://localhost:8000/api/v1/health` and `curl http://localhost:8000/docs` (Swagger UI).

**desired output to verify:**
FastAPI server starts, health endpoint returns 200, Swagger UI accessible, all routes registered, dependency injection works.

**CI/CD:**
```yaml
- name: Test API endpoints
  run: |
    cd backend
    uvicorn src.presentation.main:app --host 0.0.0.0 --port 8000 &
    sleep 5
    curl -f http://localhost:8000/api/v1/health || exit 1
```

**git commit message:**
```
feat(presentation): setup FastAPI REST API with dependency injection
```

---

## Phase 3 – Database Design & Schema
*Goal: Design scalable database schema with proper indexing, partitioning, and vector storage for embeddings.*

### Step 3.1 – Design Core Database Schema

**prompt:**
```
Create Alembic migration in backend/src/infrastructure/database/migrations/versions/001_initial_schema.py:

Tables:
- users (id UUID PRIMARY KEY, email VARCHAR UNIQUE, password_hash VARCHAR, created_at TIMESTAMP, updated_at TIMESTAMP, is_active BOOLEAN)
- user_profiles (id UUID PRIMARY KEY, user_id UUID FK, full_name VARCHAR, phone VARCHAR, location VARCHAR, resume_text TEXT, resume_file_url VARCHAR, skills JSONB, experience_years INTEGER, created_at TIMESTAMP, updated_at TIMESTAMP)
- jobs (id UUID PRIMARY KEY, title VARCHAR, company VARCHAR, location VARCHAR, salary_min DECIMAL, salary_max DECIMAL, currency VARCHAR, description TEXT, requirements TEXT, link VARCHAR UNIQUE, source VARCHAR, posted_at TIMESTAMP, scraped_at TIMESTAMP, job_hash VARCHAR UNIQUE, embedding VECTOR(384), created_at TIMESTAMP, updated_at TIMESTAMP, expires_at TIMESTAMP)
- companies (id UUID PRIMARY KEY, name VARCHAR UNIQUE, domain VARCHAR, website VARCHAR, created_at TIMESTAMP, updated_at TIMESTAMP)
- applications (id UUID PRIMARY KEY, user_id UUID FK, job_id UUID FK, status VARCHAR, tailored_resume_url VARCHAR, cover_letter_text TEXT, applied_at TIMESTAMP, response_received_at TIMESTAMP, created_at TIMESTAMP, updated_at TIMESTAMP)
- scrape_jobs (id UUID PRIMARY KEY, source VARCHAR, status VARCHAR, started_at TIMESTAMP, completed_at TIMESTAMP, jobs_found INTEGER, errors JSONB, created_at TIMESTAMP)

Add indexes: jobs(job_hash), jobs(source, posted_at), jobs(embedding vector_cosine_ops), applications(user_id, status), user_profiles(user_id). Use UUID as primary keys. Add foreign key constraints with CASCADE deletes.
```

**verify the generated content:**
Run migration: `cd backend && alembic upgrade head`. Check tables: `docker-compose exec postgres psql -U postgres -d CareerBlitz -c "\dt"`. Verify indexes: `\d+ jobs`.

**desired output to verify:**
All tables created, indexes present, foreign keys configured, UUID primary keys used.

**CI/CD:**
```yaml
- name: Run database migrations
  run: |
    cd backend
    alembic upgrade head
    docker-compose exec postgres psql -U postgres -d CareerBlitz -c "\dt"
```

**git commit message:**
```
feat(database): create initial schema with users, jobs, applications, and scrape_jobs tables
```

---

### Step 3.2 – Setup PostgreSQL Extensions and Vector Support

**prompt:**
```
Create migration 002_enable_extensions.py to enable:
- pgvector extension for embedding similarity search
- pg_trgm for fuzzy text matching
- btree_gin for GIN indexes on JSONB
- uuid-ossp for UUID generation

Create function for cosine similarity search:
```sql
CREATE OR REPLACE FUNCTION match_jobs_by_embedding(
    query_embedding vector(384),
    match_threshold float DEFAULT 0.7,
    match_count int DEFAULT 50
)
RETURNS TABLE (
    job_id uuid,
    similarity float
)
LANGUAGE plpgsql
AS $$
BEGIN
    RETURN QUERY
    SELECT
        j.id,
        1 - (j.embedding <=> query_embedding) as similarity
    FROM jobs j
    WHERE 1 - (j.embedding <=> query_embedding) > match_threshold
    ORDER BY j.embedding <=> query_embedding
    LIMIT match_count;
END;
$$;
```

Add GIN index on jobs.embedding using vector_cosine_ops.
```

**verify the generated content:**
Run migration and test: `docker-compose exec postgres psql -U postgres -d CareerBlitz -c "SELECT * FROM pg_extension WHERE extname IN ('vector', 'pg_trgm');"`. Test function: `SELECT * FROM match_jobs_by_embedding('[0.1,0.2,...]'::vector, 0.5, 10);`.

**desired output to verify:**
Extensions enabled, vector similarity function created, GIN index on embeddings exists, function returns results.

**CI/CD:**
```yaml
- name: Verify database extensions
  run: |
    docker-compose exec postgres psql -U postgres -d CareerBlitz -c "SELECT extname FROM pg_extension WHERE extname = 'vector';"
```

**git commit message:**
```
feat(database): enable pgvector extension and create embedding similarity function
```

---

### Step 3.3 – Implement Database Partitioning for Jobs Table

**prompt:**
```
Create migration 003_partition_jobs_table.py to partition jobs table by posted_at date (monthly partitions):

```sql
-- Drop existing jobs table and recreate as partitioned
CREATE TABLE jobs (
    id UUID PRIMARY KEY,
    title VARCHAR NOT NULL,
    company VARCHAR NOT NULL,
    location VARCHAR,
    salary_min DECIMAL,
    salary_max DECIMAL,
    currency VARCHAR,
    description TEXT,
    requirements TEXT,
    link VARCHAR UNIQUE,
    source VARCHAR NOT NULL,
    posted_at TIMESTAMP NOT NULL,
    scraped_at TIMESTAMP NOT NULL,
    job_hash VARCHAR UNIQUE,
    embedding VECTOR(384),
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW(),
    expires_at TIMESTAMP
) PARTITION BY RANGE (posted_at);

-- Create partitions for current and next 3 months
CREATE TABLE jobs_2025_11 PARTITION OF jobs
    FOR VALUES FROM ('2025-11-01') TO ('2025-12-01');
-- ... (create more partitions)
```

Add trigger function to automatically create new partitions. Create maintenance job to drop old partitions (>6 months).
```

**verify the generated content:**
Check partitions: `SELECT * FROM pg_partitions WHERE tablename = 'jobs';`. Insert test data and verify it goes to correct partition. Test auto-partition creation.

**desired output to verify:**
Jobs table partitioned by month, data inserts into correct partitions, auto-partition creation works, old partitions can be dropped.

**CI/CD:**
```yaml
- name: Test table partitioning
  run: |
    docker-compose exec postgres psql -U postgres -d CareerBlitz -c "SELECT schemaname, tablename FROM pg_tables WHERE tablename LIKE 'jobs_%';"
```

**git commit message:**
```
feat(database): implement monthly partitioning for jobs table
```

---

### Step 3.4 – Create Database Repository Implementations

**prompt:**
```
Implement SQLAlchemy repository adapters in backend/src/infrastructure/database/repositories/job_repository.py:

- JobRepository implementation with methods:
  - save(job: Job) -> Job
  - find_by_id(job_id: JobId) -> Optional[Job]
  - find_by_hash(job_hash: str) -> Optional[Job]
  - search(filters: JobSearchFilters) -> List[Job]
  - find_similar_by_embedding(embedding: List[float], limit: int) -> List[Job]
  - delete_expired_jobs() -> int

Use SQLAlchemy 2.0 async API. Map domain Job entity to JobModel ORM class. Handle transactions properly. Add connection pooling configuration. Implement bulk insert for performance.
```

**verify the generated content:**
Run tests: `pytest backend/tests/infrastructure/test_job_repository.py -v`. Test repository methods with real database: create job, find by id, search, similarity search.

**desired output to verify:**
Repository methods work correctly, domain entities properly mapped to ORM models, transactions handled, bulk operations efficient, tests pass.

**CI/CD:**
```yaml
- name: Test repositories
  run: |
    cd backend
    pytest tests/infrastructure/test_job_repository.py -v --cov=src/infrastructure/database
```

**git commit message:**
```
feat(infrastructure): implement SQLAlchemy repository adapters for job domain
```

---

## Phase 4 – Core Domain Models & Business Logic
*Goal: Implement complete domain models with business rules, validation, and domain events.*

### Step 4.1 – Implement User Domain with Authentication

**prompt:**
```
Implement user domain in backend/src/domain/user/:

- User entity with: register(), authenticate(password), update_email(), deactivate()
- PasswordHash value object with: hash_password(), verify_password() using bcrypt
- Email value object with validation
- UserProfile entity with: update_resume(), add_skill(), calculate_experience_level()
- UserRepository interface with: find_by_email(), find_by_id(), save()

Add domain events: UserRegistered, UserEmailUpdated, ProfileUpdated. Create unit tests for password hashing, email validation, and user methods.
```

**verify the generated content:**
Run tests: `pytest backend/tests/domain/test_user.py -v`. Test password hashing: `python -c "from backend.src.domain.user.value_objects import PasswordHash; p = PasswordHash.hash_password('test123'); print(PasswordHash.verify_password('test123', p))"`.

**desired output to verify:**
User entity methods work, password hashing secure, email validation correct, domain events emitted, all tests pass.

**CI/CD:**
```yaml
- name: Test user domain
  run: |
    cd backend
    pytest tests/domain/test_user.py -v --cov=src/domain/user
```

**git commit message:**
```
feat(domain): implement user domain with authentication and profile management
```

---

### Step 4.2 – Implement Job Domain with Matching Logic

**prompt:**
```
Implement job domain in backend/src/domain/job/:

- Job entity with: is_expired(), is_duplicate(other_job), calculate_freshness_score(), normalize_title()
- Salary value object with: parse_from_string(), to_annual(), get_range()
- JobHash value object: generate(title, company, location) -> str
- Location value object: normalize(), is_remote(), parse_coordinates()
- JobMatchingService interface: calculate_match_score(job, profile) -> float

Add business rules: jobs expire after 30 days, duplicate detection uses hash, matching considers skills/experience/location. Create comprehensive unit tests.
```

**verify the generated content:**
Test job methods: `python -c "from backend.src.domain.job.entities import Job; j = Job(...); print(j.is_expired())"`. Test matching: `pytest backend/tests/domain/test_job_matching.py`.

**desired output to verify:**
Job entity methods work, duplicate detection accurate, matching algorithm calculates scores correctly, all business rules enforced, tests pass.

**CI/CD:**
```yaml
- name: Test job domain
  run: |
    cd backend
    pytest tests/domain/test_job.py -v
```

**git commit message:**
```
feat(domain): implement job domain with matching and deduplication logic
```

---

### Step 4.3 – Implement Scraper Domain Models

**prompt:**
```
Implement scraper domain in backend/src/domain/scraper/:

- ScraperConfig entity with: validate(), get_rate_limit(), get_user_agent()
- ScrapeJob entity with: start(), complete(results), fail(error), get_status()
- ScrapeResult value object with: validate(), normalize()
- Source value object: enum of supported sources (INDEED, LINKEDIN, GLASSDOOR, etc.)
- ScrapeStatus enum: PENDING, RUNNING, COMPLETED, FAILED, CANCELLED

Add domain events: ScrapeJobStarted, ScrapeJobCompleted, ScrapeJobFailed. Implement retry logic in ScrapeJob entity.
```

**verify the generated content:**
Test scraper models: `pytest backend/tests/domain/test_scraper.py -v`. Create ScrapeJob, start it, complete it, verify events emitted.

**desired output to verify:**
Scraper domain models work, status transitions valid, retry logic functional, domain events emitted, tests pass.

**CI/CD:**
```yaml
- name: Test scraper domain
  run: |
    cd backend
    pytest tests/domain/test_scraper.py -v
```

**git commit message:**
```
feat(domain): implement scraper domain models and job orchestration
```

---

### Step 4.4 – Implement Application Domain

**prompt:**
```
Implement application domain in backend/src/domain/application/:

- Application entity with: submit(), update_status(), mark_as_sent(), track_response()
- ApplicationStatus enum: DRAFT, PENDING, SUBMITTED, REVIEWED, REJECTED, ACCEPTED
- TailoredResume value object: generate_from_base(job), validate_format()
- CoverLetter value object: generate(job, profile), personalize()
- ApplicationService interface: can_apply(user, job) -> bool, get_application_history(user) -> List[Application]

Add business rules: user can only apply once per job, applications expire after 90 days, status transitions validated. Create unit tests.
```

**verify the generated content:**
Test application logic: `pytest backend/tests/domain/test_application.py -v`. Verify status transitions, duplicate prevention, expiration logic.

**desired output to verify:**
Application entity methods work, status transitions validated, business rules enforced, tests pass.

**CI/CD:**
```yaml
- name: Test application domain
  run: |
    cd backend
    pytest tests/domain/test_application.py -v
```

**git commit message:**
```
feat(domain): implement application domain with status tracking
```

---

## Phase 5 – Scraper Infrastructure & Base Framework
*Goal: Build robust, scalable scraper framework with proxy rotation, rate limiting, and error handling.*

### Step 5.1 – Create Base Scraper Abstract Class

**prompt:**
```
Create base scraper framework in scrapers/src/scrapers/base_scraper.py:

Abstract base class BaseScraper with:
- __init__(config: ScraperConfig)
- abstract scrape(keywords: List[str], location: str) -> List[ScrapeResult]
- _fetch_page(url: str) -> BeautifulSoup
- _parse_job_listing(html: str) -> List[Dict]
- _normalize_job_data(raw: Dict) -> ScrapeResult
- _handle_errors(error: Exception) -> None
- _respect_rate_limit() -> None
- _rotate_proxy() -> None
- _detect_captcha() -> bool
- _solve_captcha() -> str

Include retry logic with exponential backoff, user-agent rotation, request headers randomization. Add logging for all operations.
```

**verify the generated content:**
Create test scraper: `class TestScraper(BaseScraper): ...`. Test instantiation and method calls. Verify retry logic works.

**desired output to verify:**
Base scraper class can be subclassed, all abstract methods defined, retry logic functional, rate limiting works, logging outputs correctly.

**CI/CD:**
```yaml
- name: Test base scraper
  run: |
    cd scrapers
    pytest tests/test_base_scraper.py -v
```

**git commit message:**
```
feat(scrapers): create base scraper framework with retry and rate limiting
```

---

### Step 5.2 – Implement Proxy Rotation Manager

**prompt:**
```
Create proxy manager in scrapers/src/scrapers/proxy_manager.py:

- ProxyManager class with:
  - add_proxy(proxy: ProxyConfig)
  - get_next_proxy() -> ProxyConfig
  - mark_proxy_failed(proxy: ProxyConfig)
  - get_healthy_proxies() -> List[ProxyConfig]
  - rotate_user_agent() -> str

- ProxyConfig dataclass: host, port, username, password, type (http/socks5), health_score, last_used
- Health monitoring: track success/failure rates, automatically disable bad proxies
- Load balancing: round-robin with health-based selection
- Integration with free proxy lists and paid services (BrightData, ScraperAPI)

Add Redis caching for proxy health scores. Create unit tests.
```

**verify the generated content:**
Test proxy manager: `python -c "from scrapers.src.scrapers.proxy_manager import ProxyManager; pm = ProxyManager(); print(pm.get_next_proxy())"`. Test health tracking and rotation.

**desired output to verify:**
Proxy manager rotates proxies correctly, health tracking works, failed proxies disabled, user-agent rotation functional, Redis caching operational.

**CI/CD:**
```yaml
- name: Test proxy manager
  run: |
    cd scrapers
    pytest tests/test_proxy_manager.py -v
```

**git commit message:**
```
feat(scrapers): implement proxy rotation manager with health monitoring
```

---

### Step 5.3 – Implement CAPTCHA Solving Integration

**prompt:**
```
Create CAPTCHA solver in scrapers/src/scrapers/captcha_solver.py:

- CaptchaSolver class with:
  - detect_captcha(page_content: str) -> bool
  - solve_reCAPTCHA(site_key: str, page_url: str) -> str
  - solve_hCaptcha(site_key: str, page_url: str) -> str
  - solve_image_captcha(image_url: str) -> str

- Integration with 2Captcha API:
  - submit_captcha_task() -> task_id
  - get_solution(task_id) -> solution
  - Polling with timeout

- Fallback strategies:
  - Browser automation with manual solving
  - CAPTCHA detection logging for manual review
  - Skip pages with unsolvable CAPTCHAs

Add configuration for API keys, timeout settings, retry logic. Create unit tests with mocked API responses.
```

**verify the generated content:**
Test CAPTCHA detection: `pytest scrapers/tests/test_captcha_solver.py -v`. Mock 2Captcha API and verify solution retrieval.

**desired output to verify:**
CAPTCHA detection works, 2Captcha integration functional, polling logic correct, fallback strategies implemented, tests pass.

**CI/CD:**
```yaml
- name: Test CAPTCHA solver
  run: |
    cd scrapers
    pytest tests/test_captcha_solver.py -v
```

**git commit message:**
```
feat(scrapers): add CAPTCHA solving integration with 2Captcha
```

---

### Step 5.4 – Create Scraper Orchestrator Service

**prompt:**
```
Create scraper orchestrator in backend/src/application/scraper/use_cases/orchestrate_scraping.py:

- ScraperOrchestrator class:
  - schedule_scraping_jobs() -> List[ScrapeJob]
  - execute_scrape_job(job: ScrapeJob) -> ScrapeResult
  - distribute_scrapers_across_workers() -> Dict
  - handle_scrape_failure(job: ScrapeJob, error: Exception) -> None
  - deduplicate_results(results: List[ScrapeResult]) -> List[ScrapeResult]

- Integration with Celery:
  - Create Celery tasks for each scraper source
  - Task routing to dedicated worker queues
  - Retry failed tasks with exponential backoff
  - Task result tracking in Redis

- Scheduling:
  - Celery Beat configuration for hourly runs
  - Dynamic scheduling based on source priority
  - Load balancing across workers

Create Celery configuration file with task definitions.
```

**verify the generated content:**
Start Celery worker: `celery -A backend.src.infrastructure.messaging.celery_app worker --loglevel=info`. Trigger task and verify execution. Check Redis for task results.

**desired output to verify:**
Orchestrator schedules jobs correctly, Celery tasks execute, workers process jobs, results stored, retry logic works.

**CI/CD:**
```yaml
- name: Test scraper orchestrator
  run: |
    cd backend
    celery -A src.infrastructure.messaging.celery_app inspect active
```

**git commit message:**
```
feat(application): implement scraper orchestrator with Celery integration
```

---

### Step 5.5 – Setup Celery Configuration and Workers

**prompt:**
```
Create Celery configuration in backend/src/infrastructure/messaging/celery_app.py:

- Celery app initialization with:
  - Broker: RabbitMQ connection
  - Result backend: Redis
  - Task serialization: JSON
  - Timezone: UTC
  - Task routes: separate queues for scrapers, AI processing, email sending

- Celery Beat schedule in celery_beat_schedule.py:
  - Hourly job scraping: every hour at :00
  - Daily cleanup: expired jobs removal at 2 AM
  - Weekly analytics: every Monday at 3 AM

- Worker configuration:
  - Concurrency: configurable (default 4)
  - Prefetch multiplier: 4
  - Task time limits: 30 minutes for scrapers
  - Task soft time limits: 25 minutes

- Monitoring:
  - Flower for task monitoring (optional)
  - Task logging to ELK stack
  - Metrics export to Prometheus

Create docker-compose service for Celery worker and beat scheduler.
```

**verify the generated content:**
Start Celery: `docker-compose up celery-worker celery-beat`. Check logs for task execution. Verify beat schedule: `celery -A backend.src.infrastructure.messaging.celery_app inspect scheduled`.

**desired output to verify:**
Celery workers start, beat scheduler runs, tasks execute on schedule, monitoring accessible, logs output correctly.

**CI/CD:**
```yaml
- name: Test Celery setup
  run: |
    docker-compose up -d rabbitmq redis
    sleep 5
    cd backend
    celery -A src.infrastructure.messaging.celery_app inspect ping
```

**git commit message:**
```
feat(infrastructure): setup Celery with RabbitMQ and Redis for task queue
```

---

## Phase 6 – Individual Scraper Implementations
*Goal: Implement specific scrapers for major job boards with robust error handling and data extraction.*

### Step 6.1 – Implement Indeed Scraper

**prompt:**
```
Create Indeed scraper in scrapers/src/scrapers/sources/indeed_scraper.py:

- IndeedScraper(BaseScraper) class:
  - scrape(keywords: List[str], location: str) -> List[ScrapeResult]
  - _build_search_url(keywords, location, page) -> str
  - _extract_job_cards(soup: BeautifulSoup) -> List[Dict]
  - _extract_job_details(job_url: str) -> Dict
  - _parse_salary(salary_text: str) -> Salary
  - _parse_posted_date(date_text: str) -> datetime

- Handle pagination: iterate through all result pages
- Extract: title, company, location, salary, description, requirements, posted date, job ID
- Use Playwright for JavaScript-heavy pages
- Respect rate limits: 1 request per 2 seconds
- Handle anti-bot measures: random delays, human-like scrolling

Create unit tests with mocked HTML responses. Add integration test (optional, can be skipped in CI).
```

**verify the generated content:**
Run scraper: `python -m scrapers.src.scrapers.sources.indeed_scraper --keywords "software engineer" --location "San Francisco"`. Verify JSON output with job listings. Check rate limiting works.

**desired output to verify:**
Indeed scraper extracts job listings, pagination works, salary parsing correct, dates normalized, rate limiting enforced, tests pass.

**CI/CD:**
```yaml
- name: Test Indeed scraper
  run: |
    cd scrapers
    pytest tests/sources/test_indeed_scraper.py -v
```

**git commit message:**
```
feat(scrapers): implement Indeed job scraper with pagination and data extraction
```

---

### Step 6.2 – Implement LinkedIn Jobs Scraper

**prompt:**
```
Create LinkedIn scraper in scrapers/src/scrapers/sources/linkedin_scraper.py:

- LinkedInScraper(BaseScraper) class:
  - Requires authenticated session (cookies or API)
  - scrape(keywords: List[str], location: str) -> List[ScrapeResult]
  - _authenticate() -> Session
  - _search_jobs_api(keywords, location) -> JSON (if API available)
  - _scrape_jobs_html(soup: BeautifulSoup) -> List[Dict]
  - _extract_company_info(company_url: str) -> Dict
  - Handle LinkedIn's dynamic content with Playwright
  - Extract: title, company, location, salary (if available), description, job ID, application link

- Anti-bot measures:
  - Random mouse movements
  - Human-like typing delays
  - Session rotation
  - CAPTCHA detection and solving

- Rate limiting: Very conservative (1 request per 5 seconds)
- Error handling: Detect account restrictions, IP bans

Create comprehensive tests. Add configuration for LinkedIn credentials.
```

**verify the generated content:**
Test scraper with mock responses. Verify authentication flow, job extraction, error handling. Check rate limiting.

**desired output to verify:**
LinkedIn scraper authenticates, extracts jobs, handles dynamic content, respects rate limits, detects bans, tests pass.

**CI/CD:**
```yaml
- name: Test LinkedIn scraper
  run: |
    cd scrapers
    pytest tests/sources/test_linkedin_scraper.py -v
```

**git commit message:**
```
feat(scrapers): implement LinkedIn jobs scraper with authentication and anti-bot measures
```

---

### Step 6.3 – Implement Glassdoor Scraper

**prompt:**
```
Create Glassdoor scraper in scrapers/src/scrapers/sources/glassdoor_scraper.py:

- GlassdoorScraper(BaseScraper) class:
  - scrape(keywords: List[str], location: str) -> List[ScrapeResult]
  - _handle_modal_popups() -> None (close signup prompts)
  - _extract_job_listings(soup: BeautifulSoup) -> List[Dict]
  - _parse_company_rating(rating_html: str) -> float
  - _extract_salary_estimate(salary_html: str) -> Salary
  - Handle JavaScript rendering with Playwright
  - Extract: title, company, location, salary estimate, company rating, description, job type

- Special handling:
  - Modal dialogs and popups
  - Infinite scroll pagination
  - Salary estimates (ranges)
  - Company information pages

Create tests with sample HTML. Add error handling for blocked requests.
```

**verify the generated content:**
Run scraper and verify job extraction. Test modal handling, pagination, salary parsing. Check error handling.

**desired output to verify:**
Glassdoor scraper extracts jobs, handles modals, parses ratings and salaries, pagination works, tests pass.

**CI/CD:**
```yaml
- name: Test Glassdoor scraper
  run: |
    cd scrapers
    pytest tests/sources/test_glassdoor_scraper.py -v
```

**git commit message:**
```
feat(scrapers): implement Glassdoor scraper with modal handling and salary estimates
```

---

### Step 6.4 – Implement Generic Company Career Page Scraper

**prompt:**
```
Create generic company career page scraper in scrapers/src/scrapers/sources/company_career_scraper.py:

- CompanyCareerScraper(BaseScraper) class:
  - scrape(company_domain: str) -> List[ScrapeResult]
  - _discover_career_page(domain: str) -> str (check /careers, /jobs, /join-us)
  - _parse_sitemap(sitemap_url: str) -> List[str]
  - _detect_job_listing_patterns(html: str) -> List[Dict]
  - _extract_structured_data(schema_markup: str) -> Dict (JSON-LD, microdata)
  - Support for:
    - Greenhouse.io ATS
    - Lever ATS
    - Workday ATS
    - Custom career pages
    - Sitemap-based discovery

- Pattern matching:
  - Common job listing CSS selectors
  - Schema.org JobPosting markup
  - API endpoints (if discoverable)

- Configuration: YAML file mapping domains to scraping strategies

Create flexible pattern matching system. Add tests for different ATS types.
```

**verify the generated content:**
Test with various company domains: `python -m scrapers.src.scrapers.sources.company_career_scraper --domain "example.com"`. Verify career page discovery, job extraction, ATS detection.

**desired output to verify:**
Career page scraper discovers pages, extracts jobs from various ATS, pattern matching works, schema.org parsing functional, tests pass.

**CI/CD:**
```yaml
- name: Test company career scraper
  run: |
    cd scrapers
    pytest tests/sources/test_company_career_scraper.py -v
```

**git commit message:**
```
feat(scrapers): implement generic company career page scraper with ATS support
```

---

### Step 6.5 – Create Scraper Factory and Registry

**prompt:**
```
Create scraper factory in scrapers/src/scrapers/factory.py:

- ScraperFactory class:
  - register_scraper(source: Source, scraper_class: Type[BaseScraper])
  - create_scraper(source: Source, config: ScraperConfig) -> BaseScraper
  - get_available_sources() -> List[Source]
  - get_scraper_config(source: Source) -> ScraperConfig

- ScraperRegistry: Auto-register all scrapers using decorator pattern
- Configuration management: Load scraper configs from YAML file
- Health checks: Test scraper availability before registration

Create scraper_registry.py that auto-discovers and registers all scrapers in sources/ directory. Add factory tests.
```

**verify the generated content:**
Test factory: `python -c "from scrapers.src.scrapers.factory import ScraperFactory; f = ScraperFactory(); scraper = f.create_scraper('INDEED'); print(type(scraper))"`. Verify all scrapers registered.

**desired output to verify:**
Factory creates scrapers correctly, registry auto-discovers scrapers, configuration loaded, health checks work, tests pass.

**CI/CD:**
```yaml
- name: Test scraper factory
  run: |
    cd scrapers
    pytest tests/test_factory.py -v
```

**git commit message:**
```
feat(scrapers): create scraper factory and auto-registration system
```

---

## Phase 7 – Data Normalization & Deduplication
*Goal: Build robust data cleaning, normalization, and deduplication pipeline.*

### Step 7.1 – Implement Job Data Normalizer

**prompt:**
```
Create job data normalizer in backend/src/infrastructure/scraping/normalizer.py:

- JobNormalizer class:
  - normalize_title(title: str) -> str (remove extra spaces, standardize case)
  - normalize_company(company: str) -> str (remove Inc., LLC, standardize)
  - normalize_location(location: str) -> Location (parse city, state, country, remote)
  - normalize_salary(salary_text: str) -> Salary (parse ranges, convert to annual)
  - normalize_description(html: str) -> str (clean HTML, extract text, remove noise)
  - normalize_requirements(requirements: str) -> List[str] (extract skills, technologies)
  - normalize_posted_date(date_text: str) -> datetime (handle relative dates: "2 days ago", "1 week ago")
  - normalize_job_type(job_type: str) -> str (FULL_TIME, PART_TIME, CONTRACT, INTERNSHIP)

- Use libraries:
  - BeautifulSoup for HTML cleaning
  - dateparser for date parsing
  - regex for pattern matching
  - unidecode for text normalization

- Handle edge cases:
  - Missing fields with defaults
  - Invalid data with fallbacks
  - Multiple currency formats
  - Various date formats

Create comprehensive unit tests with various input formats.
```

**verify the generated content:**
Run tests: `pytest backend/tests/infrastructure/test_normalizer.py -v`. Test with sample data: `python -c "from backend.src.infrastructure.scraping.normalizer import JobNormalizer; n = JobNormalizer(); print(n.normalize_title('  Software   Engineer  '))"`.

**desired output to verify:**
Normalizer cleans all fields correctly, handles edge cases, parses dates accurately, extracts skills, tests pass with >95% coverage.

**CI/CD:**
```yaml
- name: Test normalizer
  run: |
    cd backend
    pytest tests/infrastructure/test_normalizer.py -v --cov=src/infrastructure/scraping/normalizer
```

**git commit message:**
```
feat(infrastructure): implement job data normalizer with comprehensive field cleaning
```

---

### Step 7.2 – Implement Job Deduplication Engine

**prompt:**
```
Create deduplication engine in backend/src/infrastructure/scraping/deduplicator.py:

- JobDeduplicator class:
  - generate_job_hash(job: ScrapeResult) -> str (title + company + location normalized)
  - find_duplicates(job: ScrapeResult, existing_jobs: List[Job]) -> List[Job]
  - calculate_similarity(job1: Job, job2: Job) -> float (fuzzy matching)
  - merge_duplicate_jobs(jobs: List[Job]) -> Job (keep best data from all)

- Hash generation:
  - Normalize title, company, location
  - Remove special characters
  - Case-insensitive comparison
  - Handle abbreviations (Inc. vs Incorporated)

- Fuzzy matching:
  - Use Levenshtein distance for title similarity
  - Company name fuzzy matching (handle variations)
  - Location proximity matching (same city/region)
  - Threshold: 0.85 similarity = duplicate

- Merge strategy:
  - Keep most complete description
  - Use highest salary if ranges differ
  - Preserve all source links
  - Keep earliest posted_at date

- Redis caching for hash lookups (O(1) duplicate detection)
- Batch processing for performance

Create unit tests with various duplicate scenarios.
```

**verify the generated content:**
Test deduplication: `pytest backend/tests/infrastructure/test_deduplicator.py -v`. Test hash generation and similarity calculation with sample jobs.

**desired output to verify:**
Deduplicator generates consistent hashes, detects duplicates accurately, fuzzy matching works, merge strategy preserves best data, Redis caching functional, tests pass.

**CI/CD:**
```yaml
- name: Test deduplicator
  run: |
    cd backend
    pytest tests/infrastructure/test_deduplicator.py -v
```

**git commit message:**
```
feat(infrastructure): implement job deduplication engine with fuzzy matching
```

---

### Step 7.3 – Create Data Validation Pipeline

**prompt:**
```
Create validation pipeline in backend/src/infrastructure/scraping/validator.py:

- JobValidator class:
  - validate_required_fields(job: ScrapeResult) -> ValidationResult
  - validate_title(title: str) -> bool (not empty, reasonable length)
  - validate_company(company: str) -> bool (not empty, not spam)
  - validate_location(location: Location) -> bool (valid format)
  - validate_salary(salary: Salary) -> bool (reasonable range, valid currency)
  - validate_description(description: str) -> bool (not too short, not spam)
  - validate_link(link: str) -> bool (valid URL, accessible)
  - validate_posted_date(date: datetime) -> bool (not future, not too old)

- Validation rules:
  - Title: 3-200 characters, no spam keywords
  - Company: 2-100 characters, not in blacklist
  - Salary: min < max, within reasonable bounds
  - Description: >100 characters, contains job-related keywords
  - Link: valid URL format, domain matches source
  - Posted date: within last 90 days

- Spam detection:
  - Keyword blacklist (MLM, pyramid schemes, etc.)
  - Suspicious patterns detection
  - Link validation (check if URL is accessible)

- ValidationResult dataclass:
  - is_valid: bool
  - errors: List[str]
  - warnings: List[str]

Create comprehensive validation tests.
```

**verify the generated content:**
Run validation tests: `pytest backend/tests/infrastructure/test_validator.py -v`. Test with valid and invalid job data.

**desired output to verify:**
Validator catches all invalid data, spam detection works, validation results clear, tests cover all edge cases, tests pass.

**CI/CD:**
```yaml
- name: Test validator
  run: |
    cd backend
    pytest tests/infrastructure/test_validator.py -v
```

**git commit message:**
```
feat(infrastructure): create job data validation pipeline with spam detection
```

---

### Step 7.4 – Implement Data Processing Pipeline

**prompt:**
```
Create data processing pipeline in backend/src/application/scraper/use_cases/process_scraped_jobs.py:

- JobProcessingPipeline class:
  - process_batch(jobs: List[ScrapeResult]) -> List[Job]
  - normalize_all(jobs: List[ScrapeResult]) -> List[ScrapeResult]
  - validate_all(jobs: List[ScrapeResult]) -> List[ScrapeResult]
  - deduplicate_all(jobs: List[ScrapeResult]) -> List[ScrapeResult]
  - enrich_jobs(jobs: List[ScrapeResult]) -> List[ScrapeResult] (add company info, coordinates)
  - save_to_database(jobs: List[Job]) -> int

- Pipeline stages:
  1. Normalization (clean all fields)
  2. Validation (filter invalid jobs)
  3. Deduplication (remove duplicates)
  4. Enrichment (add metadata)
  5. Persistence (save to database)

- Error handling:
  - Continue processing on individual job failures
  - Log all errors for debugging
  - Retry failed operations
  - Dead letter queue for problematic jobs

- Performance:
  - Batch processing (100 jobs at a time)
  - Parallel processing where possible
  - Database bulk inserts
  - Redis caching for lookups

- Metrics:
  - Jobs processed count
  - Validation failures count
  - Duplicates found count
  - Processing time

Create integration tests for the full pipeline.
```

**verify the generated content:**
Run pipeline: `python -c "from backend.src.application.scraper.use_cases.process_scraped_jobs import JobProcessingPipeline; p = JobProcessingPipeline(); results = p.process_batch([...])"`. Check database for saved jobs.

**desired output to verify:**
Pipeline processes jobs through all stages, errors handled gracefully, batch processing efficient, metrics collected, jobs saved to database, tests pass.

**CI/CD:**
```yaml
- name: Test processing pipeline
  run: |
    cd backend
    pytest tests/application/test_process_scraped_jobs.py -v
```

**git commit message:**
```
feat(application): implement job data processing pipeline with normalization and deduplication
```

---

## Phase 8 – AI Matching Engine
*Goal: Build AI-powered job matching system using embeddings and semantic similarity.*

### Step 8.1 – Setup Embedding Service

**prompt:**
```
Create embedding service in backend/src/infrastructure/ai/embedding_service.py:

- EmbeddingService class:
  - generate_embedding(text: str) -> List[float]
  - generate_batch_embeddings(texts: List[str]) -> List[List[float]]
  - get_embedding_dimension() -> int (384 for all-MiniLM-L6-)

- Model options:
  - Primary: sentence-transformers/all-MiniLM-L6- (local, fast)
  - Fallback: OpenAI text-embedding-ada-002 (cloud, higher quality)
  - Configuration-based selection

- Implementation:
  - Load model on service initialization
  - Batch processing for efficiency
  - Caching embeddings in Redis (key: text hash)
  - Error handling and retries

- Performance:
  - Model loading: lazy initialization
  - Batch size: 32 texts per batch
  - GPU support if available (CUDA)
  - Async processing for API calls

- Integration:
  - HuggingFace transformers library
  - OpenAI API client
  - Redis for caching

Create unit tests with mocked model responses.
```

**verify the generated content:**
Test embedding generation: `python -c "from backend.src.infrastructure.ai.embedding_service import EmbeddingService; es = EmbeddingService(); emb = es.generate_embedding('software engineer'); print(len(emb))"`. Verify dimension is 384.

**desired output to verify:**
Embedding service generates vectors, batch processing works, caching functional, model loads correctly, tests pass.

**CI/CD:**
```yaml
- name: Test embedding service
  run: |
    cd backend
    pytest tests/infrastructure/test_embedding_service.py -v
```

**git commit message:**
```
feat(infrastructure): setup embedding service with sentence-transformers and OpenAI support
```

---

### Step 8.2 – Implement Job Embedding Generation

**prompt:**
```
Create job embedding generator in backend/src/application/job/use_cases/generate_job_embeddings.py:

- GenerateJobEmbeddings use case:
  - execute(job: Job) -> Job (with embedding)
  - generate_embedding_text(job: Job) -> str (combine title, description, requirements)
  - update_job_embedding(job: Job, embedding: List[float]) -> Job

- Embedding text composition:
  - Title (weight: 2x)
  - Description (weight: 1x)
  - Requirements (weight: 1.5x)
  - Skills extracted (weight: 1x)
  - Company name (weight: 0.5x)

- Batch processing:
  - Process multiple jobs in parallel
  - Update database with embeddings
  - Handle failures gracefully

- Background job:
  - Celery task to generate embeddings for new jobs
  - Scheduled job to regenerate embeddings for updated jobs
  - Retry failed embeddings

- Database:
  - Store embeddings in jobs.embedding column (VECTOR type)
  - Index for fast similarity search

Create use case tests and Celery task tests.
```

**verify the generated content:**
Test embedding generation: `pytest backend/tests/application/test_generate_job_embeddings.py -v`. Verify embeddings stored in database.

**desired output to verify:**
Embeddings generated for jobs, text composition correct, batch processing works, database updates successful, Celery tasks execute, tests pass.

**CI/CD:**
```yaml
- name: Test job embedding generation
  run: |
    cd backend
    pytest tests/application/test_generate_job_embeddings.py -v
```

**git commit message:**
```
feat(application): implement job embedding generation with batch processing
```

---

### Step 8.3 – Implement User Profile Embedding

**prompt:**
```
Create user profile embedding in backend/src/application/user/use_cases/generate_profile_embedding.py:

- GenerateProfileEmbedding use case:
  - execute(user_id: UserId) -> UserProfile (with embedding)
  - generate_embedding_text(profile: UserProfile) -> str
  - update_profile_embedding(profile: UserProfile, embedding: List[float]) -> UserProfile

- Embedding text composition:
  - Resume text (weight: 2x)
  - Skills list (weight: 1.5x)
  - Experience descriptions (weight: 1x)
  - Education (weight: 0.5x)
  - Preferred job titles (weight: 1x)
  - Preferred locations (weight: 0.5x)

- Storage:
  - Add embedding column to user_profiles table
  - Cache in Redis for fast matching
  - Update on profile changes

- Background processing:
  - Generate embedding on profile creation/update
  - Celery task for batch regeneration
  - Invalidate cache on updates

Create use case tests.
```

**verify the generated content:**
Test profile embedding: `pytest backend/tests/application/test_generate_profile_embedding.py -v`. Verify embedding stored and cached.

**desired output to verify:**
Profile embeddings generated, text composition correct, storage and caching work, background tasks execute, tests pass.

**CI/CD:**
```yaml
- name: Test profile embedding
  run: |
    cd backend
    pytest tests/application/test_generate_profile_embedding.py -v
```

**git commit message:**
```
feat(application): implement user profile embedding generation
```

---

### Step 8.4 – Implement Semantic Job Matching

**prompt:**
```
Create job matching service in backend/src/application/job/use_cases/match_jobs_for_user.py:

- MatchJobsForUser use case:
  - execute(user_id: UserId, limit: int = 50, filters: JobFilters = None) -> List[MatchedJob]
  - calculate_similarity(user_embedding: List[float], job_embedding: List[float]) -> float
  - apply_filters(jobs: List[Job], filters: JobFilters) -> List[Job]
  - rank_jobs(jobs: List[MatchedJob]) -> List[MatchedJob]

- Matching algorithm:
  1. Get user profile embedding
  2. Query database for similar job embeddings (cosine similarity)
  3. Apply business rules (location, salary, experience)
  4. Calculate composite match score
  5. Rank and return top N jobs

- Match score calculation:
  - Semantic similarity: 60% weight
  - Skills overlap: 20% weight
  - Experience match: 10% weight
  - Location preference: 5% weight
  - Salary range: 5% weight

- Database query:
  - Use pgvector cosine similarity operator (<=>)
  - Filter by similarity threshold (>0.7)
  - Limit results, then apply business filters
  - Use GIN index for performance

- Caching:
  - Cache match results in Redis (TTL: 1 hour)
  - Invalidate on profile/job updates

Create integration tests with sample embeddings.
```

**verify the generated content:**
Test matching: `pytest backend/tests/application/test_match_jobs_for_user.py -v`. Test with real user profile and jobs.

**desired output to verify:**
Matching algorithm works, similarity scores calculated correctly, filters applied, ranking accurate, database queries efficient, caching functional, tests pass.

**CI/CD:**
```yaml
- name: Test job matching
  run: |
    cd backend
    pytest tests/application/test_match_jobs_for_user.py -v
```

**git commit message:**
```
feat(application): implement semantic job matching with composite scoring
```

---

### Step 8.5 – Create Matching API Endpoint

**prompt:**
```
Create matching API endpoint in backend/src/presentation/api/v1/routes/jobs.py:

- GET /api/v1/jobs/matches
  - Query params: limit (default 50), filters (JSON)
  - Authentication: Required (JWT)
  - Response: List of MatchedJobDTO with similarity scores

- GET /api/v1/jobs/{job_id}/match-score
  - Calculate match score for specific job
  - Response: MatchScoreDTO with breakdown

- Request validation:
  - Pydantic schemas for filters
  - Rate limiting: 100 requests/hour per user

- Response format:
```json
{
  "jobs": [
    {
      "id": "uuid",
      "title": "Software Engineer",
      "company": "Google",
      "match_score": 0.92,
      "score_breakdown": {
        "semantic": 0.95,
        "skills": 0.90,
        "experience": 0.85
      }
    }
  ],
  "total": 150,
  "page": 1
}
```

- Error handling:
  - 401 if not authenticated
  - 404 if user profile not found
  - 400 for invalid filters

Add endpoint tests.
```

**verify the generated content:**
Test API: `curl -H "Authorization: Bearer $TOKEN" http://localhost:8000/api/v1/jobs/matches?limit=10`. Verify response format and authentication.

**desired output to verify:**
API endpoints return matched jobs, authentication works, rate limiting enforced, response format correct, tests pass.

**CI/CD:**
```yaml
- name: Test API endpoints
  run: |
    cd backend
    pytest tests/presentation/test_job_routes.py -v
```

**git commit message:**
```
feat(presentation): add job matching API endpoints with authentication
```

---

## Phase 9 – Resume & Cover Letter Generation
*Goal: Build AI-powered resume tailoring and cover letter generation system.*

### Step 9.1 – Setup LLM Service

**prompt:**
```
Create LLM service in backend/src/infrastructure/ai/llm_service.py:

- LLMService class:
  - generate_text(prompt: str, max_tokens: int = 1000) -> str
  - generate_with_template(template: str, variables: Dict) -> str
  - stream_generation(prompt: str) -> Iterator[str] (for streaming responses)

- Model options:
  - Primary: OpenAI GPT-4 (high quality)
  - Fallback: OpenAI GPT-3.5-turbo (faster, cheaper)
  - Alternative: Anthropic Claude (if available)
  - Configuration-based selection

- Features:
  - Temperature control (0.7 for creative, 0.3 for factual)
  - Token limits and truncation
  - Retry logic with exponential backoff
  - Rate limiting respect
  - Cost tracking per request

- Prompt management:
  - Load prompts from YAML files
  - Template variable substitution
  - Prompt versioning

- Error handling:
  - API failures with retries
  - Token limit exceeded
  - Invalid responses
  - Rate limit exceeded

Create unit tests with mocked API responses.
```

**verify the generated content:**
Test LLM service: `python -c "from backend.src.infrastructure.ai.llm_service import LLMService; llm = LLMService(); text = llm.generate_text('Write a short paragraph'); print(text)"`. Verify API calls work.

**desired output to verify:**
LLM service generates text, template substitution works, retry logic functional, error handling robust, tests pass.

**CI/CD:**
```yaml
- name: Test LLM service
  run: |
    cd backend
    pytest tests/infrastructure/test_llm_service.py -v
```

**git commit message:**
```
feat(infrastructure): setup LLM service with OpenAI and prompt management
```

---

### Step 9.2 – Implement Resume Tailoring Service

**prompt:**
```
Create resume tailoring service in backend/src/application/application/use_cases/generate_tailored_resume.py:

- GenerateTailoredResume use case:
  - execute(user_id: UserId, job_id: JobId) -> TailoredResume
  - extract_relevant_experience(profile: UserProfile, job: Job) -> List[Experience]
  - extract_relevant_skills(profile: UserProfile, job: Job) -> List[str]
  - generate_resume_text(profile: UserProfile, job: Job) -> str
  - save_resume(resume_text: str, format: str = 'pdf') -> str (S3 URL)

- Resume generation strategy:
  1. Parse user's base resume
  2. Extract job requirements and keywords
  3. Identify relevant experience and skills
  4. Reorder and emphasize matching content
  5. Add job-specific keywords naturally
  6. Generate formatted resume (PDF/DOCX)

- Prompt template:
```
You are a professional resume writer. Tailor this resume for the following job:

Job Title: {{job_title}}
Company: {{company_name}}
Job Description: {{job_description}}
Key Requirements: {{requirements}}

Candidate Resume:
{{base_resume}}

Instructions:
- Highlight experiences and skills that match the job
- Use keywords from the job description naturally
- Maintain professional tone
- Keep original formatting structure
- Do not fabricate experience
```

- Format generation:
  - Use reportlab or python-docx for PDF/DOCX
  - Preserve professional formatting
  - Support multiple templates

- Storage:
  - Save to S3 with unique filename
  - Store URL in applications table
  - Cache generated resumes (TTL: 7 days)

Create use case tests.
```

**verify the generated content:**
Test resume generation: `pytest backend/tests/application/test_generate_tailored_resume.py -v`. Verify resume is generated and saved to S3.

**desired output to verify:**
Resume tailoring works, relevant content extracted, LLM generates quality resumes, PDF generation functional, S3 upload works, tests pass.

**CI/CD:**
```yaml
- name: Test resume generation
  run: |
    cd backend
    pytest tests/application/test_generate_tailored_resume.py -v
```

**git commit message:**
```
feat(application): implement AI-powered resume tailoring service
```

---

### Step 9.3 – Implement Cover Letter Generation

**prompt:**
```
Create cover letter generator in backend/src/application/application/use_cases/generate_cover_letter.py:

- GenerateCoverLetter use case:
  - execute(user_id: UserId, job_id: JobId, tone: str = 'professional') -> CoverLetter
  - research_company(company_name: str) -> Dict (company info, values, recent news)
  - generate_cover_letter_text(profile: UserProfile, job: Job, company_info: Dict, tone: str) -> str
  - personalize_content(text: str, job: Job, profile: UserProfile) -> str

- Cover letter structure:
  1. Opening: Personalized greeting, job reference
  2. Introduction: Why interested in role/company
  3. Body: Relevant experience and skills (2-3 paragraphs)
  4. Closing: Enthusiasm, call to action

- Prompt template:
```
Write a professional cover letter for:

Candidate: {{candidate_name}}
Applying for: {{job_title}} at {{company_name}}

Company Information:
{{company_info}}

Job Description:
{{job_description}}

Candidate Background:
{{candidate_summary}}

Tone: {{tone}} (professional, enthusiastic, formal)

Requirements:
- 3-4 paragraphs
- Personalized to company and role
- Highlight relevant experience
- Show enthusiasm
- Professional closing
```

- Personalization:
  - Company research (web scraping or API)
  - Reference specific company values/projects
  - Match tone to company culture
  - Use job-specific keywords

- Tone options:
  - Professional (default)
  - Enthusiastic
  - Formal
  - Creative (for design roles)

- Storage:
  - Store in applications.cover_letter_text
  - Cache generated letters (TTL: 7 days)

Create use case tests.
```

**verify the generated content:**
Test cover letter generation: `pytest backend/tests/application/test_generate_cover_letter.py -v`. Verify letter is personalized and well-formatted.

**desired output to verify:**
Cover letters generated, company research works, personalization effective, tone variations work, storage functional, tests pass.

**CI/CD:**
```yaml
- name: Test cover letter generation
  run: |
    cd backend
    pytest tests/application/test_generate_cover_letter.py -v
```

**git commit message:**
```
feat(application): implement AI-powered cover letter generation with personalization
```

---

### Step 9.4 – Create Resume/Cover Letter API Endpoints

**prompt:**
```
Create API endpoints in backend/src/presentation/api/v1/routes/applications.py:

- POST /api/v1/applications/{job_id}/resume
  - Generate tailored resume for job
  - Request body: { "format": "pdf" }
  - Response: { "resume_url": "https://s3...", "generated_at": "..." }

- POST /api/v1/applications/{job_id}/cover-letter
  - Generate cover letter for job
  - Request body: { "tone": "professional" }
  - Response: { "cover_letter": "...", "generated_at": "..." }

- GET /api/v1/applications/{application_id}/documents
  - Get all generated documents for application
  - Response: { "resume_url": "...", "cover_letter": "..." }

- POST /api/v1/applications/{application_id}/regenerate
  - Regenerate resume or cover letter
  - Request body: { "type": "resume" | "cover_letter", "options": {...} }

- Authentication: Required (JWT)
- Rate limiting: 20 generations/hour per user
- Async processing: Return job ID, poll for completion

Add endpoint tests.
```

**verify the generated content:**
Test API: `curl -X POST -H "Authorization: Bearer $TOKEN" http://localhost:8000/api/v1/applications/{job_id}/resume`. Verify generation works and files are accessible.

**desired output to verify:**
API endpoints generate documents, authentication works, rate limiting enforced, async processing functional, tests pass.

**CI/CD:**
```yaml
- name: Test document generation API
  run: |
    cd backend
    pytest tests/presentation/test_application_routes.py -v
```

**git commit message:**
```
feat(presentation): add resume and cover letter generation API endpoints
```

---

## Phase 10 – Auto-Apply Engine
*Goal: Build automated job application submission system with browser automation.*

### Step 10.1 – Setup Browser Automation Framework

**prompt:**
```
Create browser automation framework in scrapers/src/automation/:

- BrowserAutomation class:
  - __init__(headless: bool = True)
  - navigate_to(url: str) -> None
  - fill_form(fields: Dict[str, str]) -> None
  - upload_file(file_path: str, selector: str) -> None
  - click_button(selector: str) -> None
  - wait_for_element(selector: str, timeout: int = 10) -> None
  - take_screenshot(path: str) -> None
  - close() -> None

- Implementation:
  - Use Playwright (preferred) or Selenium
  - Support Chrome, Firefox, Safari
  - Stealth mode (anti-detection)
  - Human-like interactions (typing delays, mouse movements)

- Features:
  - Cookie management
  - Session persistence
  - Proxy support
  - CAPTCHA detection and solving
  - Error recovery and retries

- Configuration:
  - Browser type selection
  - Timeout settings
  - Retry attempts
  - Screenshot on errors

Create base automation tests.
```

**verify the generated content:**
Test automation: `python -c "from scrapers.src.automation.browser_automation import BrowserAutomation; ba = BrowserAutomation(); ba.navigate_to('https://example.com'); ba.close()"`. Verify browser launches.

**desired output to verify:**
Browser automation works, form filling functional, file uploads work, stealth mode effective, error handling robust, tests pass.

**CI/CD:**
```yaml
- name: Test browser automation
  run: |
    cd scrapers
    pytest tests/automation/test_browser_automation.py -v
```

**git commit message:**
```
feat(automation): setup browser automation framework with Playwright
```

---

### Step 10.2 – Implement Application Form Parser

**prompt:**
```
Create application form parser in backend/src/infrastructure/automation/form_parser.py:

- FormParser class:
  - detect_form_type(page_html: str) -> str (Greenhouse, Lever, Workday, Custom)
  - extract_form_fields(page_html: str) -> List[FormField]
  - map_user_data_to_form(user_data: Dict, form_fields: List[FormField]) -> Dict
  - validate_form_completion(form_data: Dict) -> bool

- FormField dataclass:
  - name: str
  - type: str (text, email, file, select, etc.)
  - selector: str (CSS/XPath)
  - required: bool
  - label: str

- ATS detection:
  - Greenhouse: Detect greenhouse.io domain, specific form structure
  - Lever: Detect lever.co domain, API endpoints
  - Workday: Detect workday.com, complex multi-step forms
  - Custom: Generic form detection using common patterns

- Field mapping:
  - Name → first_name, last_name fields
  - Email → email field
  - Phone → phone field
  - Resume → file upload field
  - Cover letter → textarea field
  - Experience → dynamic fields (add rows)

- Validation:
  - Check all required fields filled
  - Validate email format
  - Verify file uploads successful
  - Check for error messages

Create parser tests with sample HTML forms.
```

**verify the generated content:**
Test form parser: `pytest backend/tests/infrastructure/test_form_parser.py -v`. Test with various ATS form HTML samples.

**desired output to verify:**
Form parser detects ATS types, extracts fields correctly, maps user data accurately, validation works, tests pass.

**CI/CD:**
```yaml
- name: Test form parser
  run: |
    cd backend
    pytest tests/infrastructure/test_form_parser.py -v
```

**git commit message:**
```
feat(infrastructure): implement application form parser with ATS detection
```

---

### Step 10.3 – Implement Auto-Apply Service

**prompt:**
```
Create auto-apply service in backend/src/application/application/use_cases/auto_apply.py:

- AutoApply use case:
  - execute(user_id: UserId, job_id: JobId, application_data: Dict) -> ApplicationResult
  - prepare_application_data(user: User, job: Job) -> Dict
  - submit_application(job: Job, application_data: Dict) -> ApplicationResult
  - handle_application_errors(error: Exception) -> None

- Application flow:
  1. Generate tailored resume and cover letter
  2. Navigate to job application page
  3. Parse application form
  4. Fill form fields with user data
  5. Upload resume and cover letter
  6. Handle additional questions
  7. Submit application
  8. Capture confirmation

- Error handling:
  - CAPTCHA detection → solve or flag for manual review
  - Form validation errors → retry with corrections
  - Network errors → retry with backoff
  - Unsupported forms → flag for manual application

- ApplicationResult:
  - success: bool
  - application_id: str (if successful)
  - confirmation_url: str
  - screenshots: List[str]
  - errors: List[str]
  - requires_manual_review: bool

- Background processing:
  - Celery task for async application submission
  - Queue management for rate limiting
  - Retry failed applications

- Safety features:
  - User confirmation before auto-applying
  - Daily application limits (configurable)
  - Duplicate application prevention
  - Application review queue

Create use case tests with mocked browser automation.
```

**verify the generated content:**
Test auto-apply: `pytest backend/tests/application/test_auto_apply.py -v`. Test with mock job application pages.

**desired output to verify:**
Auto-apply service submits applications, handles errors gracefully, captures confirmations, safety features work, tests pass.

**CI/CD:**
```yaml
- name: Test auto-apply
  run: |
    cd backend
    pytest tests/application/test_auto_apply.py -v
```

**git commit message:**
```
feat(application): implement auto-apply service with browser automation
```

---

### Step 10.4 – Create Application Tracking System

**prompt:**
```
Create application tracking in backend/src/application/application/use_cases/track_application_status.py:

- TrackApplicationStatus use case:
  - execute(application_id: ApplicationId) -> ApplicationStatus
  - check_application_status(application: Application) -> ApplicationStatus
  - parse_status_email(email: Email) -> ApplicationStatus
  - update_application_status(application: Application, status: ApplicationStatus) -> None

- Status tracking methods:
  1. Email monitoring: Parse application confirmation emails
  2. Portal checking: Login to company portals (if credentials provided)
  3. Link checking: Monitor application link for status changes
  4. Manual updates: User can update status manually

- Email parsing:
  - Monitor user's email (IMAP/Gmail API)
  - Detect application-related emails
  - Extract status information
  - Parse common email templates

- Status types:
  - SUBMITTED: Application sent
  - REVIEWED: Under review
  - INTERVIEW: Interview scheduled
  - REJECTED: Application rejected
  - ACCEPTED: Offer received
  - WITHDRAWN: User withdrew

- Background jobs:
  - Daily status check for all active applications
  - Email monitoring (every 6 hours)
  - Portal checking (weekly)

- Notifications:
  - Email notifications on status changes
  - In-app notifications
  - Dashboard updates

Create tracking tests.
```

**verify the generated content:**
Test tracking: `pytest backend/tests/application/test_track_application_status.py -v`. Test email parsing and status updates.

**desired output to verify:**
Status tracking works, email parsing functional, background jobs execute, notifications sent, tests pass.

**CI/CD:**
```yaml
- name: Test application tracking
  run: |
    cd backend
    pytest tests/application/test_track_application_status.py -v
```

**git commit message:**
```
feat(application): implement application status tracking with email monitoring
```

---

## Phase 11 – Frontend Dashboard
*Goal: Build modern, responsive frontend dashboard for job search and application management.*

### Step 11.1 – Setup Next.js Project Structure

**prompt:**
```
Create Next.js 14 project structure in frontend/:

```
frontend/
├── src/
│   ├── app/ (App Router)
│   │   ├── layout.tsx
│   │   ├── page.tsx (dashboard)
│   │   ├── jobs/
│   │   ├── applications/
│   │   ├── profile/
│   │   └── settings/
│   ├── components/
│   │   ├── ui/ (shadcn components)
│   │   ├── jobs/
│   │   ├── applications/
│   │   └── common/
│   ├── lib/
│   │   ├── api/ (API client)
│   │   ├── hooks/ (custom React hooks)
│   │   └── utils/
│   ├── store/ (Zustand stores)
│   └── types/ (TypeScript types)
├── public/
└── tailwind.config.js
```

- Setup:
  - Next.js 14 with App Router
  - TypeScript strict mode
  - TailwindCSS with custom theme
  - shadcn/ui component library
  - React Query for data fetching
  - Zustand for state management
  - Axios for HTTP client
  - React Hook Form + Zod for forms

- Configuration files:
  - next.config.js with optimizations
  - tsconfig.json with strict settings
  - tailwind.config.js with design system
  - .eslintrc.json
  - .prettierrc

Create initial layout and home page.
```

**verify the generated content:**
Run `cd frontend && npm install && npm run build`. Verify TypeScript compiles, TailwindCSS works, Next.js builds successfully.

**desired output to verify:**
Next.js project structure created, all dependencies installed, build succeeds, TypeScript configuration valid.

**CI/CD:**
```yaml
- name: Build frontend
  run: |
    cd frontend
    npm ci
    npm run build
```

**git commit message:**
```
chore(frontend): setup Next.js 14 project with TypeScript and TailwindCSS
```

---

### Step 11.2 – Implement Authentication UI

**prompt:**
```
Create authentication pages in frontend/src/app/auth/:

- login/page.tsx: Login form with email/password
- register/page.tsx: Registration form
- Components:
  - LoginForm: Email, password, remember me, forgot password
  - RegisterForm: Email, password, confirm password, terms acceptance
  - AuthLayout: Shared layout for auth pages

- Features:
  - Form validation with Zod
  - Error handling and display
  - Loading states
  - Redirect after successful auth
  - JWT token storage (httpOnly cookies)
  - Protected route wrapper

- API integration:
  - POST /api/v1/auth/login
  - POST /api/v1/auth/register
  - Token refresh handling
  - Logout functionality

- UI/UX:
  - Responsive design
  - Accessible forms (ARIA labels)
  - Password strength indicator
  - Social login buttons (optional)

Create authentication tests.
```

**verify the generated content:**
Start dev server: `cd frontend && npm run dev`. Navigate to `/auth/login`, test form submission, verify redirect works.

**desired output to verify:**
Login and register pages render, forms validate correctly, API integration works, authentication flow complete, tests pass.

**CI/CD:**
```yaml
- name: Test frontend build
  run: |
    cd frontend
    npm run build
    npm run lint
```

**git commit message:**
```
feat(frontend): implement authentication pages with form validation
```

---

### Step 11.3 – Create Job Feed Dashboard

**prompt:**
```
Create job feed dashboard in frontend/src/app/jobs/page.tsx:

- Components:
  - JobFeed: Infinite scroll job list
  - JobCard: Individual job display with match score
  - JobFilters: Search, location, salary, job type filters
  - JobSearchBar: Real-time search input

- Features:
  - Infinite scroll pagination
  - Real-time job updates (WebSocket)
  - Filter and search functionality
  - Sort by: relevance, date, salary
  - Match score display
  - Save jobs (bookmark)
  - Quick apply button

- Data fetching:
  - React Query for job list
  - Optimistic updates
  - Cache management
  - Background refetching

- UI/UX:
  - Responsive grid layout
  - Skeleton loaders
  - Empty states
  - Error states with retry
  - Toast notifications

- WebSocket integration:
  - Connect to /ws/jobs
  - Receive new job notifications
  - Update feed in real-time

Create component tests.
```

**verify the generated content:**
Navigate to `/jobs`, verify jobs load, test filters, check infinite scroll, verify WebSocket updates work.

**desired output to verify:**
Job feed displays jobs, filters work, infinite scroll functional, WebSocket updates real-time, UI responsive, tests pass.

**CI/CD:**
```yaml
- name: Test frontend components
  run: |
    cd frontend
    npm run test
```

**git commit message:**
```
feat(frontend): create job feed dashboard with real-time updates
```

---

### Step 11.4 – Implement Application Management UI

**prompt:**
```
Create application management in frontend/src/app/applications/:

- pages:
  - page.tsx: Application list with status filters
  - [id]/page.tsx: Application details
  - new/[job_id]/page.tsx: Create new application

- Components:
  - ApplicationList: Table/card view of applications
  - ApplicationCard: Status, job info, actions
  - ApplicationForm: Manual application creation
  - ApplicationTimeline: Status history
  - DocumentViewer: Resume and cover letter preview

- Features:
  - Filter by status
  - Sort by date, company
  - Status badges with colors
  - View generated documents
  - Edit application details
  - Track application timeline
  - Add notes
  - Delete/withdraw applications

- Actions:
  - Generate resume/cover letter
  - Submit application
  - Update status manually
  - Download documents

- UI/UX:
  - Status color coding
  - Progress indicators
  - Document preview modals
  - Confirmation dialogs
  - Toast notifications

Create component tests.
```

**verify the generated content:**
Navigate to `/applications`, verify list displays, test filters, create new application, verify document generation works.

**desired output to verify:**
Application management UI functional, status tracking works, document generation accessible, all actions work, tests pass.

**CI/CD:**
```yaml
- name: Test application UI
  run: |
    cd frontend
    npm run test -- applications
```

**git commit message:**
```
feat(frontend): implement application management UI with status tracking
```

---

### Step 11.5 – Create User Profile Page

**prompt:**
```
Create user profile page in frontend/src/app/profile/page.tsx:

- Components:
  - ProfileForm: Edit personal information
  - ResumeUpload: Upload and parse resume
  - SkillsEditor: Add/remove skills
  - ExperienceEditor: Add/edit work experience
  - EducationEditor: Add/edit education
  - PreferencesEditor: Job preferences (location, salary, etc.)

- Features:
  - Resume upload with parsing
  - Skills autocomplete
  - Experience timeline
  - Education history
  - Job preferences
  - Profile completion indicator
  - Preview profile

- Resume parsing:
  - Upload PDF/DOCX
  - Extract text
  - Parse sections (experience, education, skills)
  - Auto-fill profile fields

- Data management:
  - React Hook Form for forms
  - Zod validation
  - Auto-save drafts
  - Optimistic updates

- UI/UX:
  - Multi-step form wizard
  - Progress indicator
  - Form validation
  - Success/error messages
  - Profile preview mode

Create component tests.
```

**verify the generated content:**
Navigate to `/profile`, test form submission, upload resume, verify parsing works, check auto-save functionality.

**desired output to verify:**
Profile page functional, resume parsing works, forms validate, data saves correctly, UI responsive, tests pass.

**CI/CD:**
```yaml
- name: Test profile page
  run: |
    cd frontend
    npm run test -- profile
```

**git commit message:**
```
feat(frontend): create user profile page with resume parsing
```

---

## Phase 12 – Authentication & Authorization
*Goal: Implement secure authentication and authorization system.*

### Step 12.1 – Implement JWT Authentication

**prompt:**
```
Create JWT authentication in backend/src/infrastructure/auth/jwt_service.py:

- JWTService class:
  - generate_token(user_id: UserId, email: str) -> str
  - verify_token(token: str) -> Dict
  - refresh_token(refresh_token: str) -> str
  - decode_token(token: str) -> Dict

- Token configuration:
  - Access token: 15 minutes expiry
  - Refresh token: 7 days expiry
  - Secret key from environment
  - Algorithm: HS256

- Token payload:
  - user_id: UUID
  - email: str
  - exp: int (expiry)
  - iat: int (issued at)
  - type: str (access/refresh)

- Security:
  - Token blacklisting (Redis)
  - Token rotation on refresh
  - Secure cookie storage option
  - CORS configuration

- Error handling:
  - Expired token
  - Invalid token
  - Token not provided
  - Blacklisted token

Create JWT service tests.
```

**verify the generated content:**
Test JWT: `pytest backend/tests/infrastructure/test_jwt_service.py -v`. Test token generation, verification, refresh, blacklisting.

**desired output to verify:**
JWT tokens generated correctly, verification works, refresh functional, blacklisting effective, security measures in place, tests pass.

**CI/CD:**
```yaml
- name: Test JWT service
  run: |
    cd backend
    pytest tests/infrastructure/test_jwt_service.py -v
```

**git commit message:**
```
feat(infrastructure): implement JWT authentication service
```

---

### Step 12.2 – Create Authentication Middleware

**prompt:**
```
Create authentication middleware in backend/src/presentation/api/middleware/auth.py:

- AuthMiddleware class:
  - extract_token(request: Request) -> Optional[str]
  - verify_authentication(token: str) -> Optional[UserId]
  - get_current_user(request: Request) -> User

- FastAPI dependency:
  - get_current_user() -> User (dependency injection)
  - get_current_active_user() -> User (checks is_active)
  - get_optional_user() -> Optional[User] (for public endpoints)

- Middleware features:
  - Token extraction from header or cookie
  - Token verification
  - User lookup from database
  - Error responses (401 Unauthorized)
  - Rate limiting per user

- Protected routes:
  - Apply to all /api/v1/* routes except /auth/*
  - Optional auth for public endpoints
  - Role-based access (future)

- Error responses:
  - 401: Invalid/missing token
  - 403: User inactive or insufficient permissions
  - 429: Rate limit exceeded

Create middleware tests.
```

**verify the generated content:**
Test middleware: `pytest backend/tests/presentation/test_auth_middleware.py -v`. Test protected endpoints, token validation, error responses.

**desired output to verify:**
Middleware protects routes, token extraction works, user lookup functional, error responses correct, tests pass.

**CI/CD:**
```yaml
- name: Test auth middleware
  run: |
    cd backend
    pytest tests/presentation/test_auth_middleware.py -v
```

**git commit message:**
```
feat(presentation): implement authentication middleware with JWT verification
```

---

### Step 12.3 – Implement Password Security

**prompt:**
```
Enhance password security in backend/src/domain/user/value_objects.py:

- PasswordHash improvements:
  - Use bcrypt with cost factor 12
  - Password strength validation
  - Password history (prevent reuse)
  - Password expiration (optional)

- Password requirements:
  - Minimum 8 characters
  - At least one uppercase letter
  - At least one lowercase letter
  - At least one number
  - At least one special character
  - Not common password (check against list)

- Security features:
  - Rate limiting on login attempts
  - Account lockout after 5 failed attempts
  - Password reset tokens (expire in 1 hour)
  - Secure password reset flow
  - Password change requires current password

- Password reset:
  - Generate secure token
  - Send reset email
  - Validate token
  - Enforce new password requirements
  - Invalidate old sessions on password change

Create security tests.
```

**verify the generated content:**
Test password security: `pytest backend/tests/domain/test_password_security.py -v`. Test hashing, validation, reset flow, lockout.

**desired output to verify:**
Password hashing secure, validation works, reset flow functional, lockout effective, security measures enforced, tests pass.

**CI/CD:**
```yaml
- name: Test password security
  run: |
    cd backend
    pytest tests/domain/test_password_security.py -v
```

**git commit message:**
```
feat(domain): enhance password security with validation and reset flow
```

---

## Phase 13 – Monitoring & Observability
*Goal: Implement comprehensive monitoring, logging, and observability.*

### Step 13.1 – Setup Structured Logging

**prompt:**
```
Create logging infrastructure in backend/src/infrastructure/logging/:

- Logger configuration:
  - Structured JSON logging
  - Log levels: DEBUG, INFO, WARNING, ERROR, CRITICAL
  - Contextual logging (request ID, user ID)
  - Log rotation and retention

- LoggingService class:
  - log_request(request: Request, response: Response, duration: float)
  - log_error(error: Exception, context: Dict)
  - log_business_event(event: str, data: Dict)
  - log_performance(operation: str, duration: float, metadata: Dict)

- Log formats:
  - Development: Human-readable
  - Production: JSON for ELK stack
  - Include: timestamp, level, message, context, stack traces

- Integration:
  - Python logging with custom formatters
  - Correlation IDs for request tracing
  - User context injection
  - Error tracking (Sentry integration)

- Log destinations:
  - Console (development)
  - File (rotating)
  - ELK stack (production)
  - CloudWatch (AWS)

Create logging tests.
```

**verify the generated content:**
Test logging: Check log output, verify structured format, test error logging, verify correlation IDs.

**desired output to verify:**
Logging works correctly, structured format valid, context included, error tracking functional, tests pass.

**CI/CD:**
```yaml
- name: Test logging
  run: |
    cd backend
    pytest tests/infrastructure/test_logging.py -v
```

**git commit message:**
```
feat(infrastructure): setup structured logging with ELK stack integration
```

---

### Step 13.2 – Implement Metrics Collection

**prompt:**
```
Create metrics collection in backend/src/infrastructure/metrics/:

- MetricsService class:
  - increment_counter(name: str, tags: Dict)
  - record_histogram(name: str, value: float, tags: Dict)
  - set_gauge(name: str, value: float, tags: Dict)
  - record_timing(name: str, duration: float, tags: Dict)

- Key metrics:
  - HTTP requests: count, duration, status codes
  - Database queries: count, duration, errors
  - Scraper jobs: count, success rate, duration
  - Job matches: count, average score
  - Applications: count, success rate
  - Cache: hit rate, miss rate
  - Queue: size, processing time

- Integration:
  - Prometheus client library
  - Metrics endpoint: /metrics
  - Grafana dashboards
  - Alerting rules

- Performance metrics:
  - Response times (p50, p95, p99)
  - Throughput (requests/second)
  - Error rates
  - Resource usage (CPU, memory)

Create metrics tests.
```

**verify the generated content:**
Test metrics: Check `/metrics` endpoint, verify Prometheus format, test metric recording, check Grafana dashboards.

**desired output to verify:**
Metrics collected correctly, Prometheus endpoint works, dashboards display data, alerting functional, tests pass.

**CI/CD:**
```yaml
- name: Test metrics
  run: |
    cd backend
    curl http://localhost:8000/metrics | grep -q "http_requests_total"
```

**git commit message:**
```
feat(infrastructure): implement Prometheus metrics collection
```

---

### Step 13.3 – Setup Health Checks

**prompt:**
```
Create health check system in backend/src/presentation/api/routes/health.py:

- Health check endpoints:
  - GET /health: Basic health (always 200)
  - GET /health/ready: Readiness check (database, Redis, RabbitMQ)
  - GET /health/live: Liveness check (application running)

- Health checks:
  - Database: Connection test, query execution
  - Redis: Connection test, ping
  - RabbitMQ: Connection test, queue access
  - S3: Bucket access test
  - External APIs: OpenAI, 2Captcha connectivity

- Health status:
  - healthy: All checks pass
  - degraded: Some checks fail (non-critical)
  - unhealthy: Critical checks fail

- Response format:
```json
{
  "status": "healthy",
  "timestamp": "2025-01-10T12:00:00Z",
  "checks": {
    "database": {"status": "healthy", "response_time_ms": 5},
    "redis": {"status": "healthy", "response_time_ms": 2}
  }
}
```

- Integration:
  - Kubernetes liveness/readiness probes
  - Load balancer health checks
  - Monitoring alerts

Create health check tests.
```

**verify the generated content:**
Test health: `curl http://localhost:8000/health`, `curl http://localhost:8000/health/ready`. Verify all checks work.

**desired output to verify:**
Health endpoints return correct status, all checks functional, response format valid, Kubernetes integration works, tests pass.

**CI/CD:**
```yaml
- name: Test health checks
  run: |
    curl -f http://localhost:8000/health || exit 1
    curl -f http://localhost:8000/health/ready || exit 1
```

**git commit message:**
```
feat(presentation): implement health check endpoints with dependency verification
```

---

## Phase 14 – Performance Optimization & Caching
*Goal: Optimize system performance and implement caching strategies.*

### Step 14.1 – Implement Redis Caching Layer

**prompt:**
```
Create caching layer in backend/src/infrastructure/cache/redis_cache.py:

- CacheService class:
  - get(key: str) -> Optional[Any]
  - set(key: str, value: Any, ttl: int = 3600)
  - delete(key: str)
  - exists(key: str) -> bool
  - increment(key: str, amount: int = 1) -> int
  - get_or_set(key: str, callable: Callable, ttl: int) -> Any

- Cache strategies:
  - Cache-aside: Application manages cache
  - Write-through: Write to cache and DB
  - Write-behind: Write to cache, async to DB

- Cache keys:
  - User profile: `user:profile:{user_id}`
  - Job matches: `user:matches:{user_id}:{hash}`
  - Job details: `job:{job_id}`
  - Scraper results: `scraper:results:{source}:{hash}`

- TTL configuration:
  - User profiles: 1 hour
  - Job matches: 1 hour
  - Job details: 24 hours
  - Scraper results: 6 hours
  - Embeddings: 7 days

- Cache invalidation:
  - On user profile update
  - On job update
  - On new scrape results
  - Manual invalidation API

- Performance:
  - Connection pooling
  - Pipeline for batch operations
  - Compression for large values
  - Cluster support (Redis Cluster)

- Error handling:
  - Graceful degradation (fallback to DB)
  - Cache miss handling
  - Connection retry logic

Create cache service tests.
```

**verify the generated content:**
Test caching: `pytest backend/tests/infrastructure/test_redis_cache.py -v`. Test cache get/set, TTL, invalidation, error handling.

**desired output to verify:**
Cache service works correctly, TTL enforced, invalidation functional, error handling robust, performance optimized, tests pass.

**CI/CD:**
```yaml
- name: Test cache service
  run: |
    cd backend
    docker-compose up -d redis
    pytest tests/infrastructure/test_redis_cache.py -v
```

**git commit message:**
```
feat(infrastructure): implement Redis caching layer with TTL and invalidation
```

---

### Step 14.2 – Implement Database Query Optimization

**prompt:**
```
Optimize database queries in backend/src/infrastructure/database/:

- Query optimization:
  - Add missing indexes on frequently queried columns
  - Use database query analyzers (EXPLAIN ANALYZE)
  - Optimize N+1 queries with eager loading
  - Use select_related/prefetch_related for relationships
  - Implement query result pagination

- Index strategy:
  - Composite indexes for common query patterns
  - Partial indexes for filtered queries
  - GIN indexes for JSONB columns
  - B-tree indexes for range queries
  - Vector indexes for embedding searches

- Connection pooling:
  - Configure SQLAlchemy pool size
  - Set max_overflow and pool_timeout
  - Use connection pool pre-ping
  - Monitor pool usage

- Query patterns:
  - Batch inserts for bulk operations
  - Use transactions for multi-step operations
  - Avoid SELECT * (select only needed columns)
  - Use database functions for aggregations
  - Implement materialized views for analytics

- Performance monitoring:
  - Log slow queries (>100ms)
  - Track query execution times
  - Monitor database connection pool
  - Alert on query performance degradation

- Database maintenance:
  - Regular VACUUM and ANALYZE
  - Index maintenance jobs
  - Partition cleanup
  - Statistics updates

Create query optimization tests.
```

**verify the generated content:**
Run query analysis: `docker-compose exec postgres psql -U postgres -d CareerBlitz -c "EXPLAIN ANALYZE SELECT * FROM jobs WHERE source = 'indeed';"`. Check indexes: `\d+ jobs`.

**desired output to verify:**
Queries optimized, indexes created, connection pooling configured, slow query logging works, performance improved, tests pass.

**CI/CD:**
```yaml
- name: Test query optimization
  run: |
    cd backend
    pytest tests/infrastructure/test_database_queries.py -v
```

**git commit message:**
```
perf(infrastructure): optimize database queries with indexes and connection pooling
```

---

### Step 14.3 – Implement API Response Caching

**prompt:**
```
Create API response caching in backend/src/presentation/api/middleware/cache.py:

- ResponseCacheMiddleware:
  - cache_response(endpoint: str, ttl: int)
  - get_cached_response(request: Request) -> Optional[Response]
  - invalidate_cache(pattern: str)
  - cache_key_generator(request: Request) -> str

- Caching strategy:
  - Cache GET requests by default
  - Cache key: method + path + query params + user_id
  - TTL based on endpoint type
  - Conditional requests (ETag, Last-Modified)

- Cache headers:
  - Cache-Control: max-age, public/private
  - ETag for validation
  - Vary header for user-specific content
  - X-Cache-Status header

- Endpoint-specific caching:
  - Job list: 5 minutes
  - Job details: 1 hour
  - User profile: 30 minutes
  - Match results: 1 hour
  - Static content: 24 hours

- Cache invalidation:
  - On POST/PUT/DELETE to related resources
  - Manual invalidation endpoints
  - Time-based expiration
  - Pattern-based invalidation

- Edge caching:
  - CDN integration (CloudFront, Cloudflare)
  - Static asset caching
  - API response caching at edge

Create caching middleware tests.
```

**verify the generated content:**
Test caching: Make GET request, verify Cache-Control header, check Redis for cached response, test invalidation.

**desired output to verify:**
Response caching works, headers set correctly, invalidation functional, CDN integration ready, tests pass.

**CI/CD:**
```yaml
- name: Test response caching
  run: |
    cd backend
    pytest tests/presentation/test_cache_middleware.py -v
```

**git commit message:**
```
feat(presentation): implement API response caching with ETag support
```

---

### Step 14.4 – Implement Background Job Optimization

**prompt:**
```
Optimize Celery background jobs in backend/src/infrastructure/messaging/:

- Job optimization:
  - Batch processing for similar tasks
  - Priority queues for urgent jobs
  - Task result expiration
  - Task deduplication (idempotency)
  - Chunk large tasks into smaller ones

- Queue management:
  - Separate queues by priority
  - Queue monitoring and alerting
  - Dead letter queue handling
  - Queue length monitoring
  - Auto-scaling workers based on queue size

- Performance improvements:
  - Use task result backend efficiently
  - Implement task result compression
  - Use task routing for load balancing
  - Optimize task serialization
  - Reduce task payload size

- Monitoring:
  - Track task execution times
  - Monitor queue lengths
  - Alert on stuck tasks
  - Track task success/failure rates
  - Resource usage per task type

- Optimization techniques:
  - Use database bulk operations
  - Parallel task execution where possible
  - Cache intermediate results
  - Use database transactions efficiently
  - Implement task result caching

Create job optimization tests.
```

**verify the generated content:**
Monitor Celery: `celery -A backend.src.infrastructure.messaging.celery_app inspect active`. Check queue lengths and task execution times.

**desired output to verify:**
Jobs optimized, queues managed efficiently, monitoring functional, performance improved, tests pass.

**CI/CD:**
```yaml
- name: Test job optimization
  run: |
    cd backend
    celery -A src.infrastructure.messaging.celery_app inspect stats
```

**git commit message:**
```
perf(infrastructure): optimize Celery background jobs with batching and priority queues
```

---

## Phase 15 – Deployment & Scaling
*Goal: Deploy application to production with auto-scaling and high availability.*

### Step 15.1 – Create Docker Production Images

**prompt:**
```
Create production Dockerfiles in each service directory:

- Multi-stage builds:
  - Build stage: Install dependencies, compile
  - Runtime stage: Minimal base image
  - Security: Non-root user, minimal packages

- Backend Dockerfile:
  - Base: python:3.11-slim
  - Install system dependencies
  - Copy requirements and install
  - Copy application code
  - Set working directory
  - Expose port 8000
  - Health check
  - Non-root user

- Frontend Dockerfile:
  - Build stage: Node 20, install and build
  - Runtime stage: nginx:alpine
  - Copy built files to nginx
  - Configure nginx for SPA
  - Health check

- Scrapers Dockerfile:
  - Base: python:3.11-slim
  - Install Playwright browsers
  - Copy scraper code
  - Set entrypoint

- Docker Compose production:
  - Environment-specific configs
  - Resource limits
  - Health checks
  - Restart policies
  - Network configuration

- Image optimization:
  - Use .dockerignore
  - Layer caching
  - Multi-stage builds
  - Minimal base images
  - Remove build dependencies

Create .dockerignore files for each service.
```

**verify the generated content:**
Build images: `docker build -t CareerBlitz-backend:latest backend/`. Test: `docker run -p 8000:8000 CareerBlitz-backend:latest`. Check image size.

**desired output to verify:**
Docker images build successfully, optimized size, health checks work, non-root users configured, production-ready.

**CI/CD:**
```yaml
- name: Build Docker images
  run: |
    docker build -t CareerBlitz-backend:${{ github.sha }} backend/
    docker build -t CareerBlitz-frontend:${{ github.sha }} frontend/
```

**git commit message:**
```
feat: create production Docker images with multi-stage builds
```

---

### Step 15.2 – Setup Kubernetes Deployment

**prompt:**
```
Create Kubernetes manifests in infrastructure/kubernetes/:

- Namespace: CareerBlitz-production
- Deployments:
  - backend-deployment.yaml (3 replicas)
  - frontend-deployment.yaml (2 replicas)
  - scrapers-deployment.yaml (5 replicas)
  - celery-worker-deployment.yaml (3 replicas)
  - celery-beat-deployment.yaml (1 replica)

- Services:
  - backend-service.yaml (ClusterIP)
  - frontend-service.yaml (ClusterIP)
  - LoadBalancer for external access

- ConfigMaps:
  - app-config.yaml (environment variables)
  - nginx-config.yaml

- Secrets:
  - database-credentials
  - api-keys
  - jwt-secret

- Ingress:
  - ingress.yaml with TLS
  - Domain configuration
  - Path-based routing

- HorizontalPodAutoscaler:
  - Backend: 3-10 replicas (CPU 70%)
  - Scrapers: 5-20 replicas (queue length)
  - Workers: 3-10 replicas (CPU 70%)

- Resource limits:
  - CPU and memory requests/limits
  - Storage volumes
  - Network policies

- Health checks:
  - Liveness probes
  - Readiness probes
  - Startup probes

Create kustomization.yaml for environment management.
```

**verify the generated content:**
Apply manifests: `kubectl apply -f infrastructure/kubernetes/`. Check pods: `kubectl get pods -n CareerBlitz-production`. Verify HPA: `kubectl get hpa`.

**desired output to verify:**
Kubernetes deployments created, pods running, services accessible, HPA configured, health checks working, ingress functional.

**CI/CD:**
```yaml
- name: Deploy to Kubernetes
  run: |
    kubectl apply -f infrastructure/kubernetes/
    kubectl rollout status deployment/backend -n CareerBlitz-production
```

**git commit message:**
```
feat(infrastructure): setup Kubernetes deployment with auto-scaling
```

---

### Step 15.3 – Setup Database High Availability

**prompt:**
```
Configure PostgreSQL high availability:

- Primary-replica setup:
  - Primary database (write)
  - Read replicas (2-3 instances)
  - Automatic failover
  - Connection pooling (PgBouncer)

- Database configuration:
  - Connection string with read/write separation
  - Read replica selection (round-robin)
  - Write to primary only
  - Read from replicas

- Backup strategy:
  - Daily full backups
  - Continuous WAL archiving
  - Point-in-time recovery
  - Backup retention (30 days)
  - Automated backup testing

- Monitoring:
  - Replication lag monitoring
  - Primary health checks
  - Automatic failover triggers
  - Backup success monitoring

- Disaster recovery:
  - Cross-region replication
  - Backup restoration procedures
  - RTO/RPO targets
  - DR runbook

- Managed database options:
  - AWS RDS with Multi-AZ
  - Google Cloud SQL with replicas
  - Azure Database with geo-replication

Update application to use read/write splitting.
```

**verify the generated content:**
Test read/write splitting: Verify writes go to primary, reads from replicas. Check replication lag. Test failover.

**desired output to verify:**
Database HA configured, read/write splitting works, backups automated, monitoring functional, failover tested.

**CI/CD:**
```yaml
- name: Test database HA
  run: |
    # Verify primary and replicas
    psql $PRIMARY_DB_URL -c "SELECT version();"
    psql $REPLICA_DB_URL -c "SELECT version();"
```

**git commit message:**
```
feat(infrastructure): setup PostgreSQL high availability with read replicas
```

---

### Step 15.4 – Implement Auto-Scaling

**prompt:**
```
Create auto-scaling configuration:

- Kubernetes HPA:
  - CPU-based scaling (70% threshold)
  - Memory-based scaling (80% threshold)
  - Custom metrics (queue length, request rate)
  - Scaling policies (scale up fast, scale down slow)

- Application-level scaling:
  - Celery worker auto-scaling based on queue length
  - Scraper worker scaling based on job backlog
  - API server scaling based on request rate

- Scaling triggers:
  - Request rate > 1000/min per pod
  - Queue length > 1000 tasks
  - CPU usage > 70% for 5 minutes
  - Memory usage > 80% for 5 minutes

- Scaling limits:
  - Min replicas: 3 (backend), 5 (scrapers)
  - Max replicas: 20 (backend), 50 (scrapers)
  - Scale up: +2 replicas per step
  - Scale down: -1 replica per step, 10min cooldown

- Monitoring:
  - Track scaling events
  - Monitor resource usage
  - Alert on scaling failures
  - Cost tracking per service

- Cost optimization:
  - Use spot instances for scrapers
  - Right-size resource requests
  - Schedule scaling based on usage patterns

Create scaling tests and load testing scenarios.
```

**verify the generated content:**
Load test: Generate high traffic, verify auto-scaling triggers, check HPA status, verify pods scale up/down.

**desired output to verify:**
Auto-scaling works, HPA configured correctly, scaling triggers functional, cost optimized, monitoring in place.

**CI/CD:**
```yaml
- name: Test auto-scaling
  run: |
    kubectl get hpa -n CareerBlitz-production
    # Run load test
    # Verify scaling occurs
```

**git commit message:**
```
feat(infrastructure): implement auto-scaling with Kubernetes HPA and custom metrics
```

---

### Step 15.5 – Setup CI/CD Pipeline for Production

**prompt:**
```
Create production CI/CD pipeline in .github/workflows/deploy-production.yml:

- Pipeline stages:
  1. Build: Compile and test
  2. Security scan: Dependency and container scanning
  3. Build images: Docker images with tags
  4. Push to registry: Container registry (GHCR/Docker Hub)
  5. Deploy to staging: Automatic deployment
  6. Integration tests: E2E tests on staging
  7. Deploy to production: Manual approval required
  8. Post-deployment: Health checks, smoke tests

- Deployment strategy:
  - Blue-green deployment
  - Rolling updates with health checks
  - Canary releases (10% → 50% → 100%)
  - Rollback on failure

- Environment management:
  - Separate configs for staging/production
  - Secret management (GitHub Secrets, Vault)
  - Environment-specific variables
  - Feature flags

- Deployment automation:
  - Automatic staging deployments
  - Manual production approval
  - Rollback automation
  - Database migration handling

- Monitoring:
  - Deployment notifications (Slack, email)
  - Deployment metrics
  - Post-deployment verification
  - Error tracking

Create deployment runbooks and rollback procedures.
```

**verify the generated content:**
Trigger deployment: Push to main branch, verify pipeline runs, check staging deployment, test production approval flow.

**desired output to verify:**
CI/CD pipeline functional, deployments automated, rollback works, monitoring integrated, documentation complete.

**CI/CD:**
This step creates the CI/CD pipeline itself. Verify in GitHub Actions.

**git commit message:**
```
ci: setup production CI/CD pipeline with blue-green deployment
```

---

## Phase 16 – Security Hardening
*Goal: Implement comprehensive security measures for production.*

### Step 16.1 – Implement Rate Limiting

**prompt:**
```
Create rate limiting in backend/src/presentation/api/middleware/rate_limit.py:

- RateLimiter class:
  - check_rate_limit(request: Request, endpoint: str) -> bool
  - get_remaining_requests(user_id: str, endpoint: str) -> int
  - reset_rate_limit(user_id: str, endpoint: str)

- Rate limit strategies:
  - Fixed window: Simple counter per time window
  - Sliding window: More accurate, Redis-based
  - Token bucket: Burst allowance
  - Leaky bucket: Smooth rate limiting

- Rate limit rules:
  - Authentication: 5 attempts/minute per IP
  - API endpoints: 100 requests/hour per user
  - Job matching: 50 requests/hour per user
  - Document generation: 20 requests/hour per user
  - Scraper triggers: 10 requests/hour per user

- Implementation:
  - Redis-based rate limiting
  - Per-user and per-IP limits
  - Endpoint-specific limits
  - Whitelist for internal services

- Response headers:
  - X-RateLimit-Limit
  - X-RateLimit-Remaining
  - X-RateLimit-Reset
  - 429 Too Many Requests status

- Error handling:
  - Graceful degradation
  - Retry-After header
  - User-friendly error messages

Create rate limiting tests.
```

**verify the generated content:**
Test rate limiting: Make requests, verify 429 response, check headers, test different endpoints and limits.

**desired output to verify:**
Rate limiting works, headers set correctly, Redis integration functional, error responses proper, tests pass.

**CI/CD:**
```yaml
- name: Test rate limiting
  run: |
    cd backend
    pytest tests/presentation/test_rate_limit.py -v
```

**git commit message:**
```
feat(presentation): implement rate limiting with Redis and sliding window
```

---

### Step 16.2 – Implement Input Validation & Sanitization

**prompt:**
```
Enhance input validation in backend/src/presentation/api/:

- Validation layers:
  - Pydantic models for request validation
  - SQL injection prevention (parameterized queries)
  - XSS prevention (output encoding)
  - Path traversal prevention
  - Command injection prevention

- Validation rules:
  - String length limits
  - Type validation
  - Format validation (email, URL, phone)
  - Content validation (file types, sizes)
  - Business rule validation

- Sanitization:
  - HTML sanitization (bleach library)
  - SQL sanitization (ORM parameterization)
  - File upload validation
  - Filename sanitization
  - URL validation

- Security headers:
  - Content-Security-Policy
  - X-Frame-Options
  - X-Content-Type-Options
  - X-XSS-Protection
  - Strict-Transport-Security

- File upload security:
  - File type validation (whitelist)
  - File size limits
  - Virus scanning
  - Secure file storage
  - Filename sanitization

- API security:
  - Request size limits
  - Query parameter validation
  - Path parameter validation
  - Body validation
  - Header validation

Create security validation tests.
```

**verify the generated content:**
Test validation: Submit invalid inputs, verify rejection, test SQL injection attempts, XSS attempts, file upload restrictions.

**desired output to verify:**
Input validation robust, sanitization effective, security headers set, file uploads secure, tests pass.

**CI/CD:**
```yaml
- name: Test input validation
  run: |
    cd backend
    pytest tests/presentation/test_security_validation.py -v
```

**git commit message:**
```
feat(presentation): enhance input validation and sanitization with security headers
```

---

### Step 16.3 – Setup Security Monitoring

**prompt:**
```
Implement security monitoring in backend/src/infrastructure/security/:

- SecurityEventLogger:
  - log_failed_login(ip: str, email: str)
  - log_suspicious_activity(event: str, context: Dict)
  - log_security_violation(violation: str, details: Dict)
  - log_rate_limit_exceeded(endpoint: str, user_id: str)

- Security events to monitor:
  - Failed authentication attempts
  - Rate limit violations
  - Unauthorized access attempts
  - SQL injection attempts
  - XSS attempts
  - File upload violations
  - Unusual API usage patterns

- Alerting:
  - Real-time alerts for critical events
  - Daily security summary
  - Anomaly detection
  - IP reputation checking

- Integration:
  - SIEM integration (Splunk, ELK)
  - Security information sharing
  - Threat intelligence feeds
  - Incident response automation

- Compliance:
  - Audit logging
  - Data access logging
  - Security event retention (1 year)
  - Compliance reporting

- Threat detection:
  - Brute force detection
  - Account takeover detection
  - DDoS detection
  - Bot detection

Create security monitoring tests.
```

**verify the generated content:**
Test monitoring: Trigger security events, verify logging, check alerts, test anomaly detection.

**desired output to verify:**
Security monitoring functional, events logged correctly, alerts triggered, compliance met, tests pass.

**CI/CD:**
```yaml
- name: Test security monitoring
  run: |
    cd backend
    pytest tests/infrastructure/test_security_monitoring.py -v
```

**git commit message:**
```
feat(infrastructure): implement security monitoring with threat detection
```

---

### Step 16.4 – Implement Data Encryption

**prompt:**
```
Setup data encryption in backend/src/infrastructure/security/:

- EncryptionService:
  - encrypt_sensitive_data(data: str) -> str
  - decrypt_sensitive_data(encrypted: str) -> str
  - encrypt_at_rest(data: bytes) -> bytes
  - decrypt_at_rest(encrypted: bytes) -> bytes

- Encryption strategies:
  - TLS/SSL for data in transit
  - AES-256 for data at rest
  - Field-level encryption for PII
  - Database encryption (TDE)

- Key management:
  - AWS KMS / Google Cloud KMS
  - Key rotation policies
  - Key versioning
  - Secure key storage

- Data to encrypt:
  - User passwords (already hashed)
  - API keys and secrets
  - Email addresses (optional)
  - Phone numbers (optional)
  - Resume files
  - Application data

- Database encryption:
  - Encrypted connections (SSL)
  - Encrypted backups
  - Encrypted storage volumes
  - Transparent data encryption

- Compliance:
  - GDPR compliance (data encryption)
  - PCI DSS (if handling payments)
  - HIPAA (if handling health data)

Create encryption tests.
```

**verify the generated content:**
Test encryption: Encrypt/decrypt data, verify keys managed securely, test key rotation, check database encryption.

**desired output to verify:**
Encryption functional, key management secure, database encrypted, compliance met, tests pass.

**CI/CD:**
```yaml
- name: Test encryption
  run: |
    cd backend
    pytest tests/infrastructure/test_encryption.py -v
```

**git commit message:**
```
feat(infrastructure): implement data encryption with KMS integration
```

---

## Phase 17 – Testing & Quality Assurance
*Goal: Implement comprehensive testing strategy.*

### Step 17.1 – Setup Test Infrastructure

**prompt:**
```
Create test infrastructure:

- Test structure:
  - Unit tests: tests/unit/
  - Integration tests: tests/integration/
  - E2E tests: tests/e2e/
  - Performance tests: tests/performance/

- Test configuration:
  - pytest.ini with markers
  - conftest.py with fixtures
  - Test database setup
  - Mock services configuration
  - Test data factories

- Test utilities:
  - Database fixtures (test DB, migrations)
  - API client fixtures
  - Mock external services
  - Test data generators
  - Assertion helpers

- Test coverage:
  - Minimum 80% code coverage
  - Coverage reporting (coverage.py)
  - Coverage badges
  - Exclude migrations and configs

- Test execution:
  - Fast unit tests (<1s each)
  - Parallel test execution
  - Test isolation
  - Cleanup after tests

- CI integration:
  - Run tests on every PR
  - Fail on coverage drop
  - Test reports and artifacts
  - Performance regression tests

Create test infrastructure and example tests.
```

**verify the generated content:**
Run tests: `pytest backend/tests/ -v --cov`. Check coverage report, verify test structure, run all test types.

**desired output to verify:**
Test infrastructure complete, fixtures work, coverage meets threshold, tests run efficiently, CI integrated.

**CI/CD:**
```yaml
- name: Run tests
  run: |
    cd backend
    pytest tests/ -v --cov=src --cov-report=xml
    coverage report --fail-under=80
```

**git commit message:**
```
test: setup comprehensive test infrastructure with coverage reporting
```

---

### Step 17.2 – Create Integration Tests

**prompt:**
```
Create integration tests in backend/tests/integration/:

- API integration tests:
  - Test all endpoints
  - Test authentication flow
  - Test authorization
  - Test error handling
  - Test rate limiting

- Database integration tests:
  - Test repository methods
  - Test transactions
  - Test migrations
  - Test data integrity

- External service integration:
  - Test Redis caching
  - Test RabbitMQ messaging
  - Test S3 storage
  - Test email sending (mocked)

- End-to-end workflows:
  - User registration → profile → job match → application
  - Scraper → normalization → deduplication → storage
  - Resume generation → application submission

- Test data:
  - Fixtures for common scenarios
  - Factories for test data generation
  - Database seeding
  - Cleanup procedures

- Test environment:
  - Docker Compose for services
  - Test database
  - Mock external APIs
  - Isolated test execution

Create comprehensive integration test suite.
```

**verify the generated content:**
Run integration tests: `pytest backend/tests/integration/ -v`. Verify all workflows tested, services integrated correctly.

**desired output to verify:**
Integration tests comprehensive, all workflows covered, services integrated, tests reliable, CI passes.

**CI/CD:**
```yaml
- name: Run integration tests
  run: |
    docker-compose -f docker-compose.test.yml up -d
    pytest backend/tests/integration/ -v
    docker-compose -f docker-compose.test.yml down
```

**git commit message:**
```
test: add comprehensive integration test suite
```

---

### Step 17.3 – Create E2E Tests

**prompt:**
```
Create E2E tests in tests/e2e/:

- E2E test framework:
  - Playwright for browser automation
  - Test against staging environment
  - Screenshot on failure
  - Video recording

- Test scenarios:
  - User registration and login
  - Profile creation and resume upload
  - Job search and filtering
  - Job matching and application
  - Resume and cover letter generation
  - Application submission
  - Application tracking

- Test data management:
  - Test user accounts
  - Test job postings
  - Cleanup after tests
  - Data isolation

- Test execution:
  - Run in CI on staging deployments
  - Run before production deployment
  - Parallel execution
  - Retry on flaky tests

- Reporting:
  - Test reports with screenshots
  - Video recordings
  - Performance metrics
  - Test coverage

Create E2E test suite with critical user journeys.
```

**verify the generated content:**
Run E2E tests: `pytest tests/e2e/ --headed`. Verify browser automation works, all scenarios pass, reports generated.

**desired output to verify:**
E2E tests functional, critical journeys covered, screenshots captured, reports generated, CI integrated.

**CI/CD:**
```yaml
- name: Run E2E tests
  run: |
    npm install -g playwright
    playwright install
    pytest tests/e2e/ -v
```

**git commit message:**
```
test: add E2E test suite with Playwright
```

---

### Step 17.4 – Setup Load Testing

**prompt:**
```
Create load testing setup:

- Load testing tools:
  - Locust for Python-based load tests
  - k6 for JavaScript-based tests
  - Artillery for API load testing

- Load test scenarios:
  - API endpoint load tests
  - Concurrent user simulation
  - Job matching under load
  - Scraper performance
  - Database query performance

- Performance targets:
  - API response time: <200ms (p95)
  - Job matching: <500ms (p95)
  - Database queries: <100ms (p95)
  - Throughput: 1000 req/s

- Load test configuration:
  - Ramp-up users gradually
  - Sustained load periods
  - Spike tests
  - Stress tests
  - Endurance tests

- Monitoring during tests:
  - Application metrics
  - Database performance
  - Resource usage
  - Error rates

- Test reports:
  - Response time percentiles
  - Throughput metrics
  - Error rates
  - Resource utilization

Create load test scripts and documentation.
```

**verify the generated content:**
Run load test: `locust -f tests/load/api_load_test.py --host=https://staging.CareerBlitz.com`. Monitor metrics, verify targets met.

**desired output to verify:**
Load tests functional, performance targets met, monitoring works, reports generated, bottlenecks identified.

**CI/CD:**
```yaml
- name: Run load tests
  run: |
    pip install locust
    locust -f tests/load/ --headless -u 100 -r 10 -t 5m
```

**git commit message:**
```
test: add load testing suite with performance targets
```

---

## Phase 18 – Documentation
*Goal: Create comprehensive documentation for the system.*

### Step 18.1 – Create API Documentation

**prompt:**
```
Create comprehensive API documentation:

- OpenAPI/Swagger specification:
  - Complete API endpoint definitions
  - Request/response schemas
  - Authentication requirements
  - Error responses
  - Example requests/responses

- API documentation features:
  - Interactive Swagger UI
  - Postman collection
  - Code examples (Python, JavaScript)
  - Authentication guide
  - Rate limiting documentation

- Endpoint documentation:
  - Description and purpose
  - Parameters and query strings
  - Request body schemas
  - Response formats
  - Status codes
  - Error handling

- Integration guides:
  - Getting started guide
  - Authentication setup
  - Common use cases
  - Best practices
  - Troubleshooting

- API versioning:
  - Version strategy
  - Deprecation policy
  - Migration guides

Generate OpenAPI spec and Swagger UI.
```

**verify the generated content:**
Access Swagger UI: `http://localhost:8000/docs`. Verify all endpoints documented, examples work, interactive testing functional.

**desired output to verify:**
API documentation complete, Swagger UI functional, examples accurate, integration guides helpful, versioning clear.

**CI/CD:**
```yaml
- name: Validate API docs
  run: |
    cd backend
    python -c "from src.presentation.main import app; import json; print(json.dumps(app.openapi()))"
```

**git commit message:**
```
docs: create comprehensive API documentation with Swagger UI
```

---

### Step 18.2 – Create Architecture Documentation

**prompt:**
```
Create architecture documentation in docs/architecture/:

- System architecture:
  - High-level architecture diagram
  - Component diagrams
  - Data flow diagrams
  - Sequence diagrams for key flows

- Technology stack:
  - Technology choices and rationale
  - Version information
  - Dependency management
  - Upgrade procedures

- Design patterns:
  - Clean Architecture explanation
  - Domain-Driven Design
  - Repository pattern
  - Dependency injection

- Scalability:
  - Scaling strategies
  - Performance optimizations
  - Caching strategies
  - Database sharding (if applicable)

- Security architecture:
  - Security measures
  - Authentication/authorization
  - Data encryption
  - Compliance

- Deployment architecture:
  - Infrastructure setup
  - Kubernetes configuration
  - CI/CD pipeline
  - Monitoring setup

Create Mermaid diagrams for all architectures.
```

**verify the generated content:**
Review documentation: Check diagrams render, verify accuracy, test links, ensure completeness.

**desired output to verify:**
Architecture documentation complete, diagrams accurate, patterns explained, scalability documented, security covered.

**CI/CD:**
```yaml
- name: Check documentation
  run: |
    # Verify markdown files exist
    test -f docs/architecture/overview.md
```

**git commit message:**
```
docs: create comprehensive architecture documentation with diagrams
```

---

### Step 18.3 – Create Developer Guide

**prompt:**
```
Create developer guide in docs/developer/:

- Getting started:
  - Prerequisites
  - Local setup instructions
  - Development environment
  - First contribution guide

- Development workflow:
  - Git workflow
  - Branch naming
  - Commit conventions
  - PR process
  - Code review guidelines

- Code standards:
  - Coding style guide
  - Type hints
  - Documentation standards
  - Testing requirements

- Project structure:
  - Directory organization
  - File naming conventions
  - Module organization
  - Dependency management

- Common tasks:
  - Adding new features
  - Adding new scrapers
  - Database migrations
  - API endpoint creation
  - Frontend component creation

- Debugging:
  - Local debugging setup
  - Logging
  - Error tracking
  - Performance profiling

- Testing:
  - Running tests
  - Writing tests
  - Test coverage
  - E2E testing

Create comprehensive developer guide.
```

**verify the generated content:**
Follow guide: New developer should be able to set up environment and make first contribution using only the guide.

**desired output to verify:**
Developer guide complete, setup instructions work, workflows clear, examples helpful, troubleshooting covered.

**CI/CD:**
```yaml
- name: Validate developer guide
  run: |
    # Check all required sections exist
    test -f docs/developer/getting-started.md
```

**git commit message:**
```
docs: create comprehensive developer guide
```

---

### Step 18.4 – Create Operations Runbook

**prompt:**
```
Create operations runbook in docs/operations/:

- Deployment procedures:
  - Staging deployment
  - Production deployment
  - Rollback procedures
  - Database migrations

- Monitoring:
  - Key metrics to monitor
  - Alert thresholds
  - Dashboard locations
  - Log locations

- Troubleshooting:
  - Common issues and solutions
  - Error code reference
  - Performance issues
  - Database issues
  - Scraper issues

- Maintenance:
  - Regular maintenance tasks
  - Database maintenance
  - Cache cleanup
  - Log rotation
  - Backup verification

- Incident response:
  - Incident response procedures
  - Escalation paths
  - Communication templates
  - Post-incident review

- Disaster recovery:
  - Backup procedures
  - Recovery procedures
  - RTO/RPO targets
  - DR testing

- Scaling procedures:
  - Manual scaling
  - Auto-scaling configuration
  - Resource planning
  - Cost optimization

Create comprehensive operations runbook.
```

**verify the generated content:**
Review runbook: Verify all procedures documented, test deployment steps, check troubleshooting guides.

**desired output to verify:**
Operations runbook complete, procedures accurate, troubleshooting helpful, incident response clear, maintenance documented.

**CI/CD:**
```yaml
- name: Validate runbook
  run: |
    test -f docs/operations/deployment.md
    test -f docs/operations/troubleshooting.md
```

**git commit message:**
```
docs: create operations runbook with deployment and troubleshooting procedures
```

---

## Final Deployment Checklist

**prompt:**
```
Create final deployment checklist in docs/deployment-checklist.md:

Pre-deployment:
- [ ] All tests passing (unit, integration, E2E)
- [ ] Code coverage >80%
- [ ] Security scan passed
- [ ] Performance tests passed
- [ ] Documentation updated
- [ ] Database migrations tested
- [ ] Environment variables configured
- [ ] Secrets stored securely
- [ ] Backup procedures verified

Infrastructure:
- [ ] Kubernetes cluster provisioned
- [ ] Database cluster configured with HA
- [ ] Redis cluster configured
- [ ] RabbitMQ cluster configured
- [ ] S3 buckets created
- [ ] Load balancer configured
- [ ] DNS records configured
- [ ] SSL certificates installed
- [ ] Monitoring setup complete
- [ ] Logging setup complete
- [ ] Alerting configured

Application:
- [ ] Docker images built and pushed
- [ ] Kubernetes manifests applied
- [ ] ConfigMaps and Secrets created
- [ ] Ingress configured
- [ ] Health checks working
- [ ] Auto-scaling configured
- [ ] Resource limits set
- [ ] Environment variables set

Services:
- [ ] Backend API deployed and healthy
- [ ] Frontend deployed and accessible
- [ ] Scrapers deployed and running
- [ ] Celery workers deployed
- [ ] Celery beat scheduled
- [ ] Background jobs processing

Verification:
- [ ] Health endpoints responding
- [ ] API endpoints functional
- [ ] Authentication working
- [ ] Database connections working
- [ ] Cache working
- [ ] Queue processing
- [ ] Scrapers executing
- [ ] Job matching working
- [ ] Document generation working

Monitoring:
- [ ] Metrics collection working
- [ ] Logs flowing to ELK
- [ ] Alerts configured
- [ ] Dashboards created
- [ ] Error tracking setup

Security:
- [ ] HTTPS enforced
- [ ] Security headers set
- [ ] Rate limiting active
- [ ] Input validation working
- [ ] Authentication required
- [ ] Encryption configured
- [ ] Secrets secured

Post-deployment:
- [ ] Smoke tests passed
- [ ] Load test passed
- [ ] Monitoring verified
- [ ] Team notified
- [ ] Documentation published
- [ ] Support channels ready

Rollback plan:
- [ ] Previous version tagged
- [ ] Rollback procedure documented
- [ ] Database rollback tested
- [ ] Rollback automation ready

Create comprehensive deployment checklist.
```

**verify the generated content:**
Use checklist: Go through each item, verify completion, test deployment, verify all systems operational.

**desired output to verify:**
Deployment checklist complete, all items verifiable, rollback plan ready, team can deploy confidently.

**CI/CD:**
```yaml
- name: Validate deployment checklist
  run: |
    test -f docs/deployment-checklist.md
    # Verify checklist is comprehensive
```

**git commit message:**
```
docs: create final deployment checklist
```

---

## Phase 19 – Post-Launch Product Readiness Assessment
*Goal: Evaluate product readiness for company launch and identify enhancement opportunities.*

### Step 19.1 – Product Readiness Checklist

**prompt:**
```
Create product readiness assessment in docs/product-readiness.md:

Core Functionality:
- [ ] Job scraping from all major sources working reliably
- [ ] AI job matching accuracy >85% user satisfaction
- [ ] Resume and cover letter generation quality acceptable
- [ ] Auto-apply success rate >70% for supported ATS
- [ ] Application tracking functional
- [ ] User dashboard responsive and intuitive

Technical Readiness:
- [ ] System handles 10,000+ concurrent users
- [ ] API response times <200ms (p95)
- [ ] Database query performance optimized
- [ ] Caching strategy effective (hit rate >80%)
- [ ] Error rate <0.1%
- [ ] Uptime >99.9%
- [ ] Security audit passed
- [ ] Load testing passed (1000+ req/s)

Business Readiness:
- [ ] User onboarding flow complete
- [ ] Payment integration (if applicable)
- [ ] Terms of Service and Privacy Policy
- [ ] Customer support system ready
- [ ] Analytics and tracking implemented
- [ ] Marketing website ready
- [ ] Legal compliance verified

Scalability Readiness:
- [ ] Auto-scaling tested and working
- [ ] Database can handle 1M+ jobs
- [ ] Can support 100K+ users
- [ ] Cost structure understood
- [ ] Infrastructure monitoring complete

Create comprehensive readiness assessment document.
```

**verify the generated content:**
Review checklist: Go through each item, verify completion status, identify gaps, prioritize missing items.

**desired output to verify:**
Readiness checklist complete, all critical items verified, gaps identified, prioritization clear, action items documented.

**CI/CD:**
```yaml
- name: Validate product readiness
  run: |
    # Check readiness document exists
    test -f docs/product-readiness.md
    # Run automated readiness checks
    python scripts/check_readiness.py
```

**git commit message:**
```
docs: create product readiness assessment checklist
```

---

### Step 19.2 – MVP vs Full Product Feature Matrix

**prompt:**
```
Create feature matrix in docs/feature-matrix.md:

MVP Features (Launch Ready):
- Core job scraping (3-5 major sources)
- Basic AI job matching
- Resume generation (1 template)
- Cover letter generation
- Manual application submission
- Basic dashboard
- User authentication
- Profile management

Phase 2 Features (Post-Launch):
- Auto-apply for major ATS (Greenhouse, Lever, Workday)
- Advanced AI matching with learning
- Multiple resume templates
- Cover letter customization
- Application tracking with email parsing
- Advanced filters and search
- Job alerts and notifications
- Analytics dashboard

Phase 3 Features (Growth):
- Multi-language support
- International job boards
- Company research integration
- Interview preparation tools
- Salary negotiation insights
- Referral tracking
- Social sharing
- Mobile app

Phase 4 Features (Scale):
- Enterprise features
- Team collaboration
- API for third-party integrations
- White-label solutions
- Advanced analytics
- Custom AI models
- Multi-tenant support

Create feature prioritization framework with user value vs effort matrix.
```

**verify the generated content:**
Review matrix: Verify MVP features are complete, prioritize Phase 2 features, assess effort vs value for each feature.

**desired output to verify:**
Feature matrix complete, MVP clearly defined, roadmap prioritized, effort estimates realistic, user value assessed.

**CI/CD:**
```yaml
- name: Validate feature matrix
  run: |
    test -f docs/feature-matrix.md
    # Verify MVP features are implemented
    python scripts/check_mvp_features.py
```

**git commit message:**
```
docs: create feature matrix with MVP and roadmap
```

---

## Phase 20 – Enhancement & Business Adaptation Framework
*Goal: Establish methodology for continuous improvement and business adaptation.*

### Step 20.1 – Create Enhancement Request Process

**prompt:**
```
Create enhancement request process in docs/enhancement-process.md:

Enhancement Request Workflow:
1. Request Collection:
   - User feedback forms
   - Support tickets
   - Feature requests in app
   - Community forums
   - Sales/customer success input
   - Internal team suggestions

2. Request Evaluation:
   - Business value assessment
   - Technical feasibility analysis
   - Effort estimation
   - User impact analysis
   - Strategic alignment check
   - ROI calculation

3. Prioritization Framework:
   - Impact vs Effort matrix
   - User demand scoring
   - Revenue impact
   - Competitive advantage
   - Technical debt consideration
   - Strategic goals alignment

4. Request Management:
   - Issue tracking system (Jira, GitHub Issues)
   - Request categorization
   - Status tracking (Backlog, In Review, Approved, In Progress, Done)
   - Stakeholder communication
   - Timeline estimation

5. Approval Process:
   - Product manager review
   - Engineering assessment
   - Design review (if UI/UX)
   - Business case approval
   - Resource allocation

Create enhancement request template and tracking system.
```

**verify the generated content:**
Test process: Submit sample enhancement request, verify workflow, check tracking system, test prioritization.

**desired output to verify:**
Enhancement process documented, workflow functional, tracking system set up, prioritization framework clear, stakeholders aligned.

**CI/CD:**
```yaml
- name: Validate enhancement process
  run: |
    test -f docs/enhancement-process.md
    # Check issue templates exist
    test -f .github/ISSUE_TEMPLATE/enhancement.md
```

**git commit message:**
```
feat(docs): create enhancement request process and workflow
```

---

### Step 20.2 – Implement Feature Flag System

**prompt:**
```
Create feature flag system in backend/src/infrastructure/feature_flags/:

- FeatureFlagService:
  - is_enabled(flag_name: str, user_id: Optional[str] = None) -> bool
  - enable_flag(flag_name: str, rollout_percentage: int = 100)
  - disable_flag(flag_name: str)
  - get_flag_config(flag_name: str) -> FeatureFlagConfig

- Feature flag types:
  - Boolean flags (on/off)
  - Percentage rollout (gradual release)
  - User-based flags (specific users)
  - A/B test flags (variant selection)
  - Time-based flags (scheduled releases)

- Flag configuration:
  - Database table: feature_flags (name, enabled, rollout_percentage, config JSONB)
  - Redis caching for performance
  - Admin API for flag management
  - Audit logging for flag changes

- Usage examples:
  - New feature: `if feature_flags.is_enabled('new_matching_algorithm', user_id):`
  - Gradual rollout: `if feature_flags.is_enabled('auto_apply_', user_id, rollout=10):`
  - A/B testing: `variant = feature_flags.get_variant('ui_redesign', user_id)`

- Management:
  - Admin dashboard for flag management
  - Real-time flag updates (no deployment needed)
  - Flag analytics (usage, impact)
  - Rollback capability

Create feature flag infrastructure and admin interface.
```

**verify the generated content:**
Test feature flags: Create flag, test enable/disable, verify percentage rollout, test A/B variants, check admin interface.

**desired output to verify:**
Feature flag system functional, flags can be toggled without deployment, rollout works, A/B testing supported, admin interface usable.

**CI/CD:**
```yaml
- name: Test feature flags
  run: |
    cd backend
    pytest tests/infrastructure/test_feature_flags.py -v
```

**git commit message:**
```
feat(infrastructure): implement feature flag system with gradual rollout
```

---

### Step 20.3 – Create Business Adaptation Framework

**prompt:**
```
Create business adaptation framework in docs/business-adaptation.md:

Adaptation Triggers:
- Market changes (new competitors, regulations)
- User feedback and behavior patterns
- Business model pivots
- Technology shifts
- Partnership requirements
- Regional expansion needs
- Compliance requirements

Adaptation Process:
1. Market Analysis:
   - Competitive analysis
   - User research
   - Market trends
   - Technology trends
   - Regulatory changes

2. Business Impact Assessment:
   - Revenue impact
   - User impact
   - Technical impact
   - Resource requirements
   - Timeline implications

3. Solution Design:
   - Architecture changes needed
   - Feature modifications
   - Integration requirements
   - Data migration needs
   - Backward compatibility

4. Implementation Strategy:
   - Phased approach
   - Risk mitigation
   - Rollback plans
   - User communication
   - Training needs

5. Success Metrics:
   - KPIs to track
   - Success criteria
   - Monitoring plan
   - Feedback collection

Common Adaptation Scenarios:
- Adding new job sources
- Supporting new regions/languages
- Changing pricing model
- Adding enterprise features
- Integrating with partners
- Compliance adaptations (GDPR, CCPA)
- Technology stack updates

Create adaptation playbook with templates for common scenarios.
```

**verify the generated content:**
Review framework: Test with sample adaptation scenario, verify process flow, check templates, validate success metrics.

**desired output to verify:**
Adaptation framework complete, process clear, templates useful, success metrics defined, team trained on process.

**CI/CD:**
```yaml
- name: Validate adaptation framework
  run: |
    test -f docs/business-adaptation.md
    # Check templates exist
    test -d docs/templates/adaptation
```

**git commit message:**
```
docs: create business adaptation framework and playbook
```

---

### Step 20.4 – Setup A/B Testing Infrastructure

**prompt:**
```
Create A/B testing system in backend/src/infrastructure/ab_testing/:

- ABTestService:
  - assign_variant(test_name: str, user_id: str) -> str (A or B)
  - track_event(test_name: str, variant: str, event: str, data: Dict)
  - get_test_results(test_name: str) -> TestResults
  - conclude_test(test_name: str, winning_variant: str)

- Test configuration:
  - Test name and description
  - Variants (A, B, C...)
  - Traffic split (50/50, 80/20, etc.)
  - Target audience (all users, segment, percentage)
  - Duration and sample size
  - Success metrics

- Statistical analysis:
  - Conversion rate calculation
  - Statistical significance testing (chi-square, t-test)
  - Confidence intervals
  - Minimum sample size calculation
  - Early stopping rules

- Test management:
  - Database table: ab_tests (name, status, config, results)
  - Admin API for test creation
  - Dashboard for test monitoring
  - Automated result analysis
  - Alert on significant results

- Integration:
  - Feature flags integration
  - Analytics integration
  - Event tracking
  - User segmentation

Create A/B testing infrastructure with statistical analysis.
```

**verify the generated content:**
Test A/B system: Create test, assign variants, track events, analyze results, verify statistical significance, check dashboard.

**desired output to verify:**
A/B testing system functional, variant assignment works, statistical analysis accurate, dashboard displays results, tests can be concluded.

**CI/CD:**
```yaml
- name: Test A/B testing
  run: |
    cd backend
    pytest tests/infrastructure/test_ab_testing.py -v
```

**git commit message:**
```
feat(infrastructure): implement A/B testing system with statistical analysis
```

---

## Phase 21 – SDLC Methodology for Ongoing Development
*Goal: Establish Software Development Life Cycle methodology for continuous product development.*

### Step 21.1 – Define SDLC Process

**prompt:**
```
Create SDLC methodology document in docs/sdlc-methodology.md:

SDLC Phases:
1. Planning & Requirements:
   - Feature request evaluation
   - Requirements gathering
   - User stories creation
   - Acceptance criteria definition
   - Technical design
   - Effort estimation
   - Sprint planning

2. Design:
   - Architecture design (if major change)
   - Database schema design
   - API design
   - UI/UX design
   - Security review
   - Performance considerations
   - Design review

3. Development:
   - Feature branch creation
   - Code implementation
   - Unit tests
   - Code review process
   - Continuous integration
   - Documentation updates

4. Testing:
   - Integration tests
   - E2E tests
   - Performance tests
   - Security tests
   - User acceptance testing
   - QA sign-off

5. Deployment:
   - Staging deployment
   - Smoke tests
   - Production deployment
   - Post-deployment verification
   - Monitoring

6. Maintenance:
   - Bug fixes
   - Performance optimization
   - Security updates
   - User support
   - Monitoring and alerts

Development Methodology:
- Agile/Scrum framework
- 2-week sprints
- Daily standups
- Sprint planning and retrospectives
- Backlog grooming
- Definition of Done checklist

Create comprehensive SDLC documentation with templates.
```

**verify the generated content:**
Review SDLC: Test with sample feature, verify all phases covered, check templates, validate process flow.

**desired output to verify:**
SDLC methodology documented, all phases clear, templates available, team trained, process followed consistently.

**CI/CD:**
```yaml
- name: Validate SDLC docs
  run: |
    test -f docs/sdlc-methodology.md
    test -d docs/templates/sdlc
```

**git commit message:**
```
docs: create SDLC methodology documentation
```

---

### Step 21.2 – Implement Sprint Planning Process

**prompt:**
```
Create sprint planning process in docs/sprint-planning.md:

Sprint Planning Workflow:
1. Pre-Planning:
   - Backlog grooming (prioritize items)
   - Capacity planning (team availability)
   - Dependencies identification
   - Technical debt assessment

2. Sprint Planning Meeting:
   - Review sprint goal
   - Select user stories from backlog
   - Break down stories into tasks
   - Estimate effort (story points/hours)
   - Assign tasks to team members
   - Identify risks and blockers

3. Sprint Backlog:
   - User stories with acceptance criteria
   - Technical tasks
   - Bug fixes
   - Technical debt items
   - Documentation tasks

4. Definition of Ready:
   - Clear acceptance criteria
   - Technical design complete
   - Dependencies identified
   - Effort estimated
   - Priority assigned

5. Definition of Done:
   - Code implemented and reviewed
   - Tests written and passing
   - Documentation updated
   - Deployed to staging
   - QA verified
   - Product owner accepted

Sprint Artifacts:
- Sprint backlog (Jira/GitHub Projects)
- Sprint goal statement
- Burndown chart
- Velocity tracking
- Risk register

Create sprint planning templates and tools.
```

**verify the generated content:**
Test sprint planning: Run sample sprint planning, verify workflow, check templates, validate artifacts created.

**desired output to verify:**
Sprint planning process clear, templates useful, tools configured, artifacts created correctly, team follows process.

**CI/CD:**
```yaml
- name: Validate sprint planning
  run: |
    test -f docs/sprint-planning.md
    # Check project board exists
    # Verify sprint template
```

**git commit message:**
```
docs: create sprint planning process and templates
```

---

### Step 21.3 – Setup Continuous Integration/Deployment Pipeline

**prompt:**
```
Enhance CI/CD pipeline for ongoing development in .github/workflows/:

Development Workflow:
1. Feature Branch:
   - Create feature branch from main
   - Push code
   - Automatic: Lint, test, build
   - Create PR

2. Pull Request:
   - Automatic: Full test suite
   - Code coverage check
   - Security scan
   - Build Docker images
   - Deploy to preview environment
   - E2E tests on preview

3. Code Review:
   - Required reviewers
   - Automated checks must pass
   - Manual review
   - Address feedback

4. Merge to Main:
   - Squash and merge
   - Automatic: Full pipeline
   - Deploy to staging
   - Integration tests
   - Smoke tests

5. Production Release:
   - Create release tag
   - Manual approval
   - Deploy to production
   - Post-deployment tests
   - Monitoring verification

Environments:
- Development: Feature branches
- Preview: PR deployments
- Staging: Main branch
- Production: Tagged releases

Branch Strategy:
- main: Production-ready code
- develop: Integration branch (optional)
- feature/*: Feature branches
- hotfix/*: Production fixes
- release/*: Release preparation

Create comprehensive CI/CD workflow with all environments.
```

**verify the generated content:**
Test CI/CD: Create feature branch, push code, verify pipeline runs, create PR, test deployment, verify production flow.

**desired output to verify:**
CI/CD pipeline functional, all environments configured, automated tests run, deployments work, monitoring integrated.

**CI/CD:**
This step creates the CI/CD pipeline itself. Verify in GitHub Actions.

**git commit message:**
```
ci: enhance CI/CD pipeline for ongoing development workflow
```

---

### Step 21.4 – Create Release Management Process

**prompt:**
```
Create release management process in docs/release-management.md:

Release Types:
1. Major Release (.0.0):
   - Breaking changes
   - Major new features
   - Architecture changes
   - Quarterly cadence

2. Minor Release (v1.1.0):
   - New features
   - Enhancements
   - Non-breaking changes
   - Monthly cadence

3. Patch Release (v1.0.1):
   - Bug fixes
   - Security patches
   - Hotfixes
   - As needed

Release Process:
1. Release Planning:
   - Feature freeze date
   - Release candidate creation
   - Testing period
   - Documentation updates
   - Marketing materials

2. Release Candidate:
   - Tag release candidate (v1.1.0-rc1)
   - Deploy to staging
   - Full test suite
   - Performance testing
   - Security review
   - Beta testing (if applicable)

3. Release Preparation:
   - Update version numbers
   - Changelog generation
   - Release notes
   - Database migration scripts
   - Rollback plan
   - Communication plan

4. Release Execution:
   - Create release tag
   - Deploy to production
   - Verify deployment
   - Monitor metrics
   - Post-release communication

5. Post-Release:
   - Monitor for issues
   - Collect feedback
   - Plan next release
   - Retrospective

Release Artifacts:
- Release notes (CHANGELOG.md)
- Migration guides
- API documentation updates
- Deployment runbook
- Rollback procedures

Create release management templates and automation.
```

**verify the generated content:**
Test release: Create release candidate, verify process, test deployment, check artifacts, validate rollback plan.

**desired output to verify:**
Release process documented, templates available, automation works, artifacts created, team trained on process.

**CI/CD:**
```yaml
- name: Validate release process
  run: |
    test -f docs/release-management.md
    test -f CHANGELOG.md
    # Verify release script exists
    test -f scripts/release.sh
```

**git commit message:**
```
docs: create release management process and templates
```

---

### Step 21.5 – Implement Product Analytics & Feedback Loop

**prompt:**
```
Create product analytics and feedback system:

Analytics Implementation:
- User behavior tracking:
  - Page views and navigation
  - Feature usage
  - User flows
  - Conversion funnels
  - Drop-off points

- Business metrics:
  - User acquisition
  - Activation rate
  - Retention rate
  - Revenue metrics
  - Feature adoption

- Technical metrics:
  - API performance
  - Error rates
  - System health
  - Resource usage

- Tools integration:
  - Google Analytics / Mixpanel
  - Custom event tracking
  - Database analytics
  - Log analysis

Feedback Collection:
- In-app feedback forms
- User surveys
- Support ticket analysis
- User interviews
- Beta testing feedback
- App store reviews

Feedback Analysis:
- Sentiment analysis
- Feature request extraction
- Bug identification
- User pain points
- Improvement opportunities

Feedback Loop:
1. Collect feedback
2. Analyze and categorize
3. Prioritize improvements
4. Implement changes
5. Measure impact
6. Iterate

Create analytics dashboard and feedback collection system.
```

**verify the generated content:**
Test analytics: Verify tracking works, check dashboard, test feedback collection, verify analysis, test feedback loop.

**desired output to verify:**
Analytics implemented, tracking functional, dashboard displays data, feedback collected, analysis automated, loop working.

**CI/CD:**
```yaml
- name: Validate analytics
  run: |
    # Check analytics implementation
    grep -r "track_event" backend/src/
    # Verify dashboard exists
    test -f frontend/src/components/analytics/Dashboard.tsx
```

**git commit message:**
```
feat: implement product analytics and feedback collection system
```

---

### Step 21.6 – Create Technical Debt Management Process

**prompt:**
```
Create technical debt management in docs/technical-debt.md:

Technical Debt Categories:
- Code quality: Refactoring needed, code smells
- Architecture: Design improvements, scalability
- Dependencies: Outdated libraries, security vulnerabilities
- Documentation: Missing or outdated docs
- Testing: Low coverage, missing tests
- Infrastructure: Optimization opportunities
- Performance: Slow queries, inefficient code

Debt Tracking:
- Issue tracking system (Jira, GitHub Issues)
- Debt registry with priority
- Impact assessment
- Effort estimation
- Business impact

Debt Management:
1. Identification:
   - Code reviews
   - Static analysis tools
   - Performance profiling
   - Security scans
   - Team retrospectives

2. Prioritization:
   - Impact on users
   - Risk assessment
   - Cost of delay
   - Business impact
   - Effort required

3. Planning:
   - Allocate sprint capacity (20% rule)
   - Debt reduction sprints
   - Continuous improvement
   - Refactoring as part of features

4. Execution:
   - Address high-priority debt
   - Prevent new debt
   - Code quality gates
   - Regular debt reviews

Debt Prevention:
- Code review requirements
- Automated quality checks
- Architecture reviews
- Documentation standards
- Testing requirements

Create technical debt tracking system and process.
```

**verify the generated content:**
Test debt management: Identify sample debt, prioritize, track, plan reduction, verify prevention measures.

**desired output to verify:**
Debt management process clear, tracking system functional, prioritization works, prevention measures in place, team follows process.

**CI/CD:**
```yaml
- name: Check technical debt
  run: |
    # Run code quality checks
    pylint backend/src/ --fail-under=8.0
    # Check test coverage
    pytest --cov --cov-fail-under=80
```

**git commit message:**
```
docs: create technical debt management process
```

---

## Phase 22 – Scaling & Growth Strategy
*Goal: Prepare for company growth and product scaling.*

### Step 22.1 – Create Scaling Roadmap

**prompt:**
```
Create scaling roadmap in docs/scaling-roadmap.md:

Scaling Dimensions:
1. User Scaling:
   - Current: 1K users
   - 3 months: 10K users
   - 6 months: 50K users
   - 12 months: 100K users
   - 24 months: 1M users

2. Data Scaling:
   - Jobs: 100K → 1M → 10M
   - Applications: 10K → 100K → 1M
   - User profiles: 1K → 10K → 100K

3. Geographic Scaling:
   - Single region → Multi-region
   - Single language → Multi-language
   - Single currency → Multi-currency

4. Feature Scaling:
   - MVP → Full feature set
   - Single use case → Multiple use cases
   - B2C → B2B → Enterprise

Scaling Milestones:
- Milestone 1 (10K users):
  - Optimize database queries
  - Implement CDN
  - Add caching layer
  - Cost: $X/month

- Milestone 2 (50K users):
  - Database sharding
  - Microservices architecture
  - Multi-region deployment
  - Cost: $Y/month

- Milestone 3 (100K users):
  - Advanced caching
  - Read replicas
  - Auto-scaling optimization
  - Cost: $Z/month

Scaling Checklist:
- [ ] Database can handle target load
- [ ] API can handle target requests
- [ ] Infrastructure auto-scales
- [ ] Monitoring and alerts configured
- [ ] Cost optimization done
- [ ] Performance targets met
- [ ] Disaster recovery ready

Create detailed scaling roadmap with cost estimates.
```

**verify the generated content:**
Review roadmap: Verify milestones realistic, check cost estimates, validate scaling strategies, test assumptions.

**desired output to verify:**
Scaling roadmap complete, milestones clear, cost estimates reasonable, strategies validated, checklist actionable.

**CI/CD:**
```yaml
- name: Validate scaling roadmap
  run: |
    test -f docs/scaling-roadmap.md
    # Check scaling tests exist
    test -f tests/performance/test_scaling.py
```

**git commit message:**
```
docs: create scaling roadmap with milestones and cost estimates
```

---

### Step 22.2 – Implement Multi-Tenancy (if needed)

**prompt:**
```
Create multi-tenancy support if needed for B2B/Enterprise:

Multi-Tenancy Models:
1. Database per tenant (isolated)
2. Shared database, separate schemas
3. Shared database, shared schema (with tenant_id)

Implementation:
- Tenant identification:
  - Subdomain-based (tenant1.CareerBlitz.com)
  - Path-based (/tenant1/jobs)
  - Header-based (X-Tenant-ID)

- Data isolation:
  - Tenant ID in all tables
  - Row-level security
  - Query filtering by tenant
  - Data access controls

- Tenant management:
  - Tenant creation/deletion
  - Tenant configuration
  - Feature flags per tenant
  - Billing per tenant
  - Admin dashboard

- Security:
  - Tenant data isolation
  - Cross-tenant access prevention
  - Audit logging per tenant
  - Compliance per tenant

Create multi-tenancy infrastructure if B2B model is planned.
```

**verify the generated content:**
Test multi-tenancy: Create tenant, verify isolation, test data access, verify security, check admin functions.

**desired output to verify:**
Multi-tenancy functional, data isolated, security enforced, admin tools work, scalable architecture.

**CI/CD:**
```yaml
- name: Test multi-tenancy
  run: |
    cd backend
    pytest tests/infrastructure/test_multitenancy.py -v
```

**git commit message:**
```
feat(infrastructure): implement multi-tenancy support for B2B model
```

---

### Step 22.3 – Create Business Model Adaptation Guide

**prompt:**
```
Create business model adaptation guide in docs/business-models.md:

Business Model Options:
1. Freemium:
   - Free: Basic features, limited usage
   - Premium: Full features, unlimited usage
   - Implementation: Feature flags, usage limits, payment integration

2. Subscription:
   - Monthly/Annual plans
   - Tiered pricing (Basic, Pro, Enterprise)
   - Implementation: Stripe/Recurly, subscription management

3. Usage-Based:
   - Pay per application
   - Pay per job match
   - Implementation: Usage tracking, billing system

4. Enterprise:
   - Custom pricing
   - White-label options
   - Dedicated support
   - Implementation: Multi-tenancy, custom features

Adaptation Process:
1. Market Research:
   - Competitor analysis
   - User willingness to pay
   - Market size
   - Pricing sensitivity

2. Model Design:
   - Feature tiers
   - Pricing structure
   - Value proposition
   - Go-to-market strategy

3. Technical Implementation:
   - Payment integration
   - Subscription management
   - Usage tracking
   - Billing system
   - Admin dashboard

4. Launch:
   - Beta testing
   - Gradual rollout
   - User communication
   - Support preparation

5. Optimization:
   - Pricing experiments
   - Feature adjustments
   - Conversion optimization
   - Retention strategies

Create business model adaptation framework.
```

**verify the generated content:**
Review guide: Test with sample business model, verify implementation steps, check technical requirements, validate process.

**desired output to verify:**
Business model guide complete, adaptation process clear, implementation steps detailed, technical requirements defined.

**CI/CD:**
```yaml
- name: Validate business model docs
  run: |
    test -f docs/business-models.md
    # Check payment integration exists
    test -d backend/src/infrastructure/payments
```

**git commit message:**
```
docs: create business model adaptation guide
```

---

## Conclusion

This Prompt-Generator Book provides a complete, step-by-step guide to building CareerBlitz  from scratch to production, and beyond. The system is designed using Clean Architecture and Domain-Driven Design principles to support millions of users with high availability, fault tolerance, and comprehensive monitoring.

**Product Readiness:**
✅ The book provides a **production-ready foundation** that can support a company launch with:
- Core functionality complete (scraping, matching, applications)
- Scalable architecture (handles 100K+ users)
- Security hardened
- Comprehensive testing
- Monitoring and observability
- Documentation complete

**Post-Launch Enhancement:**
✅ The book includes methodology for:
- Feature enhancement process
- Business adaptation framework
- A/B testing infrastructure
- Feature flag system
- Continuous improvement process

**SDLC Methodology:**
✅ Complete SDLC process for ongoing development:
- Agile/Scrum framework
- Sprint planning and execution
- CI/CD pipeline
- Release management
- Technical debt management
- Product analytics and feedback loops

**Key Features:**
- ✅ Clean Architecture with clear layer separation
- ✅ Domain-Driven Design with bounded contexts
- ✅ Scalable infrastructure with auto-scaling
- ✅ Comprehensive testing strategy
- ✅ Security hardening throughout
- ✅ Production-ready deployment
- ✅ Complete documentation
- ✅ Enhancement and adaptation framework
- ✅ SDLC methodology for continuous development
- ✅ Scaling and growth strategy

**Next Steps:**
1. **Launch MVP**: Complete Phases 1-18 to launch your product
2. **Gather Feedback**: Use Phase 21 analytics to collect user feedback
3. **Iterate**: Use Phase 20 enhancement process to prioritize improvements
4. **Scale**: Follow Phase 22 roadmap as you grow
5. **Adapt**: Use business adaptation framework as market needs change

**Starting a Company:**
This book provides enough foundation to:
- ✅ Launch an MVP product
- ✅ Support initial users (1K-10K)
- ✅ Scale to growth (100K+ users)
- ✅ Adapt to business needs
- ✅ Continuously improve

**Ongoing Development:**
After launch, use:
- **Phase 19**: Assess product readiness and plan enhancements
- **Phase 20**: Implement new features and adapt to business needs
- **Phase 21**: Follow SDLC methodology for continuous development
- **Phase 22**: Scale as you grow

**Support:**
- Review architecture diagrams in each phase
- Refer to domain models for business logic
- Check infrastructure setup for scaling
- Use monitoring and observability for debugging
- Follow security best practices throughout
- Use enhancement process for new features
- Follow SDLC methodology for development

Good luck building and scaling CareerBlitz ! 🚀

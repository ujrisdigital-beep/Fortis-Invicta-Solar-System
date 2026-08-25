# Fortis Invicta Solar System

![Version](https://img.shields.io/badge/version-2.5.0--production-emerald)
![Node.js](https://img.shields.io/badge/node.js-22%20LTS-green)
![React](https://img.shields.io/badge/React-19-blue)
![Database](https://img.shields.io/badge/database-PostgreSQL%2FSupabase-teal)
![License](https://img.shields.io/badge/license-Proprietary-red)

## Overview

**Fortis Invicta Solar System** is an enterprise-grade solar project management and fintech platform built for The Gambia and West Africa. It enables seamless client onboarding, financial operations through EcobankPay bank transfers, institutional union verification (GTUCCU, NAGNMC), site assessment management, and comprehensive project tracking.

**Target Audience:** Solar installation companies, financial institutions, educational unions, healthcare facilities, and government agencies across West Africa.

---

## 🎯 Key Features

### 1. **Client Onboarding & Management**
- Comprehensive client registration with institutional affiliation tracking
- RAG (Red-Amber-Green) status tracking for project milestones
- Multi-tier client segmentation (lead, qualified, installation, completed)

### 2. **Financial Operations**
- **EcobankPay Integration**: Direct bank transfer processing with merchant verification
- **80/20 Payment Split**: Enforced deposit structure (80% upfront, 20% upon completion)
- **Institutional Payroll Deduction**: Automated GTUCCU/NAGNMC union member salary deductions
- **Payment Ledger**: Teller slip uploads, OCR verification, and payment status tracking

### 3. **Institutional Verification**
- GTUCCU (Gambia Teachers' Union Credit and Cooperative Union) member verification
- NAGNMC (National Association of Gambian Nurses and Midwives) institutional checks
- Proof-of-membership token generation with HMAC-SHA256 cryptography
- Pre-approved credit limit validation

### 4. **Site Assessment**
- Digital rooftop survey with azimuth/tilt angle documentation
- Daily energy load calculation (kWh)
- Solar panel and battery sizing recommendations
- Shading analysis and NAWEC grid stability assessment

### 5. **Project Tracking**
- Installation timeline management with engineer dispatch
- 4-tier solar package catalog (Tier 1–4, 1.5kVA to 15kVA+)
- Warranty management (5-year standard coverage)
- Real-time inverter and microgrid telemetry via ThingsBoard

### 6. **AI-Powered Intelligence**
- Google Gemini 2.5 AI Assistant for solar engineering consultations
- Automated solar system quote generation
- Payment receipt OCR with AI-based verification
- Exponential backoff retry logic with fallback responses

### 7. **Enterprise Integration**
- **Directus Headless CMS**: Package catalog and content management
- **ERPNext**: HR roster, staff availability, and engineer dispatch
- **Moodle**: Academy training platform for technicians
- **Postal**: Transactional email and invoice delivery
- **OpenSearch**: Audit logging and compliance tracking

---

## 🏗️ Architecture

```
┌─────────────────────────────────────┐
│    React 19 SPA (Vite + Tailwind)   │
│  Client-Side Sentry Error Tracking  │
└──────────────┬──────────────────────┘
               │ HTTPS/WSS
               ▼
┌─────────────────────────────────────┐
│    Cloud Run / Docker Container     │
│  (Node.js 22 LTS Alpine Linux)      │
└──────────────┬──────────────────────┘
               │
    ┌──────────┼──────────┐
    ▼          ▼          ▼
┌────────┐ ┌────────┐ ┌─────────────┐
│Express │ │Supabase│ │Google Gemini│
│Server  │ │  PG    │ │   2.5 AI    │
│ (3000) │ │        │ │             │
└────────┘ └────────┘ └─────────────┘
```

### Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Frontend** | React 19, Vite, Tailwind CSS | Web client interface |
| **Backend** | Express.js, TypeScript | REST API server |
| **Database** | PostgreSQL 16 / Supabase | Relational data store with RLS |
| **Authentication** | JWT (HS256), bcryptjs | Secure session management |
| **AI/ML** | Google Gemini 2.5 | Solar engineering assistant |
| **Observability** | Sentry, Structured Logging | Error tracking & diagnostics |
| **Payments** | EcobankPay (Ecobank Gambia) | Bank transfer processing |
| **Email** | Postal Server | Transactional emails & invoices |
| **Search** | OpenSearch 2.11 | Audit log indexing |
| **IoT Telemetry** | ThingsBoard | Inverter & microgrid monitoring |
| **Container** | Docker, Cloud Run | Production deployment |

---

## 🚀 Quick Start

### Prerequisites
- **Node.js** 22 LTS or later
- **Docker & Docker Compose** (for local development with all services)
- **PostgreSQL** 15+ or **Supabase** account
- **Google Cloud Account** (for Gemini API & Cloud Run)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/ujrisdigital-beep/Fortis-Invicta-Solar-System.git
   cd Fortis-Invicta-Solar-System
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env
   ```
   
   **Required variables:**
   ```env
   NODE_ENV=development
   PORT=3000
   
   # Database
   DATABASE_URL=postgresql://user:password@localhost:5432/fortis_solar_db
   SUPABASE_URL=https://your-project.supabase.co
   SUPABASE_SERVICE_ROLE_KEY=your-service-role-key
   
   # Authentication
   JWT_SECRET=your-256-bit-secret-key-here
   JWT_REFRESH_SECRET=your-refresh-secret-key
   
   # Payment Gateway
   ECOBANK_MERCHANT_CODE=505825057
   ECOBANK_WEBHOOK_SECRET=your-webhook-secret
   
   # AI & ML
   GEMINI_API_KEY=your-google-gemini-api-key
   
   # Enterprise Services
   DIRECTUS_URL=http://localhost:8055
   DIRECTUS_API_KEY=fortis-cms-token
   ERPNEXT_URL=http://localhost:8000
   ERPNEXT_API_KEY=your-erpnext-key
   MOODLE_URL=http://localhost:8080
   MOODLE_API_KEY=your-moodle-key
   THINGSBOARD_URL=http://localhost:9090
   THINGSBOARD_API_TOKEN=your-tb-token
   POSTAL_API_URL=http://localhost:5000/api/v1
   POSTAL_API_KEY=your-postal-key
   POSTAL_SENDER=noreply@fortisinvicta.co.uk
   OPENSEARCH_URL=http://localhost:9200
   
   # Observability
   SENTRY_DSN=https://your-sentry-dsn
   ```

4. **Run with Docker Compose (all services)**
   ```bash
   docker-compose up -d
   ```
   
   This spins up:
   - **App** (Node.js) — Port 3000
   - **PostgreSQL** — Port 5432
   - **Directus CMS** — Port 8055
   - **ERPNext** — Port 8000
   - **Moodle** — Port 8080
   - **ThingsBoard** — Port 9090
   - **Postal** — Port 5000
   - **OpenSearch** — Port 9200

5. **Development server**
   ```bash
   npm run dev
   ```
   
   Vite dev server will start at `http://localhost:5173`

6. **Build for production**
   ```bash
   npm run build
   ```

7. **Run production server**
   ```bash
   npm run start
   ```

---

## 📖 API Documentation

### Authentication Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/auth/signup` | Register new user |
| `POST` | `/api/auth/login` | Authenticate user |
| `POST` | `/api/auth/refresh` | Renew access token |
| `POST` | `/api/auth/logout` | Invalidate session |
| `GET` | `/api/auth/me` | Get current user profile |

### Client Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/v2/clients` | List all clients |
| `POST` | `/api/clients/onboard` | Onboard new client |
| `GET` | `/api/v2/clients/{id}` | Get client details |

### Project Management

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/v2/projects` | List projects |
| `POST` | `/api/v2/projects` | Create project |
| `PUT` | `/api/v2/projects/{id}` | Update project |

### Payments & Financial

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/payments` | List all payments |
| `POST` | `/api/checkout/calculate` | Calculate order totals |
| `POST` | `/api/payments/ecobank-webhook` | EcobankPay webhook receiver |

### Site Assessments

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/v2/assessments` | List assessments |
| `POST` | `/api/assessments` | Create new assessment |

### Institutional Verification

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/verify-member` | Verify union member |

### AI Services

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/ai/assistant` | Chat with solar AI consultant |
| `POST` | `/api/ai/quote` | Generate solar system quote |
| `POST` | `/api/ai/ocr-payment` | Analyze payment receipt image |

### System Health

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/health` | Health check probe |
| `GET` | `/api/system/readiness` | Detailed diagnostics report |

---

## 🔐 Security & RBAC

### Role-Based Access Control (RBAC)

| Role | Permissions |
|------|-------------|
| **admin** | Full system control, financial oversight, database admin |
| **finance_officer** | Verify bank deposits, manage payments, ledger audits |
| **project_manager** | Schedule installations, track timelines, dispatch engineers |
| **engineer** | Perform site assessments, calculate loads, log commissions |
| **institutional_admin** | Verify union members, approve pre-credit |
| **client** | View personal projects, payment history, upload teller slips |

### Security Features

✅ **HTTP Security Headers**: X-Content-Type-Options, X-Frame-Options, Strict CSP  
✅ **CORS Protection**: Explicit allowlist by domain  
✅ **Rate Limiting**: Auth (10/15min), Verification (30/10min), API (300/15min)  
✅ **JWT Tokens**: 15-min access tokens, 7-day refresh tokens  
✅ **Password Hashing**: bcryptjs with 12 salt rounds  
✅ **Row-Level Security**: Supabase RLS policies enforce data isolation  
✅ **Audit Logging**: Immutable ledger via OpenSearch  
✅ **HMAC Signatures**: Webhook & institutional proof token validation  

---

## 🧪 Testing

Run the complete test suite:

```bash
npm test
```

Individual test files:
```bash
npm run test:qa                    # QA ecosystem verification
tsx tests/solarEngine.test.ts      # Solar sizing engine
tsx tests/paymentLedger.test.ts    # Payment processing
tsx tests/rbacAuth.test.ts         # Role-based access control
```

---

## 📊 Deployment

### Deploy to Google Cloud Run

1. **Build and push Docker image**
   ```bash
   gcloud builds submit --tag gcr.io/[PROJECT_ID]/fortis-invicta-solar:latest
   ```

2. **Deploy to Cloud Run**
   ```bash
   gcloud run deploy fortis-invicta-solar \
     --image gcr.io/[PROJECT_ID]/fortis-invicta-solar:latest \
     --platform managed \
     --region europe-west2 \
     --allow-unauthenticated \
     --port 3000 \
     --set-env-vars NODE_ENV=production,PORT=3000 \
     --set-secrets JWT_SECRET=fortis-jwt-secret:latest,SUPABASE_URL=supabase-url:latest
   ```

3. **Verify deployment**
   ```bash
   curl https://fortis-invicta-solar-xxxxx.run.app/api/health
   ```

### Database Migration

1. Execute `/src/db/schema.sql` in Supabase SQL Editor
2. Enable Row-Level Security (RLS) on core tables
3. Configure Supabase backup policies (daily snapshots recommended)

---

## 📡 Monitoring & Observability

### Sentry Error Tracking

Sentry is integrated on both frontend and backend:

```typescript
// Backend: src/server/monitoring.ts
initBackendMonitoring();

// Frontend: src/services/sentry.ts
<SentryErrorBoundary>
```

**Recommended Alert Rules:**
- **P0**: Auth failure spike (>25 failures in 5 min)
- **P0**: Database connection drop
- **P1**: Gemini API consecutive rate-limits (3+ errors)
- **P1**: Client exception count (>5 in 10 min)

### System Readiness Probe

Check deployment readiness:
```bash
curl https://your-app/api/system/readiness
```

Returns:
- Environment audit (all variables validated)
- Database connectivity status
- Service worker specifications
- System metrics (uptime, memory, connections)

---

## 📁 Project Structure

```
Fortis-Invicta-Solar-System/
├── src/
│   ├── components/          # React components
│   ├── pages/               # Page layouts
│   ├── server/              # Express middleware & utilities
│   │   ├── auth.ts          # JWT & RBAC logic
│   │   ├── security.ts      # CORS, rate limiting, headers
│   │   ├── monitoring.ts    # Sentry initialization
│   │   ├── geminiService.ts # AI integration
│   │   ├── routes/          # API route handlers
│   │   └── envConfig.ts     # Configuration validation
│   ├── db/                  # Database schema & client
│   ├── services/            # Business logic
│   └── main.tsx             # React entry point
├── tests/                   # Test suites
├── public/                  # Static assets
├── docker-compose.yml       # Multi-service orchestration
├── Dockerfile               # Production container build
├── package.json             # Dependencies & scripts
├── tsconfig.json            # TypeScript configuration
├── vite.config.ts           # Vite bundler config
└── README.md                # This file
```

---

## 🛠️ Development Workflow

1. **Feature branch**
   ```bash
   git checkout -b feature/your-feature
   ```

2. **Development**
   ```bash
   npm run dev
   ```

3. **Linting**
   ```bash
   npm run lint
   ```

4. **Testing**
   ```bash
   npm test
   ```

5. **Build & verify**
   ```bash
   npm run build
   npm run production:check
   ```

6. **Commit & push**
   ```bash
   git add .
   git commit -m "feat: add your feature"
   git push origin feature/your-feature
   ```

7. **Create Pull Request** on GitHub

---

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

- Fork the repository
- Create a feature branch (`feature/your-feature`)
- Make your changes with clear commit messages
- Add tests for new functionality
- Ensure all tests pass
- Submit a pull request

---

## 📝 License

**Proprietary Software** — All rights reserved by Fortis Invicta Ltd.  
Unauthorized copying, modification, or distribution is prohibited.

---

## 📞 Support & Contact

For issues, feature requests, or support:

- **Email**: support@fortisinvicta.co.uk
- **GitHub Issues**: [Create an issue](https://github.com/ujrisdigital-beep/Fortis-Invicta-Solar-System/issues)
- **Documentation**: Check `/docs` folder (coming soon)

---

## 🌍 Supported Regions

- **Gambia** (Primary market)
- **Senegal** (Planned Q3 2026)
- **Sierra Leone** (Planned Q4 2026)
- **West Africa** (Regional expansion roadmap)

---

## 📅 Changelog

### v2.5.0 (Current — Production Upgrade)
- ✅ Cloud Run deployment support
- ✅ Supabase RLS policies
- ✅ Sentry observability integration
- ✅ Google Gemini 2.5 AI assistant
- ✅ Multi-service Docker Compose
- ✅ GTUCCU/NAGNMC institutional verification

**[See full changelog](./CHANGELOG.md)** (Coming soon)

---

**Built with ❤️ by Fortis Invicta Ltd — Powering Solar Energy in West Africa**

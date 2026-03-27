# crispy-octo-funicular


# 🐿️ Squirrel News: Personalized UPSC & Premium Hub

Squirrel News is a high-performance, AI-driven news aggregator and personalized learning companion. Designed for UPSC aspirants and news enthusiasts, it provides curated briefings, AI-powered enrichment, and an interactive squirrel companion (Squirrel) to help users master current affairs.

---

## 🏗️ Architecture

```mermaid
graph TD
    User((User))
    
    subgraph "Frontend (React + Vite)"
        UI[UI Components]
        Context[Auth & Theme Context]
        Feed[Personalized Feed]
    end
    
    subgraph "Backend (FastAPI)"
        API[API Gateway]
        Auth[Auth Processor]
        News[News & UPSC Processor]
        AI[AI Assistant / Groq]
        Stripe[Stripe Payment Verifier]
    end
    
    subgraph "Data & Services"
        DB[(MongoDB)]
        NAPI[NewsAPI / RSS]
        StripeS[Stripe API]
    end
    
    User <--> UI
    UI <--> Context
    UI <--> API
    API <--> Auth
    API <--> News
    API <--> AI
    API <--> Stripe
    Auth <--> DB
    News <--> NAPI
    News <--> AI
    Stripe <--> StripeS
    Stripe <--> DB
```

---

## 🔄 Workflows

### 1. UPSC Enrichment Flow
```mermaid
sequenceDiagram
    participant User
    participant Backend
    participant Groq
    participant DB

    User->>Backend: Request Feed (Role: Student)
    Backend->>DB: Fetch Raw News
    loop For each article
        Backend->>Groq: Generate UPSC Insights
        Groq-->>Backend: GS Paper, Facts, Mains Prompt
    end
    Backend-->>User: Personalized UPSC Feed
```

### 2. Premium Subscription Verification
```mermaid
sequenceDiagram
    participant User
    participant Frontend
    participant Backend
    participant Stripe
    participant DB

    User->>Frontend: Clicks "Go Premium"
    Frontend->>Stripe: Redirect to Checkout
    User->>Stripe: Completes Payment
    Stripe-->>Frontend: Redirect back with session_id
    Frontend->>Backend: GET /verify-session?id=...
    Backend->>Stripe: Finalize & Verify Session
    Stripe-->>Backend: Session Confirmed
    Backend->>DB: Update User.is_premium = true
    Backend-->>Frontend: Success Response
    Frontend->>Frontend: Refresh User State
```

---

## ✨ Features

- **Personalized Feed**: Content tailored to your role (Student, Professional, etc.).
- **UPSC Deep Prep**: Mapping news to GS Papers, Prelims facts, and Mains answers.
- **Interactive Squirrel**: Your AI companion for explaining news and taking quizzes.
- **Premium Perks**: Unlock advanced AI tools and UPSC-specific analytics via Stripe.
- **Dark Mode**: Sleek, eye-friendly design for late-night study sessions.

---

## 🚀 Getting Started

### Prerequisites
- Python 3.9+
- Node.js 18+
- MongoDB instance (local or Atlas)

### Local Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/levi178u/ET-Hackathon.git
   cd ET-Hackathon
   ```

2. **Environment Variables**
   Create `.env` in `backend/` and `frontend/`:
   ```env
   # Backend .env
   MONGODB_URL=your_mongo_url
   GROQ_API_KEY=your_groq_key
   STRIPE_SECRET_KEY=your_stripe_key
   NEWSAPI_KEY=your_newsapi_key
   ```

3. **Running the App**
   Use our automated deployment script:
   ```powershell
   ./scripts/deploy.ps1
   ```

---

## 🛠️ Tech Stack

- **Frontend**: React, Tailwind CSS 4, Lucide Icons, Axios.
- **Backend**: FastAPI, Motor (Async MongoDB), Pydantic.
- **AI**: Groq (Llama-3 models) for speed and intelligence.
- **Payment**: Stripe Checkout for seamless billing.

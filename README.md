# 💰 Welth -- AI-Powered Personal Finance Manager

A **Next.js (App Router)** full-stack finance management platform that
helps you track income and expenses, manage multiple accounts, set
budgets, automate recurring transactions, and receive **AI-powered
insights**.

Built with **Clerk**, **Prisma**, **Inngest**, **Resend**, **Google
Gemini**, and **Arcjet**.

------------------------------------------------------------------------

## Demo
[![Watch Demo](https://img.shields.io/badge/Watch%20Demo-Video-blue?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/1rq-5huxmxu3Q5DWLpi54dKvh2zyPhC7l/view?usp=sharing)

------------------------------------------------------------------------
## ✨ Features

-   🔐 **Authentication** -- Clerk-powered sign-in / sign-up with
    protected routes\
-   💳 **Multi-Account Support** -- Create and manage multiple accounts,
    set default account\
-   💸 **Transactions** -- CRUD operations with atomic balance updates\
-   📊 **Analytics Dashboard** -- Income/expense charts, breakdowns, and
    budget progress\
-   🧾 **AI Receipt Scanner** -- Extracts amount, date, category from
    receipts via Gemini\
-   📅 **Recurring Transactions** -- Auto-processed with throttling via
    Inngest\
-   📧 **Smart Emails** -- Budget alerts & monthly reports with
    AI-generated insights\
-   📉 **Budget Tracking** -- Alerts when expenses exceed 80% of budget\
-   🛡 **Bot Protection & Rate Limiting** -- Arcjet middleware + Clerk
    auth guard\
-   🧪 **Demo Mode** -- Seed database with realistic sample data

------------------------------------------------------------------------

## 🏗 Architecture

  -----------------------------------------------------------------------
  Layer                           Purpose
  ------------------------------- ---------------------------------------
  **Next.js (App Router)**        Pages, server actions, API routes

  **Clerk**                       Authentication & session management

  **Prisma**                      PostgreSQL ORM, migrations, seeding

  **Inngest**                     Background jobs (budget checks,
                                  recurring txns, monthly reports)

  **Resend + React Email**        Transactional emails & reports

  **Google Gemini**               Receipt OCR & monthly insights

  **Arcjet**                      Rate limiting, shield, bot detection

  **Tailwind + ShadCN UI**        Modern responsive UI components

  **Recharts**                    Data visualization (charts, graphs)
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## 🔄 Data Flow

1.  **User signs in** (Clerk) → session validated by middleware.
2.  **Dashboard loads** → server actions fetch accounts, budgets, and
    transactions.
3.  **Add transaction** → balance updated in Prisma; optional receipt
    scanner auto-fills form with Gemini OCR.
4.  **Recurring transactions** → Inngest scheduler creates events;
    processor runs jobs per interval.
5.  **Budget alerts** → Every 6h, Inngest checks expenses vs. budget →
    sends email if threshold exceeded.
6.  **Monthly reports** → First of each month, Inngest aggregates data,
    generates insights with Gemini, and emails report.

------------------------------------------------------------------------

## 📦 Tech Stack

-   **Framework**: Next.js 15 (App Router, Server Actions)
-   **Language**: JavaScript / JSX
-   **Auth**: Clerk
-   **Database**: PostgreSQL + Prisma 6
-   **Background Jobs**: Inngest
-   **Email**: Resend + React Email
-   **AI**: Google Gemini (OCR + insights)
-   **Security**: Arcjet (shield, detectBot, rate-limiting)
-   **UI**: Tailwind CSS 4, ShadCN components, Recharts
-   **State**: React hooks + custom server actions

------------------------------------------------------------------------

## 🚀 Getting Started

### 1. Clone the repo

```bash 
git clone https://github.com/Vadrevuharipriya/welth-AI-Finance-Platform.git
cd welth 
```

### 2. Install dependencies

```bash 
npm install 
```

### 3. Setup environment variables

Create a \`.env.local\` file:

```env 
DATABASE_URL=postgresql://user:password@localhost:5432/welth
CLERK_SECRET_KEY=your_clerk_secret CLERK_PUBLISHABLE_KEY=your_clerk_key
RESEND_API_KEY=your_resend_key GEMINI_API_KEY=your_gemini_key
ARCJET_KEY=your_arcjet_key 
```

### 4. Setup database

```bash 
npx prisma generate 
npx prisma migrate dev 
```

### 5. Run dev servers

``` bash 
npm run dev # Start Next.js 
npx inngest-cli@latest dev # Start Inngest dev server 
``` 

### 6. (Optional) Seed demo data

```bash
curl -X POST http://localhost:3000/api/seed 
```

------------------------------------------------------------------------

## 📧 Email Preview

You can preview email templates locally: 
```bash
 npm run email 
```

------------------------------------------------------------------------

## 📂 Repo Structure

<!-- \`\`\` welth/ ├─ app/ \# Next.js routes (App Router) │ ├─ (auth)/ \#
Clerk auth pages │ ├─ (main)/ \# Dashboard & core pages │ └─ api/ \# API
routes (Inngest, seeding) ├─ actions/ \# Server actions (CRUD, logic) ├─
lib/ \# Prisma, Inngest, Arcjet setup ├─ prisma/ \# Database schema ├─
emails/ \# React Email templates ├─ components/ \# UI components
(ShadCN, charts, forms) ├─ public/ \# Static assets (logos, icons) └─
data/ \# Predefined categories, landing content \`\`\` -->
```
welth/
 ├─ app/                # Next.js routes (App Router)
 │   ├─ (auth)/         # Clerk auth pages
 │   ├─ (main)/         # Dashboard & core pages
 │   └─ api/            # API routes (Inngest, seeding)
 ├─ actions/            # Server actions (CRUD, logic)
 ├─ lib/                # Prisma, Inngest, Arcjet setup
 ├─ prisma/             # Database schema
 ├─ emails/             # React Email templates
 ├─ components/         # UI components (ShadCN, charts, forms)
 ├─ public/             # Static assets (logos, icons)
 └─ data/               # Predefined categories, landing content

```
------------------------------------------------------------------------

## 🛡 Security

-   **Clerk** handles secure authentication and session management.\
-   **Arcjet** protects against abuse with:
    -   \`shield\` -- baseline abuse protection
    -   \`detectBot\` -- blocks non-human traffic (except search
        engines)\
-   **Prisma Transactions** ensure consistent account balances.

------------------------------------------------------------------------

## 📈 Roadmap

-   [ ] Mobile app version (Expo + React Native)\
-   [ ] More AI-driven financial coaching\
-   [ ] Export reports (PDF/CSV)\
-   [ ] Multi-currency support

------------------------------------------------------------------------

## 📝 License

MIT -- feel free to use and modify.

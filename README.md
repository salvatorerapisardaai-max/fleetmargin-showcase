# 🚗 FleetMargin

> Integrated management platform for car-rental businesses — vehicles, operators, maintenance and **per-vehicle profit & loss**, in one dashboard.

![Next.js](https://img.shields.io/badge/Next.js-16-000000?logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/Neon-PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-deployed-000000?logo=vercel&logoColor=white)

**🔗 Live demo:** [fleetmargin.vercel.app](https://fleetmargin.vercel.app)

> Built for a real car-rental business; the live demo runs on sample data. Published as a portfolio reference — production data and credentials are handled off-repo via environment variables.

## Why I built it

The client managed a rental fleet but had **no per-plate visibility** into profitability — revenue, maintenance and operator costs lived in scattered spreadsheets. They knew the fleet made money overall, but not *which cars* were eroding the margin. FleetMargin turns that into a single source of truth: every vehicle's revenue, cost and profit, in real time.

## What it does

- 📊 **Real-time dashboard** — active vehicles, operators and rentals, total revenue and **profit margin**, plus a per-car margin table (revenue, cost, profit, %).
- 🚗 **Fleet management** — full CRUD on vehicles (plate, make, model, year, owner), availability windows and configurable daily cost.
- 👥 **Operators** — technician registry with role and hourly cost, and per-operator activity history.
- 🔧 **Maintenance activities** — custom activity types with fixed cost and standard duration; each execution auto-computes total cost (labour + materials + fixed cost) against a vehicle and operator.
- 🎫 **Rentals** — bookings linking vehicles to clients, with active/historical tracking.
- 📈 **Economic reporting** — per-vehicle P&L driven by a dedicated database view.

## Architecture

| Layer | Tech | Notes |
|------|------|------|
| Front-end | Next.js 16 + React 19 | App Router, Server Components |
| Styling | Tailwind CSS 4 | utility-first |
| Back-end | Next.js API Routes + Server Actions | full-stack TypeScript |
| Database | PostgreSQL (Neon) | serverless, parametrized SQL |
| Quality | ESLint 9, TypeScript 5 | type-safe end-to-end |
| Hosting / CI | Vercel | GitHub → Vercel continuous deployment |

### Engineering highlights

- **Server Actions over a thin data layer**: all mutations run server-side (`'use server'`) with type-safe **parametrized** queries via `@neondatabase/serverless`, automatic cache revalidation (`revalidatePath`) and post-action redirects — no separate API layer to maintain.
- **Economics as a database view** (`vista_economia_auto`): per-vehicle P&L is computed in SQL rather than in the UI, keeping the dashboard fast and the logic single-sourced.
- **Locale-aware money formatting** (IT-IT): `euro(1234.56) → "1.234,56 €"`.

## Roadmap

- 🔐 Authentication & authorization
- 📄 Report export (PDF / Excel)
- 📊 Charts and visualizations
- ✅ Test suite

## What I learned

Owning a real product end-to-end: setting up the GitHub → Vercel deployment pipeline from scratch, modelling per-plate cost/revenue attribution in PostgreSQL, and leaning on Server Actions to ship a full-stack TypeScript app without a separate API. The unglamorous part — environment config, redeploy flow, data modelling — is what made it actually ship.

---

**FleetMargin v0.1.0** — MVP · built and maintained by **Salvatore Rapisarda** ([@salvatorerapisardaai-max](https://github.com/salvatorerapisardaai-max))

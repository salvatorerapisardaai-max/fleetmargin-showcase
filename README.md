# 🚗 FleetMargin

> 🇬🇧 [English](#-english) · 🇮🇹 [Italiano](#-italiano)

![Next.js](https://img.shields.io/badge/Next.js-16-000000?logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-19-61DAFB?logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/Neon-PostgreSQL-4169E1?logo=postgresql&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-deployed-000000?logo=vercel&logoColor=white)

**🔗 Live demo:** [fleetmargin.vercel.app](https://fleetmargin.vercel.app)

---

## 🇬🇧 English

> Integrated management platform for car-rental businesses — vehicles, operators, maintenance and **per-vehicle profit & loss**, in one dashboard.

> Built for a real car-rental business; the live demo runs on sample data. Published as a portfolio reference — production data and credentials are handled off-repo via environment variables.

### Why I built it

The client managed a rental fleet but had **no per-plate visibility** into profitability — revenue, maintenance and operator costs lived in scattered spreadsheets. They knew the fleet made money overall, but not *which cars* were eroding the margin. FleetMargin turns that into a single source of truth: every vehicle's revenue, cost and profit, in real time.

### What it does

- 📊 **Real-time dashboard** — active vehicles, operators and rentals, total revenue and **profit margin**, plus a per-car margin table (revenue, cost, profit, %).
- 🚗 **Fleet management** — full CRUD on vehicles (plate, make, model, year, owner), availability windows and configurable daily cost.
- 👥 **Operators** — technician registry with role and hourly cost, and per-operator activity history.
- 🔧 **Maintenance activities** — custom activity types with fixed cost and standard duration; each execution auto-computes total cost (labour + materials + fixed cost) against a vehicle and operator.
- 🎫 **Rentals** — bookings linking vehicles to clients, with active/historical tracking.
- 📈 **Economic reporting** — per-vehicle P&L driven by a dedicated database view.

### Architecture

| Layer | Tech | Notes |
|------|------|------|
| Front-end | Next.js 16 + React 19 | App Router, Server Components |
| Styling | Tailwind CSS 4 | utility-first |
| Back-end | Next.js API Routes + Server Actions | full-stack TypeScript |
| Database | PostgreSQL (Neon) | serverless, parametrized SQL |
| Quality | ESLint 9, TypeScript 5 | type-safe end-to-end |
| Hosting / CI | Vercel | GitHub → Vercel continuous deployment |

**Engineering highlights**
- **Server Actions over a thin data layer**: all mutations run server-side (`'use server'`) with type-safe **parametrized** queries via `@neondatabase/serverless`, automatic cache revalidation (`revalidatePath`) and post-action redirects — no separate API layer to maintain.
- **Economics as a database view** (`vista_economia_auto`): per-vehicle P&L is computed in SQL rather than in the UI, keeping the dashboard fast and the logic single-sourced.
- **Locale-aware money formatting** (IT-IT): `euro(1234.56) → "1.234,56 €"`.

### Roadmap
- 🔐 Authentication & authorization
- 📄 Report export (PDF / Excel)
- 📊 Charts and visualizations
- ✅ Test suite

### What I learned

Owning a real product end-to-end: setting up the GitHub → Vercel deployment pipeline from scratch, modelling per-plate cost/revenue attribution in PostgreSQL, and leaning on Server Actions to ship a full-stack TypeScript app without a separate API. The unglamorous part — environment config, redeploy flow, data modelling — is what made it actually ship.

---

## 🇮🇹 Italiano

> Piattaforma di gestione integrata per autonoleggi — mezzi, operatori, manutenzioni e **conto economico per singola auto**, in un'unica dashboard.

> Realizzato per un autonoleggio reale; la demo live gira su dati di esempio. Pubblicato come riferimento di portfolio — dati di produzione e credenziali restano fuori dal repo, gestiti tramite variabili d'ambiente.

### Perché l'ho costruito

Il cliente gestiva una flotta a noleggio ma **non aveva visibilità del margine per singola targa**: ricavi, manutenzioni e costi operatori erano sparsi in fogli di calcolo. Sapeva che la flotta era complessivamente profittevole, ma non *quali auto* stessero erodendo il margine. FleetMargin trasforma tutto questo in un'unica fonte di verità: ricavi, costi e utile di ogni mezzo, in tempo reale.

### Cosa fa

- 📊 **Dashboard in tempo reale** — auto attive, operatori e noleggi, ricavi totali e **margine di profitto**, più la tabella del margine per singola auto (ricavi, costi, utile, %).
- 🚗 **Gestione flotta** — CRUD completo sui mezzi (targa, marca, modello, anno, proprietario), finestre di disponibilità e costo giornaliero configurabile.
- 👥 **Operatori** — registro tecnici con ruolo e costo orario, e storico attività per operatore.
- 🔧 **Attività di manutenzione** — tipi di attività personalizzati con costo fisso e durata standard; ogni esecuzione calcola in automatico il costo totale (manodopera + materiali + costo fisso) su auto e operatore.
- 🎫 **Noleggi** — contratti che collegano mezzi e clienti, con tracciamento attivi/storici.
- 📈 **Reportistica economica** — conto economico per auto generato da una view dedicata del database.

### Architettura

| Livello | Tecnologia | Note |
|------|------|------|
| Front-end | Next.js 16 + React 19 | App Router, Server Components |
| Styling | Tailwind CSS 4 | utility-first |
| Back-end | Next.js API Routes + Server Actions | full-stack TypeScript |
| Database | PostgreSQL (Neon) | serverless, SQL parametrizzato |
| Qualità | ESLint 9, TypeScript 5 | type-safe end-to-end |
| Hosting / CI | Vercel | deploy continuo GitHub → Vercel |

**Punti tecnici notevoli**
- **Server Actions su un data layer sottile**: tutte le mutazioni girano lato server (`'use server'`) con query **parametrizzate** type-safe via `@neondatabase/serverless`, revalidazione automatica della cache (`revalidatePath`) e redirect post-operazione — nessun layer API separato da mantenere.
- **Economia come view del database** (`vista_economia_auto`): il conto economico per auto è calcolato in SQL invece che nella UI, mantenendo la dashboard veloce e la logica in un unico punto.
- **Formattazione valuta localizzata** (IT-IT): `euro(1234.56) → "1.234,56 €"`.

### Roadmap
- 🔐 Autenticazione e autorizzazione
- 📄 Export report (PDF / Excel)
- 📊 Grafici e visualizzazioni
- ✅ Suite di test

### Cosa ho imparato

Gestire un prodotto reale dall'inizio alla fine: configurare da zero la pipeline di deploy GitHub → Vercel, modellare l'attribuzione costi/ricavi per targa in PostgreSQL e sfruttare le Server Actions per spedire un'app full-stack TypeScript senza un'API separata. La parte meno appariscente — configurazione ambiente, flusso di redeploy, modellazione dati — è quella che l'ha fatta davvero arrivare in produzione.

---

**FleetMargin v0.1.0** — MVP · realizzato e mantenuto da **Salvatore Rapisarda** ([@salvatorerapisardaai-max](https://github.com/salvatorerapisardaai-max))

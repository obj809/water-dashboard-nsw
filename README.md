# Water Dashboard NSW

A full-stack data visualization platform for monitoring and analyzing dam water resources across New South Wales, Australia. This monorepo contains a React frontend, Flask REST API backend, and database management systems for both local MySQL and cloud-hosted Supabase PostgreSQL environments.

![App Demo](frontend/screenshot.png)

## Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Sub-Projects](#sub-projects)
- [Features](#features)
- [Roadmap](#roadmap)
- [Known Issues](#known-issues)
- [Contributing](#contributing)
- [Contact](#contact)

## Overview

Water Dashboard NSW provides real-time insights into dam storage levels, water inflows, and releases across 36 NSW dams. The platform combines interactive data visualizations with historical trend analysis, including 12-month, 5-year, and 20-year rolling averages.

### Key Capabilities

- Real-time dam storage monitoring with automatic data refresh
- Historical time-series data with customizable date filtering
- Multi-period trend analysis across grouped dam systems
- Interactive charts built with Recharts, Chart.js, and D3.js
- RESTful API with auto-generated Swagger documentation
- Flexible database support for local development and cloud deployment

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        Frontend (React)                         │
│              TypeScript • Redux Toolkit • Vite                  │
└─────────────────────────┬───────────────────────────────────────┘
                          │ HTTP/REST
┌─────────────────────────▼───────────────────────────────────────┐
│                    Backend API (Flask)                          │
│            Flask-RESTX • SQLAlchemy • Swagger UI                │
└─────────────────────────┬───────────────────────────────────────┘
                          │ SQL
┌─────────────────────────▼───────────────────────────────────────┐
│                        Database Layer                           │
│         MySQL (Local) │ PostgreSQL (Supabase/Render)            │
└─────────────────────────────────────────────────────────────────┘
```

## Tech Stack

| Layer | Technologies |
|-------|--------------|
| Frontend | React 18, TypeScript, Vite, Redux Toolkit (RTK Query), React Router v6, SCSS |
| Visualization | Recharts, Chart.js, D3.js |
| Backend | Flask 3.1, Flask-RESTX, Flask-SQLAlchemy, Flask-Migrate, Gunicorn |
| Database | PostgreSQL, MySQL 8.0+, Supabase |
| Testing | Vitest, Testing Library, pytest |
| Data Processing | Pandas, OpenPyXL, psycopg2 |

## Getting Started

### Prerequisites

- Node.js 18+
- Python 3.10+
- MySQL 8.0+ (for local database)
- PostgreSQL (or Supabase account for cloud database)

### Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/water-dashboard-nsw.git
   cd water-dashboard-nsw
   ```

2. **Set up the database** (choose one)

   *Local MySQL:*
   ```bash
   cd database-local
   python3 -m venv venv && source venv/bin/activate
   pip install -r requirements.txt
   # Configure .env with MySQL credentials
   python3 scripts/local_db_create_db.py
   python3 scripts/local_db_create_schema.py
   python3 scripts/local_db_seed_data.py
   ```

   *Supabase PostgreSQL:*
   ```bash
   cd database-supabase
   python3 -m venv venv && source venv/bin/activate
   pip install -r requirements.txt
   # Configure .env with Supabase credentials
   python scripts/db_connect.py
   python scripts/create_schema.py
   python scripts/seed_data.py
   ```

3. **Start the backend API**
   ```bash
   cd backend
   python3 -m venv venv && source venv/bin/activate
   pip install -r requirements.txt
   # Configure .env with database credentials
   python run.py
   ```
   API available at `http://localhost:5001` with docs at `http://localhost:5001/api/docs`

4. **Start the frontend**
   ```bash
   cd frontend
   npm install
   npm run dev
   ```
   Dashboard available at `http://localhost:5173`

## Project Structure

```
water-dashboard-nsw/
├── frontend/               # React TypeScript dashboard
│   ├── src/
│   │   ├── components/     # Reusable UI components
│   │   ├── features/       # Redux slices and RTK Query APIs
│   │   ├── pages/          # Route-level components
│   │   └── styles/         # SCSS stylesheets
│   └── tests/              # Vitest test suites
│
├── backend/                # Flask REST API
│   ├── app/
│   │   ├── models/         # SQLAlchemy models
│   │   ├── routes/         # API endpoints
│   │   └── services/       # Business logic
│   └── tests/              # pytest test suites
│
├── database-local/         # Local MySQL setup
│   ├── scripts/            # Database creation and seeding
│   └── exports/            # Excel exports
│
├── database-supabase/      # Cloud PostgreSQL setup
│   └── scripts/            # Schema and seed scripts
│
└── docs/                   # Additional documentation
```

## Sub-Projects

| Project | Description | Documentation |
|---------|-------------|---------------|
| [frontend](./frontend) | React dashboard with interactive visualizations | [README](./frontend/README.md) |
| [backend](./backend) | Flask REST API with Swagger documentation | [README](./backend/README.md) |
| [database-local](./database-local) | Local MySQL database management | [README](./database-local/README.md) |
| [database-supabase](./database-supabase) | Cloud PostgreSQL with Supabase | [README](./database-supabase/README.md) |

## Features

### Frontend
- Real-time dam data fetching via RTK Query with automatic caching
- Advanced search functionality to filter dams by name
- Interactive data visualizations using multiple charting libraries
- Stacked-pages layout with smooth scroll navigation
- Individual dam detail pages with comprehensive statistics
- Full-screen graph views for in-depth analysis
- Responsive design across all device sizes

### Backend API
- Dam management with CRUD operations and geolocation data
- Real-time storage level snapshots for all dams
- Historical time-series data with date filtering
- Multi-period analysis (12-month, 5-year, 20-year averages)
- Interactive Swagger UI documentation
- Multi-database support (MySQL and PostgreSQL)

### Database
- 36 NSW dams with metadata (capacity, coordinates, identifiers)
- Dam grouping system (Sydney, popular, large, small, greatest released)
- 24-month historical snapshots with rolling average analysis
- Normalized schema with foreign key relationships

## Roadmap

- [ ] Historical comparison tool for dam levels across time periods
- [ ] Export functionality for graph data (CSV, PNG)
- [ ] Weather data integration for rainfall correlations
- [ ] Alert system for critical storage levels
- [ ] Dark mode theme
- [ ] E2E testing with Playwright
- [ ] Pagination support for large datasets
- [ ] Rate limiting and API authentication
- [ ] Real-time WebSocket updates
- [ ] Docker containerization
- [ ] Automated data refresh scheduling

## Known Issues

- Application requires backend API to be running; no offline mode currently implemented
- Some touch interactions on complex charts may require refinement on mobile
- Performance may degrade when rendering graphs with very large historical datasets
- Render deployment has a cold start; initial page load may be slow after periods of inactivity
- Current data is synthetic and does not reflect actual NSW dam levels

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Contact

**Oliver Jenkins**

- LinkedIn: [Visit Profile](https://linkedin.com/in/yourprofile)
- GitHub: [Check Projects](https://github.com/yourusername)
- Email: obj809@gmail.com

---

Thanks for your interest in this project. Feel free to reach out with any thoughts or questions.

© 2025 Oliver Jenkins
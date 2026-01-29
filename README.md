# Water Dashboard NSW

[![tests-frontend](https://github.com/obj809/frontend-water-dashboard-nsw/actions/workflows/test.yml/badge.svg?branch=main)](https://github.com/obj809/frontend-water-dashboard-nsw/actions/workflows/test.yml)
[![tests-backend](https://github.com/obj809/backend-water-dashboard-nsw/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/obj809/backend-water-dashboard-nsw/actions/workflows/ci.yml)

A modern data visualization dashboard displaying live and historical water dam information for New South Wales, Australia. Built with React, TypeScript, and Flask to provide real-time insights into dam storage levels, water inflows, and releases.

## Live Demo

**[https://frontend-water-dashboard-nsw.netlify.app/](https://frontend-water-dashboard-nsw.netlify.app/)**

## Screenshots

| Light Mode | Dark Mode |
|------------|-----------|
| ![Light Mode](images/project-screenshot-light.png) | ![Dark Mode](images/project-screenshot-dark.png) |

## Architecture

![Project Architecture](images/project-diagram.png)

### Database Schema

![Database ERD](database-erd.png)

## Project Repositories

| Repository | Description | Tech Stack |
|------------|-------------|------------|
| [Frontend](https://github.com/obj809/frontend-water-dashboard-nsw) | React dashboard UI | React 18, TypeScript, Vite, Redux Toolkit, Recharts, Chart.js, D3.js |
| [Backend](https://github.com/obj809/backend-water-dashboard-nsw) | REST API service | Flask 3.1, Flask-RESTX, SQLAlchemy, PostgreSQL |
| [Local Database](https://github.com/obj809/local-db-water-dashboard-nsw) | Local MySQL setup | Python, MySQL, Pandas, OpenPyXL |
| [Supabase Database](https://github.com/obj809/supabase-water-dashboard-nsw) | Cloud PostgreSQL setup | Python, PostgreSQL, Supabase |

## Features

- Real-time dam data fetching with automatic caching via RTK Query
- Advanced search functionality to filter dams by name
- Interactive data visualizations using Recharts, Chart.js, and D3
- Stacked-pages layout with smooth scroll navigation
- Individual dam detail pages with comprehensive statistics
- Full-screen graph views for in-depth analysis
- Multi-period analysis (12-month, 5-year, 20-year averages)
- Interactive Swagger UI API documentation

## Quick Start

### Prerequisites

- Node.js 18+
- Python 3.10+
- Docker (optional)

### Using Docker

```bash
docker-compose up --build   # Build and start all services
docker-compose down         # Stop services
docker-compose logs -f      # Follow logs
```

### Manual Setup

**Backend:**
```bash
cd backend-water-dashboard-nsw
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
python run.py
# API docs available at http://localhost:5001/api/docs
```

**Frontend:**
```bash
cd frontend-water-dashboard-nsw
npm install
npm run dev
# Dashboard available at http://localhost:5173
```

## API Endpoints

| Endpoint | Description |
|----------|-------------|
| `GET /api/dams` | List all dams with metadata |
| `GET /api/dams/{id}` | Get specific dam details |
| `GET /api/dams/{id}/storage` | Get current storage levels |
| `GET /api/dams/{id}/history` | Get historical time-series data |
| `GET /api/analysis` | Get system-wide rolling averages |

Full API documentation available at `/api/docs` when backend is running.

## Tech Stack Overview

### Frontend
- **Framework:** React 18 with TypeScript
- **Build Tool:** Vite
- **State Management:** Redux Toolkit (RTK Query)
- **Routing:** React Router v6
- **Charts:** Recharts, Chart.js, D3.js
- **Styling:** SCSS
- **Testing:** Vitest + Testing Library

### Backend
- **Framework:** Flask 3.1
- **API Documentation:** Flask-RESTX with Swagger UI
- **ORM:** Flask-SQLAlchemy
- **Database:** PostgreSQL (production) / MySQL (local)
- **Testing:** pytest
- **Deployment:** Render with Gunicorn

## Deployment

- **Frontend:** Netlify (automatic deployments from main branch)
- **Backend:** Render
- **Database:** Supabase PostgreSQL

![AWS Pipeline](images/aws-pipeline.png)

## Project Structure

```
water-dashboard-nsw/           # This repo - documentation & overview
├── images/                    # Architecture diagrams & screenshots
├── gifs/                      # Demo animations
├── database-erd.png           # Database schema diagram
├── commands.md                # Docker command reference
└── README.md

frontend-water-dashboard-nsw/  # Separate repo
backend-water-dashboard-nsw/   # Separate repo
local-db-water-dashboard-nsw/  # Separate repo
supabase-water-dashboard-nsw/  # Separate repo
```

## Contact

**Oliver Jenkins**

- [LinkedIn](https://www.linkedin.com/in/yourprofile)
- [GitHub](https://github.com/obj809)
- Email: obj809@gmail.com

---

Oliver Jenkins © 2025

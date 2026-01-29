# Water Dashboard NSW

[![tests-frontend](https://github.com/obj809/frontend-water-dashboard-nsw/actions/workflows/test.yml/badge.svg?branch=main)](https://github.com/obj809/frontend-water-dashboard-nsw/actions/workflows/test.yml)
[![tests-backend](https://github.com/obj809/backend-water-dashboard-nsw/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/obj809/backend-water-dashboard-nsw/actions/workflows/ci.yml)

A modern full-stack data visualization platform for monitoring real-time and historical water storage levels across 36 dams in New South Wales, Australia. The system provides comprehensive analytics including multi-year rolling averages, historical trends, and interactive visualizations for water resource management.

## Live Deployment

[https://frontend-water-dashboard-nsw.netlify.app/](https://frontend-water-dashboard-nsw.netlify.app/)

## Screenshots

![Dark Mode](images/project-screenshot-dark.png)
![Light Mode](images/project-screenshot-light.png)
![Dashboard View](images/project-screenshot-2.png)

## Architecture

![Project Architecture](images/project-diagram.png)
![AWS Pipeline](images/aws-pipeline.png)
![Database ERD](database-erd.png)

## Project Repositories

- **[Frontend](https://github.com/obj809/frontend-water-dashboard-nsw)** - React + TypeScript dashboard with Redux Toolkit
- **[Backend](https://github.com/obj809/backend-water-dashboard-nsw)** - Flask REST API with Swagger documentation
- **[Local Database](https://github.com/obj809/local-db-water-dashboard-nsw)** - MySQL data pipeline and ETL scripts
- **[Supabase Database](https://github.com/obj809/supabase-water-dashboard-nsw)** - PostgreSQL cloud deployment

## Tech Stack

### Frontend
- React 18 with TypeScript
- Redux Toolkit (RTK Query for API caching)
- Recharts, Chart.js, D3.js for data visualization
- React Router v6, SCSS styling
- Vite build tool, Vitest testing

### Backend
- Flask 3.1 with Flask-RESTX (Swagger UI)
- PostgreSQL/MySQL with SQLAlchemy ORM
- Flask-Migrate for schema management
- Gunicorn production server
- Pytest testing, GitHub Actions CI/CD

### Database
- MySQL 8.0+ (local development)
- PostgreSQL (Supabase cloud production)
- Python ETL pipelines with Pandas
- 24-month historical data retention
- Multi-period rolling averages (12-month, 5-year, 20-year)

## Key Features

- Real-time dam storage monitoring with automatic data refresh
- Advanced search and filtering by dam name or region
- Interactive time-series charts with full-screen analysis views
- Historical trend analysis with 12-month, 5-year, and 20-year averages
- Individual dam detail pages with comprehensive statistics
- Responsive design with dark/light mode support
- RESTful API with interactive Swagger documentation
- Normalized relational database with 34+ NSW dams

## Quick Start with Docker

```bash
# Build and start all services
docker-compose up --build

# View logs
docker-compose logs -f

# Stop all services
docker-compose down
```

## Manual Setup

### Backend API
```bash
cd backend
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
python run.py
```
Access API docs at `http://localhost:5001/api/docs`

### Frontend Dashboard
```bash
cd frontend
npm install
npm run dev
```
Access dashboard at `http://localhost:5173`

### Database Setup
```bash
cd local-db-water-dashboard-nsw
pip install -r requirements.txt
# Configure .env with MySQL credentials
python seed_data.py
```

## API Documentation

![API Endpoints](api-documentation.png)

Core endpoints include:
- `GET /api/dams` - List all dams with metadata
- `GET /api/dams/{dam_id}` - Retrieve specific dam details
- `GET /api/water-snapshots` - Historical water level data
- `GET /api/analysis` - Rolling average calculations

## Database Schema

The system uses a normalized relational design with:
- **Dams table**: Metadata for 36 NSW facilities (capacity, coordinates, identifiers)
- **Water Snapshots**: Monthly storage measurements with 24-month retention
- **Analysis tables**: Pre-computed rolling averages for performance
- **Dam Groups**: Regional categorization (Sydney, popular, large, small)

## Design Goals

- **Data-first interface**: Clean, intuitive visualizations prioritizing clarity
- **Performance optimization**: RTK Query caching, indexed database queries
- **Scalability**: Modular architecture supporting additional data sources
- **Developer experience**: Comprehensive testing, Swagger docs, type safety

## Learning Highlights

- Implemented Redux Toolkit for efficient client-side state management
- Built RESTful API with Flask-RESTX automatic Swagger generation
- Designed normalized database schema with composite keys and foreign key constraints
- Deployed full-stack application with Netlify (frontend) and Render (backend)
- Configured CI/CD pipelines with GitHub Actions for automated testing

## Challenges & Solutions

- **Multi-database support**: Implemented environment-based provider switching (MySQL/PostgreSQL)
- **Large dataset performance**: Added RTK Query caching and considered pagination strategies
- **Cold start delays**: Documented Render's free-tier limitations for production planning
- **Composite primary keys**: Designed custom route parameters for multi-dimensional analysis queries

## Future Improvements

- WebSocket integration for real-time data streaming
- API authentication and rate limiting
- Pagination for large historical datasets
- Enhanced mobile chart interactions
- Automated data refresh pipelines

## Contact

Created by [obj809](https://github.com/obj809)

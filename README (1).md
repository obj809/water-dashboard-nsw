# Water Dashboard NSW

## Project Overview
Full-stack platform for monitoring NSW dam water resources with real-time visualization and historical analysis.

## Screenshot
![App Demo](frontend/screenshot.png)

## Table of Contents
- [Frontend](#frontend)
- [Backend](#backend)
- [Database](#database)
- [General](#general)

## Goals & MVP
Interactive dashboard displaying real-time storage levels, historical data, and rolling averages (12-month, 5-year, 20-year) for 36 NSW dams.

## Build Strategy
React frontend → Flask REST API → MySQL (local) / PostgreSQL (production)

<a id="frontend"></a>
# Frontend - React Dashboard

## Tech Stack
React 18, TypeScript, Vite, Redux Toolkit, Recharts, Chart.js, D3.js, SCSS

## How To Use
Run `npm install && npm run dev` → `http://localhost:5173`

## Project Features
- [x] RTK Query caching with real-time data fetching
- [x] Interactive multi-library visualizations
- [x] Search, stacked-pages navigation, full-screen graphs

<a id="backend"></a>
# Backend - Flask API

## Tech Stack
Flask 3.1, Flask-RESTX, SQLAlchemy, PostgreSQL/MySQL, pytest

## How To Use
Run `pip install -r requirements.txt && python run.py` → `http://localhost:5001/api/docs`

## Project Features
- [x] CRUD operations with Swagger documentation
- [x] Historical time-series with date filtering
- [x] Multi-period rolling average analysis

<a id="database"></a>
# Database - MySQL & PostgreSQL

## Tech Stack
Python 3, MySQL 8.0+, PostgreSQL (Supabase), Pandas, OpenPyXL, psycopg2-binary, python-dotenv

## Design Goals
- **Data Integrity:** Foreign keys with cascading relationships
- **Idempotency:** Upsert operations for safe re-runs
- **Security:** Parameterized queries to prevent SQL injection
- **Modularity:** Dependency-ordered seeding scripts

## How To Use
1. Create virtual environment: `python3 -m venv venv && source venv/bin/activate`
2. Install dependencies: `pip install -r requirements.txt`
3. Configure `.env` with database credentials
4. Run setup scripts: `python scripts/create_schema.py && python scripts/seed_data.py`

## Project Features
- [x] 36 NSW dams with metadata (capacity, coordinates, identifiers)
- [x] Dam grouping system (Sydney, popular, large, small, greatest released)
- [x] 24-month historical snapshots with time-series data
- [x] Rolling average analysis (12-month, 5-year, 20-year)
- [x] Excel export with customizable table filtering

<a id="general"></a>
# General

## Additions & Improvements
- [ ] Data export (CSV, PNG), weather integration, alerts
- [ ] Dark mode, pagination, WebSocket updates, Docker

## Learning Highlights
RTK Query caching, multi-charting integration, Flask-RESTX documentation, multi-database SQLAlchemy configuration

## Challenges
Vite proxy setup, composite primary keys in Flask-RESTX, foreign key constraint ordering

## Contact Me
[LinkedIn](https://linkedin.com/in/yourprofile) · [GitHub](https://github.com/yourusername) · obj809@gmail.com

Oliver Jenkins © 2025

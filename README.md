# Water Dashboard NSW

![test-frontend](https://github.com/obj809/frontend-water-dashboard-nsw/actions/workflows/test.yml/badge.svg?branch=main)
![tests-backend](https://github.com/obj809/backend-water-dashboard-nsw/actions/workflows/ci.yml/badge.svg)

## Project Overview
A full-stack platform for monitoring dam water resources across New South Wales, Australia. Features a React dashboard, Flask REST API, and flexible database support for MySQL and PostgreSQL.

## Live Deployment

- [Live Deployment](https://frontend-water-dashboard-nsw.netlify.app/)

## Project Links

- [Frontend](https://github.com/obj809/frontend-water-dashboard-nsw)
- [Backend](https://github.com/obj809/backend-water-dashboard-nsw)
- [Local Database](https://github.com/obj809/local-db-water-dashboard-nsw)
- [Supabase](https://github.com/obj809/supabase-water-dashboard-nsw)

## Table of Contents
- [Frontend](#frontend)
- [Backend](#backend)
- [Database](#database)

<a id="frontend"></a>
# Frontend - React Dashboard

<img src="./screen-recording.gif" alt="App Demo" width="960"/>

## Tech Stack
React 18, TypeScript, Vite, Redux Toolkit (RTK Query), React Router v6, Recharts, Chart.js, D3.js, SCSS, Vitest

## Design Goals
Data-first interface with responsive design, RTK Query caching for performance, and smooth navigation.

## How To Use
1. Ensure backend API is running on `http://127.0.0.1:5001`
2. Run `npm install` then `npm run dev`
3. Navigate to `http://localhost:5173`

## Project Features
- [x] Real-time data fetching with RTK Query caching
- [x] Search functionality and stacked-pages navigation
- [x] Interactive visualizations (Recharts, Chart.js, D3)
- [x] Full-screen graph views and dam detail pages

<a id="backend"></a>
# Backend - Flask API

![API documentation](images/api-documentation-dark.png)

## Tech Stack
Flask 3.1, Flask-RESTX, Flask-SQLAlchemy, Flask-Migrate, PostgreSQL/MySQL, pytest, Gunicorn

## Design Goals
RESTful architecture with auto-generated Swagger documentation and multi-database support.

## How To Use
1. Run `python3 -m venv venv && source venv/bin/activate && pip install -r requirements.txt`
2. Configure `.env` with database credentials
3. Run `python run.py` — docs at `http://localhost:5001/api/docs`

## Project Features
- [x] CRUD operations with geolocation data
- [x] Historical time-series data with date filtering
- [x] Multi-period analysis (12-month, 5-year, 20-year averages)
- [x] Interactive Swagger UI and CI/CD with GitHub Actions

<a id="database"></a>
# Database - MySQL & Supabase PostgreSQL

![Database schema](images/database-schema.png)

## Tech Stack
Python 3, MySQL 8.0+, PostgreSQL (Supabase), Pandas, OpenPyXL, psycopg2-binary

## Design Goals
Normalized schema with foreign key integrity, idempotent upsert operations, and modular dependency-ordered seeding scripts.

## How To Use
1. Run `python3 -m venv venv && source venv/bin/activate && pip install -r requirements.txt`
2. Configure `.env` with database credentials
3. Run `python scripts/create_schema.py && python scripts/seed_data.py`

## Project Features
- [x] 36 NSW dams with metadata, coordinates, and grouping system
- [x] 24-month historical snapshots with time-series data
- [x] Rolling average analysis (12-month, 5-year, 20-year)

## Contact Me
- Visit my [LinkedIn](https://www.linkedin.com/in/obj809/) for more details.
- Check out my [GitHub](https://github.com/cyberforge1) for more projects.
- Or send me an email at obj809@gmail.com
<br />
Thanks for your interest in this project. Feel free to reach out with any thoughts or questions.
<br />
<br />
Oliver Jenkins © 2025
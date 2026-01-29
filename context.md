Water Dashboard NSW Frontend
Tests

Project Overview
A modern data visualization dashboard displaying live and historical water dam information for New South Wales, Australia. Built with React, TypeScript, Redux Toolkit, and multiple charting libraries to provide real-time insights into dam storage levels, water inflows, and releases.

Screenshot
App Demo

Table of Contents
Goals & MVP
Tech Stack
How To Use
Design Goals
Project Features
Additions & Improvements
Learning Highlights
Known Issues
Challenges
Goals & MVP
The goal of this project is to create an accessible, interactive dashboard for visualizing NSW dam water data. By leveraging RTK Query for efficient API state management and multiple charting libraries, the application provides real-time insights into water resources while maintaining a responsive, user-friendly interface.

Tech Stack
React 18
TypeScript
Vite
Redux Toolkit (RTK Query)
React Router v6
Recharts
Chart.js
D3.js
SCSS
Vitest + Testing Library
How To Use
Ensure the backend API is running on http://127.0.0.1:5001.
Install dependencies with npm install.
Start the development server with npm run dev.
Navigate to http://localhost:5173 to view the dashboard.
Use the search bar to find specific dams or scroll through the stacked pages.
Design Goals
Data-First Interface: Prioritize clear, accurate visualization of complex water data.
Responsive Design: Ensure optimal viewing experience across all device sizes.
Performance: Leverage RTK Query caching for fast load times and minimal API calls.
Intuitive Navigation: Implement smooth-scroll stacked pages for seamless browsing.
Project Features
 Real-time dam data fetching via RTK Query with automatic caching
 Advanced search functionality to filter dams by name
 Interactive data visualizations using Recharts, Chart.js, and D3
 Stacked-pages layout with smooth scroll navigation
 Individual dam detail pages with comprehensive statistics
 Full-screen graph views for in-depth analysis
 Comprehensive test suite with Vitest and Testing Library
Additions & Improvements
 Implement historical comparison tool for dam levels across time periods
 Add export functionality for graph data (CSV, PNG)
 Integrate weather data to show rainfall correlations
 Add alert system for critical storage levels
 Implement dark mode theme
 Add E2E testing with Playwright
Learning Highlights
Leveraging RTK Query for automatic caching, background refetching, and API state management
Integrating multiple charting libraries (Recharts, Chart.js, D3) for different visualization needs
Configuring Vite proxy for seamless backend communication during development
Implementing comprehensive test coverage with Vitest and Testing Library
Building responsive data visualizations that work across all device sizes
Known Issues
Application requires backend API to be running; no offline mode currently implemented
Some touch interactions on complex charts may require refinement on mobile
Performance may degrade when rendering graphs with very large historical datasets
Challenges
Configuring Vite proxy to seamlessly communicate with Flask backend
Evaluating and integrating multiple charting libraries for different use cases
Ensuring charts render correctly and remain interactive across all device sizes
Maintaining TypeScript type safety with dynamic API responses
Contact Me
Visit my LinkedIn for more details.
Check out my GitHub for more projects.
Or send me an email at obj809@gmail.com
Thanks for your interest in this project. Feel free to reach out with any thoughts or questions.

Oliver Jenkins © 2025



Water Dashboard NSW Backend API
tests-backend

Project Overview
A Flask REST API backend providing dam storage and water resource data for New South Wales, Australia. The API delivers real-time and historical water data including storage levels, inflow/release metrics, and multi-year trend analysis across NSW dam systems.

Screenshot
Application Screenshot

Table of Contents
Goals & MVP
Tech Stack
How To Use
Design Goals
Project Features
Additions & Improvements
Learning Highlights
Known Issues
Challenges
Contact Me
Goals & MVP
Build a robust REST API for NSW dam and water resource data that supports real-time storage monitoring, historical data queries with date filtering, and analytical insights including 12-month, 5-year, and 20-year averages across grouped dam systems.

Tech Stack
Flask 3.1
Flask-RESTX
Flask-SQLAlchemy
Flask-Migrate
PostgreSQL / MySQL
pytest
Gunicorn
Render
How To Use
Clone the repository and install dependencies:
python3 -m venv venv && source venv/bin/activate && pip install -r requirements.txt
Configure your .env file with database credentials and run:
python run.py
Access the API documentation at http://localhost:5001/api/docs
Design Goals
RESTful Architecture: Clean, predictable API design following REST principles
Automatic Documentation: Self-documenting API with interactive Swagger UI
Database Flexibility: Support for multiple database backends (MySQL, PostgreSQL)
Test-Driven Development: Comprehensive test suite with high code coverage
Project Features
 Dam management with CRUD operations and geolocation data
 Real-time storage level snapshots for all dams
 Historical time-series data with date filtering
 Multi-period analysis (12-month, 5-year, 20-year averages)
 Interactive Swagger UI documentation
 Automated CI/CD with GitHub Actions
Additions & Improvements
 Pagination support for large datasets
 Rate limiting and API authentication
 Real-time WebSocket updates
 Docker containerization
Learning Highlights
Implementing automatic API documentation with Flask-RESTX and Swagger UI
Designing complex SQLAlchemy relationships (one-to-one, one-to-many, many-to-many)
Building comprehensive pytest test suites with in-memory SQLite for test isolation
Implementing multi-database support with environment-based configuration
Known Issues
Large dataset queries without pagination may cause performance issues
Fixed numeric precision - Numeric columns have fixed precision (e.g., 10,3 for volumes) which may truncate extremely large values
Render deployment has a cold start - Initial page load may be slow after periods of inactivity
Challenges
Multi-Database Support
Challenge: Supporting both MySQL (local) and PostgreSQL (production) with different connection formats.
Solution: Implemented flexible configuration with DB_PROVIDER environment variable and SQLAlchemy's database-agnostic ORM.
Composite Primary Keys
Challenge: SpecificDamAnalysis uses composite primary key (dam_id, analysis_date) requiring special Flask-RESTX handling.
Solution: Created custom route parameters and date parsing utilities for proper database queries.
Contact Me
Visit my LinkedIn for more details.
Check out my GitHub for more projects.
Or send me an email at obj809@gmail.com

Thanks for your interest in this project. Feel free to reach out with any thoughts or questions.

Oliver Jenkins © 2025


Local Database Water Dashboard NSW
Project Overview
A local MySQL-based system for tracking and analyzing dam data across NSW, Australia. Built with Python, MySQL, Pandas, and OpenPyXL.

Table of Contents
Goals & MVP
Tech Stack
How To Use
Design Goals
Project Features
Additions & Improvements
Learning Highlights
Known Issues
Challenges
Goals & MVP
Create a centralized system that stores dam metadata, tracks water storage levels, archives historical data, and generates analytical reports with rolling averages (12-month, 5-year, 20-year) for 34 NSW dams.

Tech Stack
Python 3
MySQL 8.0+
Pandas
OpenPyXL
python-dotenv
How To Use
Create virtual environment: python3 -m venv venv && source venv/bin/activate
Install dependencies: pip install -r requirements.txt
Create .env file with MySQL credentials (LOCAL_DB_HOST, LOCAL_DB_PORT, LOCAL_DB_NAME, LOCAL_DB_USER, LOCAL_DB_PASSWORD)
Run database setup: python3 scripts/local_db_create_db.py && python3 scripts/local_db_create_schema.py && python3 scripts/local_db_seed_data.py
Export to Excel: python scripts/local_export_mysql_to_excel.py
Design Goals
Data Integrity: Foreign keys with cascading relationships
Idempotency: Upsert operations for safe re-runs
Security: Parameterized queries to prevent SQL injection
Modularity: Separate seeding scripts with dependency-ordered execution
Project Features
 34 NSW dams with metadata (capacity, coordinates, identifiers)
 Dam grouping system (Sydney, popular, large, small, greatest released)
 24-month historical snapshots with rolling average analysis
 Excel export with customizable table filtering
Additions & Improvements
 Dashboard visualization layer
 Automated data refresh scheduling
 Multi-region support
Learning Highlights
Normalized database schema design with foreign key relationships
Orchestrated data pipelines with dependency ordering
Upsert patterns and composite keys in SQL
Known Issues
Local MySQL only; no cloud deployment configuration
Synthetic data; does not reflect actual NSW dam levels
Manual refresh required; no automated scheduling
Challenges
Establishing correct seeding order for foreign key constraints
Designing composite primary keys for analysis tables
Generating realistic synthetic historical data patterns
Contact Me
Visit my LinkedIn for more details.
Check out my GitHub for more projects.
Or send me an email at obj809@gmail.com

Thanks for your interest in this project. Feel free to reach out with any thoughts or questions.

Oliver Jenkins © 2025


Supabase Water Dashboard NSW
A Supabase PostgreSQL-based system for tracking and analyzing dam data across NSW, Australia. Built with Python and psycopg2.

Table of Contents
Goals & MVP
Tech Stack
How To Use
Design Goals
Project Features
Project Structure
Additions & Improvements
Learning Highlights
Known Issues
Challenges
Contact
Goals & MVP
Create a cloud-hosted system that stores dam metadata, tracks water storage levels, archives historical data, and generates analytical reports with rolling averages (12-month, 5-year, 20-year) for 36 NSW dams.

Tech Stack
Python 3
PostgreSQL (Supabase)
psycopg2-binary
python-dateutil
python-dotenv
How To Use
Create virtual environment: python3 -m venv venv && source venv/bin/activate
Install dependencies: pip install -r requirements.txt
Create .env file with Supabase credentials (see example.env)
Run database setup: python scripts/db_connect.py && python scripts/create_schema.py && python scripts/seed_data.py
Verify data: python scripts/verify_seed.py
Design Goals
Cloud-Native: Hosted on Supabase PostgreSQL for accessibility
Data Integrity: Foreign keys with cascading relationships
Idempotency: Upsert operations for safe re-runs
Security: Parameterized queries to prevent SQL injection
Modularity: Separate seeding scripts with dependency-ordered execution
Project Features
Dam grouping system (Sydney, popular, large, small, greatest released)
24-month historical snapshots with time-series data
Per-dam and system-wide rolling average analysis (12-month, 5-year, 20-year)
Learning Highlights
Normalized database schema design with foreign key relationships
Cloud PostgreSQL deployment with Supabase
Orchestrated data pipelines with dependency ordering
Upsert patterns and composite primary keys in PostgreSQL
Known Issues
Synthetic data; does not reflect actual NSW dam levels
Manual refresh required; no automated scheduling
Analysis calculations use fixed values
Challenges
Establishing correct seeding order for foreign key constraints
Designing composite primary keys for analysis tables
Generating realistic synthetic historical data patterns
Contact Me
Visit my LinkedIn for more details.
Check out my GitHub for more projects.
Or send me an email at obj809@gmail.com

Thanks for your interest in this project. Feel free to reach out with any thoughts or questions.

Oliver Jenkins © 2025
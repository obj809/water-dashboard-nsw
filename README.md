# Water Dashboard NSW

[![tests-frontend](https://github.com/obj809/frontend-water-dashboard-nsw/actions/workflows/test.yml/badge.svg?branch=main)](https://github.com/obj809/frontend-water-dashboard-nsw/actions/workflows/test.yml)  
[![tests-backend](https://github.com/obj809/backend-water-dashboard-nsw/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/obj809/backend-water-dashboard-nsw/actions/workflows/ci.yml)

## Deployment Link

[Live Deployment](https://frontend-water-dashboard-nsw.netlify.app/)

## Project Overview

A full-stack data dashboard application that visualizes and analyzes water storage data from dams across New South Wales, Australia. The project integrates live data from the WaterNSW API, processes it through an automated pipeline, stores it in a MySQL database, and displays interactive visualizations through a modern React TypeScript frontend. The application features real-time analytics powered by PySpark and includes comprehensive historical data analysis spanning up to 20 years.

### Key Features

- Real-time dam water level monitoring across NSW
- Interactive charts and visualizations using Chart.js
- Historical data analysis (12 months, 5 years, 20 years)
- Google Maps integration showing dam locations
- Search functionality to find specific dams
- Dam grouping capabilities (Sydney dams, large dams, etc.)
- PySpark-powered analytics for large-scale data processing
- Automated AWS-based data pipeline for monthly updates

## Project Links

- [Frontend](https://github.com/obj809/frontend-water-dashboard-nsw)

- [Backend](https://github.com/obj809/backend-water-dashboard-nsw)

- [Local Database](https://github.com/obj809/local-db-water-dashboard-nsw)

- [Supabase Database](https://github.com/obj809/supabase-water-dashboard-nsw)

- [Data Pipeline](https://github.com/obj809/aws-etl-pipeline)

## Table of Contents

- [Technology Stack](#technology-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Project Structure](#project-structure)
- [API Documentation](#api-documentation)
- [Data Pipeline](#data-pipeline)
- [Deployment](#deployment)
- [Known Issues](#known-issues)

## Technology Stack

### Frontend
- **Framework**: React 18.3.1 with TypeScript
- **Build Tool**: Vite 5.3.1
- **Routing**: React Router DOM 6.24.0
- **Charts**: Chart.js 4.4.3 with react-chartjs-2
- **Maps**: @react-google-maps/api 2.19.3
- **Styling**: Sass 1.77.6
- **Icons**: FontAwesome 6.5.2

### Backend
- **Framework**: Flask 2.0.1
- **Database ORM**: SQLAlchemy 1.4.22, Flask-SQLAlchemy 2.5.1
- **Database Driver**: PyMySQL 1.1.1, mysql-connector-python 8.0.26
- **Analytics**: PySpark 3.1.2
- **CORS**: Flask-CORS 3.0.10

### Data Collection & Processing
- **Data Processing**: Pandas 1.3.5
- **Database**: PyMySQL 1.0.2
- **HTTP Requests**: Requests 2.26.0
- **Excel Export**: openpyxl 3.0.9

### Database
- **RDBMS**: MySQL 8.0
- **Cloud Database**: AWS RDS

### Infrastructure & DevOps
- **Cloud Services**: AWS Lambda, AWS S3, AWS RDS, AWS ECS
- **Containerization**: Docker with nginx
- **Serverless Compute**: AWS Fargate
- **Frontend Hosting**: Netlify

## Prerequisites

Before you begin, ensure you have the following installed:

- **Python** 3.8 or higher
- **Node.js** 16.x or higher
- **npm** 7.x or higher
- **MySQL** 8.0 or higher
- **Java** 8 or higher (required for PySpark)

### API Access Requirements

- **WaterNSW API Credentials**: OAuth2 credentials from the WaterNSW API
- **Google Maps API Key**: Required for map functionality in the frontend

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/obj809/water-dashboard-nsw.git
cd water-dashboard-nsw
```

### 2. Backend Setup

```bash
cd flask-backend-retired

# Create virtual environment
python3 -m venv venv

# Activate virtual environment
# On macOS/Linux:
source venv/bin/activate
# On Windows:
# venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### 3. Frontend Setup

```bash
cd react-frontend-retired

# Install dependencies
npm install
```

### 4. Database Preparation Setup

```bash
cd database-prep

# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 5. Database Setup

```bash
# Log into MySQL
mysql -u root -p

# Create database
CREATE DATABASE dam_data;
USE dam_data;
```

Then run the schema from the [Database](#database) section below.

## Configuration

### Backend Configuration

Create a `.env` file in the `flask-backend-retired` directory:

```env
# Database Configuration
DB_HOST=localhost
DB_PORT=3306
DB_NAME=dam_data
DB_USER=your_mysql_username
DB_PASSWORD=your_mysql_password

# SQLAlchemy
SQLALCHEMY_DATABASE_URI=mysql+pymysql://your_mysql_username:your_mysql_password@localhost:3306/dam_data

# Flask
SECRET_KEY=your_secret_key_here
FLASK_APP=run.py
FLASK_ENV=development
```

### Frontend Configuration

Create a `.env` file in the `react-frontend-retired` directory:

```env
VITE_GOOGLE_MAPS_API_KEY=your_google_maps_api_key
VITE_API_BASE_URL=http://127.0.0.1:5000
```

### Database Preparation Configuration

Create a `.env` file in the `database-prep` directory:

```env
# Database Configuration
DB_HOST=localhost
DB_PORT=3306
DB_NAME=dam_data
DB_USER=your_mysql_username
DB_PASSWORD=your_mysql_password

# WaterNSW API
AUTHORIZATION_HEADER=Basic your_base64_encoded_credentials
```

## Running the Application

### 1. Start MySQL Database

Ensure MySQL is running:

```bash
# macOS
brew services start mysql

# Linux
sudo systemctl start mysql
```

### 2. Populate the Database (First Time Only)

```bash
cd database-prep

# Activate virtual environment
source venv/bin/activate

# Get OAuth2 token
python3 requests/oauth2_request.py

# Collect data from WaterNSW API
python3 requests/list_of_dams.py
python3 requests/latest_data.py
python3 requests/collect_all_data.py

# Seed the database
python3 database-seeding/insert_dams.py
python3 database-seeding/insert_latest_data.py
python3 database-seeding/insert_all_data.py
```

### 3. Start the Backend Server

```bash
cd flask-backend-retired

# Activate virtual environment
source venv/bin/activate

# Run the Flask server
python3 run.py
```

The backend API will be available at `http://127.0.0.1:5000`

### 4. Start the Frontend Development Server

In a new terminal:

```bash
cd react-frontend-retired

# Start the development server
npm run dev
```

The frontend will be available at `http://localhost:5173`

## Project Structure

```
water-dashboard-nsw/
├── flask-backend-retired/          # Flask REST API
│   ├── app/
│   │   ├── __init__.py            # Flask app factory
│   │   ├── config.py              # Configuration settings
│   │   ├── models.py              # SQLAlchemy database models
│   │   ├── routes.py              # API endpoints
│   │   ├── pyspark_analysis.py   # PySpark analytics functions
│   │   └── db_info.py             # Database utilities
│   ├── run.py                     # Application entry point
│   └── requirements.txt           # Python dependencies
│
├── react-frontend-retired/         # React TypeScript frontend
│   ├── src/
│   │   ├── components/            # Reusable UI components
│   │   │   ├── DamContent/
│   │   │   ├── DamGroupSelector/
│   │   │   ├── FigureBox/
│   │   │   ├── Footer/
│   │   │   ├── GoogleMapComponent/
│   │   │   ├── IndividualDamCard/
│   │   │   ├── OpenListOfDams/
│   │   │   ├── SearchForDam/
│   │   │   └── TextBox/
│   │   ├── pages/                 # Route pages
│   │   │   ├── HomePage/
│   │   │   ├── SelectedDamPage/
│   │   │   ├── DamListPage/
│   │   │   ├── PageTwo/
│   │   │   ├── PageThree/
│   │   │   ├── PageFour/
│   │   │   └── PageFive/
│   │   ├── graphs/                # Chart.js visualizations
│   │   │   ├── DamCapacityGraph/
│   │   │   ├── DamCapacityPercentageGraph/
│   │   │   └── DamStorageGraph/
│   │   ├── services/
│   │   │   └── api.ts             # API service functions
│   │   ├── App.tsx                # Main application component
│   │   └── main.tsx               # Application entry point
│   ├── vite.config.ts             # Vite configuration
│   ├── Dockerfile                 # Docker configuration
│   └── package.json               # npm dependencies
│
├── database-prep/                  # Data collection & seeding
│   ├── requests/                  # WaterNSW API scripts
│   │   ├── oauth2_request.py     # OAuth2 authentication
│   │   ├── list_of_dams.py       # Fetch dam list
│   │   ├── latest_data.py        # Fetch latest readings
│   │   └── collect_all_data.py   # Fetch historical data
│   ├── database-seeding/          # Database population scripts
│   │   ├── insert_dams.py        # Seed dams table
│   │   ├── insert_latest_data.py # Seed latest_data table
│   │   └── insert_all_data.py    # Seed dam_resources table
│   ├── json_to_excel/             # Data export utilities
│   ├── database-schema.sql        # Database schema
│   └── requirements.txt           # Python dependencies
│
└── README.md                      # This file
```

## Frontend
<img src="./gifs/drone.gif" alt="App Demo" width="900" height="600"/>

## API Documentation

![API documentation](./api-documentation.png)

### Base URL
```
http://127.0.0.1:5000
```

### Endpoints

#### General
- `GET /` - Health check endpoint

#### Dam Information
- `GET /latestdata/<dam_id>` - Get latest data for a specific dam
- `GET /damnames` - Get list of all dam names
- `GET /damdata?dam_name=<name>` - Get data by dam name
- `GET /damsdata/<group_name>` - Get data for a group of dams
  - Available groups: `sydney_dams`, `popular_dams`, `large_dams`, `small_dams`, `greatest_released`

#### Historical Data
- `GET /damresources/<dam_id>` - Get 12 months of historical data for a specific dam
- `GET /damdata/12_months/<group_name>` - Get 12 months of data for a dam group

#### Analytics (PySpark-powered)
- `GET /average_percentage_full/12_months` - Overall average for last 12 months
- `GET /average_percentage_full/5_years` - Overall average for last 5 years
- `GET /average_percentage_full/20_years` - Overall average for last 20 years
- `GET /average_percentage_full/<dam_id>/12_months` - Dam-specific 12-month average
- `GET /average_percentage_full/<dam_id>/5_years` - Dam-specific 5-year average
- `GET /average_percentage_full/<dam_id>/20_years` - Dam-specific 20-year average

### Example Response

```json
{
  "dam_id": "212232",
  "dam_name": "Warragamba Dam",
  "date": "2024-01-01",
  "storage_volume": 2027.450,
  "percentage_full": 95.40,
  "storage_inflow": 12.500,
  "storage_release": 8.300,
  "latitude": -33.8939,
  "longitude": 150.5969
}
```

## Database

<!-- ![Database ERD](./database-erd.png) -->

```sql

CREATE TABLE dams (
    dam_id VARCHAR(20) PRIMARY KEY,
    dam_name VARCHAR(255) NOT NULL,
    full_volume INT,
    latitude DECIMAL(10, 6),
    longitude DECIMAL(10, 6)
);

CREATE TABLE latest_data (
    dam_id VARCHAR(20) PRIMARY KEY,
    dam_name VARCHAR(255) NOT NULL,
    date DATE NOT NULL,
    storage_volume DECIMAL(10, 3),
    percentage_full DECIMAL(6, 2),
    storage_inflow DECIMAL(10, 3),
    storage_release DECIMAL(10, 3),
    FOREIGN KEY (dam_id) REFERENCES dams(dam_id)
);

CREATE TABLE dam_resources (
    resource_id INT AUTO_INCREMENT PRIMARY KEY,
    dam_id VARCHAR(20) NOT NULL,
    date DATE NOT NULL,
    storage_volume DECIMAL(10, 3),
    percentage_full DECIMAL(6, 2),
    storage_inflow DECIMAL(10, 3),
    storage_release DECIMAL(10, 3),
    FOREIGN KEY (dam_id) REFERENCES dams(dam_id)
);

CREATE TABLE specific_dam_analysis (
    dam_id VARCHAR(20),
    analysis_date DATE,
    avg_storage_volume_12_months DECIMAL(10, 3),
    avg_storage_volume_5_years DECIMAL(10, 3),
    avg_storage_volume_20_years DECIMAL(10, 3),
    avg_percentage_full_12_months DECIMAL(6, 2),
    avg_percentage_full_5_years DECIMAL(6, 2),
    avg_percentage_full_20_years DECIMAL(6, 2),
    avg_storage_inflow_12_months DECIMAL(10, 3),
    avg_storage_inflow_5_years DECIMAL(10, 3),
    avg_storage_inflow_20_years DECIMAL(10, 3),
    avg_storage_release_12_months DECIMAL(10, 3),
    avg_storage_release_5_years DECIMAL(10, 3),
    avg_storage_release_20_years DECIMAL(10, 3),
    PRIMARY KEY (dam_id, analysis_date),
    FOREIGN KEY (dam_id) REFERENCES dams(dam_id)
);

CREATE TABLE overall_dam_analysis (
    analysis_date DATE PRIMARY KEY,
    avg_storage_volume_12_months DECIMAL(10, 3),
    avg_storage_volume_5_years DECIMAL(10, 3),
    avg_storage_volume_20_years DECIMAL(10, 3),
    avg_percentage_full_12_months DECIMAL(6, 2),
    avg_percentage_full_5_years DECIMAL(6, 2),
    avg_percentage_full_20_years DECIMAL(6, 2),
    avg_storage_inflow_12_months DECIMAL(10, 3),
    avg_storage_inflow_5_years DECIMAL(10, 3),
    avg_storage_inflow_20_years DECIMAL(10, 3),
    avg_storage_release_12_months DECIMAL(10, 3),
    avg_storage_release_5_years DECIMAL(10, 3),
    avg_storage_release_20_years DECIMAL(10, 3)
);

CREATE TABLE dam_groups (
    group_name VARCHAR(255) PRIMARY KEY
);

CREATE TABLE dam_group_members (
    group_name VARCHAR(255) NOT NULL,
    dam_id VARCHAR(20) NOT NULL,
    PRIMARY KEY (group_name, dam_id),
    FOREIGN KEY (group_name) REFERENCES dam_groups(group_name),
    FOREIGN KEY (dam_id) REFERENCES dams(dam_id)
);

```

## Data Pipeline

### Data Collection Process

The project implements a three-stage data pipeline:

#### 1. Local Development Pipeline

```bash
# Stage 1: OAuth2 Authentication
python3 requests/oauth2_request.py

# Stage 2: Data Collection
python3 requests/list_of_dams.py       # Fetch dam metadata
python3 requests/latest_data.py         # Fetch current readings
python3 requests/collect_all_data.py    # Fetch historical data

# Stage 3: Database Seeding
python3 database-seeding/insert_dams.py
python3 database-seeding/insert_latest_data.py
python3 database-seeding/insert_all_data.py
```

#### 2. AWS Cloud Pipeline

![AWS Data Pipeline](images/aws-pipeline.png)

The production environment uses AWS services for automated monthly updates:

1. **AWS Lambda Function 1**: Scheduled trigger on the 1st of each month
   - Authenticates with WaterNSW API using OAuth2
   - Stores access token in AWS S3 bucket
   - Token lifetime: 12 hours

2. **AWS Lambda Function 2**: Triggered after token retrieval
   - Retrieves access token from S3
   - Fetches latest dam data from WaterNSW API
   - Stores raw JSON data in S3

3. **AWS Glue/Lambda Function 3**: ETL process
   - Reads JSON from S3
   - Transforms and cleans data
   - Writes to AWS RDS MySQL database

4. **AWS RDS**: Production MySQL database
   - Stores all dam data
   - Connected to Flask backend

#### 3. PySpark Analytics

Real-time data analysis is performed using PySpark:

- Calculate averages over different time periods (12 months, 5 years, 20 years)
- Metrics analyzed: storage volume, percentage full, storage inflow, storage release
- On-demand computation via API requests

### Data Update Frequency

- **WaterNSW API**: Updates on the 1st of each month
- **AWS Pipeline**: Triggered automatically on the 1st of each month
- **PySpark Analytics**: Computed on-demand via API requests

## Deployment

### Frontend Deployment (Netlify)

The frontend is deployed on Netlify with automatic deployments from the main branch.

```bash
# Build the frontend
cd react-frontend-retired
npm run build
```

### Backend Deployment (Docker + AWS ECS)

#### Build Docker Image

```bash
cd react-frontend-retired
docker build -t water-dashboard-frontend .
```

#### AWS ECS Deployment

The application uses:
- Amazon ECR for Docker image storage
- ECS Task Definition for container configuration
- AWS Fargate for serverless container management
- Automatic scaling based on demand

### Development Scripts

#### Frontend Scripts

```bash
npm run dev      # Start development server
npm run build    # Build for production
npm run preview  # Preview production build
npm run lint     # Run ESLint
```

#### Backend Scripts

```bash
python3 run.py   # Start Flask development server
```

#### Docker Commands

```bash
docker-compose up --build    # Build and start all services
docker-compose down          # Stop all services
docker-compose logs -f       # View logs
```

## Known Issues





<!-- ## Table of Contents

- [Frontend](#frontend)
- [Backend](#backend)
- [Data Approach](#data)
- [General](#general)


## Goals & MVP

- This project aims to support water management efforts and enhance public awareness about water resource trends and statuses.

- The MVP was to collect live and historic data about dams in NSW, using the WaterNSW API and display this in a responsive data dashboard to the user. 

- One major focus was to integrate cloud and data tools to create a live data pipeline directly from the public API into an AWS RDS, which could then be cleaned, processed and analyzed with PySpark.

## Build Strategy

- **First Stage** - Python scripting to collect all available data from the WaterNSW API, process it with Pandas, and then seed it into a local MySQL database.

- **Second Stage** - Building a Flask API on top of the local database, then connecting a React UI to display the data, including graphically with the Chart.js package

- **Third Stage** - Creating a live data pipeline with AWS Services and connecting this live-update database with the Flask backend, to create a real-time data experience

<a id="frontend"></a>
# Frontend - React Typescript

## Tech Stack

- React 
- Chart.js
- Typescript

## Design Goals
- This frontend was designed primarily as an SPA, with additional search functionality to fetch pages about specific resources. 
- Designed with the objective of creating an aesthetically appealing and interactive interface to display useful data for an engaging UX experience. 

## How To Use
- Use the search functionality with the search bar or open a list to find specific insights on a dam. 
- Clicking the 'dam-group' button will allow for automatic population of a new grouping and re-render the associated graph. 
- A variety of graphs and statistics display useful information to the user.

## Project Features
- [x] Chart.js integrated to provide graphical insights
- [x] Search feature allowing users to find specific dams
- [x] Individual pages about each dam that provide specific insights and analysis
- [x] Google Maps API integration for dynamically displaying location 

<a id="backend"></a>
# Backend - Flask API

## Tech Stack

- Flask
- Python


## Design Goals

## How To Use

## Project Features

<a id="data"></a>
# Data - Collection, Storage & Analysis

## Project Diagram
![Project Diagram](images/project-diagram.png)

## Tech Stack

- Pandas
- PySpark
- WaterNSW API 
- AWS RDS
- AWS S3 bucket
- AWS Lambda

## Data Components

There are three major data components in this project:

### Collection 

- A series of Python scripts were written to collect all data from the WaterNSW API and automate the database seeding process. These files can be found in the database-prep folder.

### PySpark Analysis

- PySpark was attached to the local database during development to perform a series of real-time calculations on the dataset, accessible through endpoints in the Flask API. 

- The analysis focuses specifically about how the average water level of any specific dam or the aggregation of dams within the dataset have changed over set time periods (12 months, 5 years, and 20 years).


### Live Data Pipeline 

- The WaterNSW API provides new data about each dam in the dataset on the first day of each month.

- A live data pipeline was created by first creating an AWS Lambda function call to collect an OAuth2 key, with a 12-hour duration, from the WaterNSW API on the first of each month and store this in an AWS S3 Bucket. 

- A second Lambda function call then uses this key to make an API call that accesses the endpoint that provides the latest data for each dam. This recent data is then stored in the AWS S3 Bucket. 

- This recent data is then written into the historical and latest data tables in the associated AWS RDS to provide an access point to the Flask API.

## AWS Pipeline Diagram
![AWS Data Pipeline](images/aws-pipeline.png)

## Project Features
- [x] AWS Lambda, AWS S3 Bucket and AWS RDS to create a live data pipeline 
- [x] Pandas for data handling and transfer
- [x] Live data cleaning, processing and analysis with PySpark
- [x] Scripting for API data collection and database seeding 

## Deployment - Docker, AWS ECS, Fargate

- Deployed by using Docker by tagging images in the AWS ECR, and then creating a service in AWS ECS 
- This project uses AWS Fargate to spin up a serverless compute engine when the deployment URL is accessed.

<a id="general"></a>
# General

## Additions & Improvements
- [ ] Investigate cached storage for calculations each month
- [ ] Fix bug with dynamically updating months on graphs
- [ ] Fix bug with button click in 'Dam Capacity Percentage Over Last 12 Months' graph
- [ ] Create testing for frontend and backend 
- [ ] Providing more complex analysis with PySpark (time-series, seasonal trends, etc.)
- [ ] Addition of distributed computing for data processing with Spark


## Learning Highlights
- Building a cloud-based live update data pipeline
- Integrating new data tools such as Pandas and PySpark
- Gaining hands-on experience with various AWS services 
- Creating a React based data dashboard to display insights to users
- Deploying with Docker and serverless computing resources

## Challenges
Many aspects of this application were challenging and provided experience in new domains, including creating a live-data pipeline, deployment with Docker, and learning new data tools. -->

## Contact Me
- Visit my [LinkedIn](https://www.linkedin.com/in/obj809/) for more details.
- Check out my [GitHub](https://github.com/cyberforge1) for more projects.
- Or send me an email at obj809@gmail.com
<br />
Thanks for your interest in this project. Feel free to reach out with any thoughts or questions.
<br />
<br />
Oliver Jenkins © 2024






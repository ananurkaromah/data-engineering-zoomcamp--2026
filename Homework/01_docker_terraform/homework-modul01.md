# Module 1 Homework: Docker, SQL & Terraform

This document contains the complete solutions for **Module 1 Homework**  
(Data Engineering Zoomcamp 2026 – DataTalksClub).

All commands, SQL queries, and answers are included directly in this Markdown file as required.

---

##  Ana Nurkaromah

- Homework: Module 1 – Docker & SQL
- Topic: Docker, SQL, Terraform
- Dataset: NYC TLC Green Taxi Trips (November 2025)

---

## 🐳 Question 1: Understanding Docker Images

### Task
Run Docker with the `python:3.13` image using bash as the entrypoint and identify the installed pip version.

### Command
the command to run docker with python 3.13 can be seen below:
```bash
docker run -it --entrypoint bash python:3.13
```
then, in order to identify the installed pip version use command below:
```bash
pip --version
```
### Answer
**pip version: 25.3**

---

## 🐳 Question 2: Docker networking & docker-compose
### Task
Given the following docker-compose.yaml, determine the hostname and port that pgAdmin should use to connect to PostgreSQL.

### Command
the command to run can be seen below:
```
yaml

services:
  db:
    container_name: postgres
    image: postgres:17-alpine
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: postgres
      POSTGRES_DB: ny_taxi
    ports:
      - "5433:5432"

  pgadmin:
    container_name: pgadmin
    image: dpage/pgadmin4:latest
    environment:
      PGADMIN_DEFAULT_EMAIL: pgadmin@pgadmin.com
      PGADMIN_DEFAULT_PASSWORD: pgadmin
    ports:
      - "8080:80"
```

#### Explanation

- Docker Compose creates a shared internal network
- Service names act as hostnames
- Containers communicate using internal ports, not host ports

### Answer
**db:5432**

#### Data Preparation
Download Green Taxi Trip Data (November 2025)
```bash
wget https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2025-11.parquet
```
Download Taxi Zone Lookup Table
```bash
wget https://github.com/DataTalksClub/nyc-tlc-data/releases/download/misc/taxi_zone_lookup.csv
```
note: Note: Raw data files are not committed to the repository.

## 🐳 Question 3: Counting short trips
### Task
Count trips in November 2025 where trip_distance <= 1.

### Command
the command SQL Query to run can be seen below:

```
sql

SELECT COUNT(*)
FROM green_tripdata
WHERE lpep_pickup_datetime >= '2025-11-01'
  AND lpep_pickup_datetime < '2025-12-01'
  AND trip_distance <= 1;
```

### Answer
**8,007 trips**

## 🐳 Question 4: Longest Trip for Each Day
### Task
Identify the pickup day with the longest trip distance, considering only trips with trip_distance < 100.

### Command
the command SQL Query to run can be seen below:

```
sql

SELECT DATE(lpep_pickup_datetime) AS pickup_date,
       MAX(trip_distance) AS max_distance
FROM green_tripdata
WHERE trip_distance < 100
GROUP BY pickup_date
ORDER BY max_distance DESC
LIMIT 1;
```

### Answer
**2025-11-23**

## 🐳 Question 5: Biggest Pickup Zone
### Task
Find the pickup zone with the highest total revenue (total_amount) on November 18, 2025.

### Command
the command SQL Query to run can be seen below:

```
sql

SELECT z.zone,
       SUM(g.total_amount) AS total_revenue
FROM green_tripdata g
JOIN taxi_zones z
  ON g.PULocationID = z.LocationID
WHERE DATE(g.lpep_pickup_datetime) = '2025-11-18'
GROUP BY z.zone
ORDER BY total_revenue DESC
LIMIT 1;
```

### Answer
**East Harlem South**

## 🐳 Question 6: Largest Tip
### Task
For passengers picked up in East Harlem North in November 2025,  determine the drop-off zone with the largest total tip amount.

### Command
the command SQL Query to run can be seen below:

```
sql

SELECT dz.zone AS dropoff_zone,
       SUM(g.tip_amount) AS total_tip
FROM green_tripdata g
JOIN taxi_zones pz
  ON g.PULocationID = pz.LocationID
JOIN taxi_zones dz
  ON g.DOLocationID = dz.LocationID
WHERE pz.zone = 'East Harlem North'
  AND g.lpep_pickup_datetime >= '2025-11-01'
  AND g.lpep_pickup_datetime < '2025-12-01'
GROUP BY dz.zone
ORDER BY total_tip DESC
LIMIT 1;
```

### Answer
**LaGuardia Airport**

## 🐳 Question 7: Terraform Workflow
### Task
Select the correct Terraform workflow for:
1. Initializing providers and backend
2. Creating resources automatically
3. Removing all managed resources

### Command
```
1. terraform init
2. terraform apply -auto-approve
3. terraform destroy
```

### Answer
**terraform init, terraform apply -auto-approve, terraform destroy**


### ✅ Final Notes

- All SQL and shell commands are included directly in this Markdown file
- Queries were executed using PostgreSQL
- Docker and Terraform workflows follow best practices
- Repository structure follows DataTalksClub guidelines
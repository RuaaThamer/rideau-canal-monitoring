# Rideau Canal Real‑Time Monitoring System

## Project Title and Description

**Rideau Canal Real‑Time Monitoring System**

This project implements a cloud‑based, real‑time monitoring system for the Rideau Canal Skateway in Ottawa.  
The system simulates IoT sensors deployed at multiple canal locations, processes streaming environmental data using Azure Stream Analytics, stores both aggregated and historical data, and visualizes live safety conditions through a web dashboard deployed to Azure App Service.

The solution demonstrates an end‑to‑end Internet of Things (IoT) and real‑time analytics architecture using Microsoft Azure.

---

## Student Information

- **Name:** Ruaa Thamer  
- **Student ID:** *(Add your student ID here)*  

### Repository Links
- **Sensor Simulation Repository:**  
  https://github.com/RuaaThamer/rideau-canal-sensor-simulation
- **Main Documentation Repository:**  
  https://github.com/RuaaThamer/rideau-canal-monitoring
- **Web Dashboard Repository:**  
  https://github.com/RuaaThamer/rideau-canal-dashboard

---

## Scenario Overview

### Problem Statement
Monitoring ice safety conditions across large outdoor skating surfaces such as the Rideau Canal requires continuous data collection and timely analysis. Manual inspections are inefficient, costly, and do not provide real‑time updates across multiple locations.

### System Objectives
- Simulate multiple IoT sensors measuring environmental conditions
- Ingest and process telemetry in real time
- Aggregate and analyze data using streaming analytics
- Store current and historical monitoring results
- Visualize live safety conditions through a web dashboard
- Deploy the complete system using cloud‑native Azure services

---

## System Architecture

### Architecture Diagram
The system architecture diagram is available in the `architecture/` folder of this repository.

### Data Flow Overview


## Azure Services Used

The following Microsoft Azure services were used to implement – Web dashboard hostingThe following Microsoft Azure services were used to implement the Rideau Canal Real‑Time Monitoring system:
- **GitHub Actions** – Continuous Integration and Deployment (CI/CD)

---

## Implementation Overview

### IoT Sensor Simulation

- Python‑based IoT sensor simulator
- Configurable sensor locations:
  - Dows Lake
  - Fifth Avenue
  - NAC
- Telemetry is generated and sent every **10 seconds**
- Repository:  
  https://github.com/RuaaThamer/rideau-canal-sensor-simulation

---

### Azure IoT Hub Configuration

- Three IoT devices registered (one per location)
- JSON‑formatted telemetry ingestion
- Secure device authentication
- Data ingestion verified using Azure IoT Hub metrics

---

### Azure Stream Analytics Job

- Reads real‑time telemetry from Azure IoT Hub
- Uses **5‑minute tumbling windows**
- Aggregates:
  - Ice thickness
  - Surface temperature
  - Snow accumulation
- Computes ice safety classification:
  - **Safe**
  - **Caution**
  - **Unsafe**
- Streams processed data to:
  - Azure Cosmos DB
  - Azure Blob Storage

**Stream Analytics Query:**  
Located in `stream-analytics/query.sql`

---

### Azure Cosmos DB Setup

- **Database:** `RideauCanalDB`
- **Container:** `SensorAggregations`
- **Partition Key:** `/location`
- Stores aggregated safety data for fast querying
- Serves as the data source for the dashboard backend API

---

### Azure Blob Storage Configuration

- **Container:** `historical-data`
- **Path pattern:**
 aggregations/{date}/{time}

- **Azure IoT Hub** – Device management and telemetry ingestion
- **Azure Stream Analytics** – Real‑time stream processing and aggregation
- **Azure Cosmos DB (NoSQL)** – Storage of aggregated, queryable safety data
- **Azure Blob Storage** – Historical data archival


- Stores historical JSON snapshots for long‑term analysis and auditing

---

### Web Dashboard

- Backend implemented using **Node.js and Express**
- REST API endpoints:
- `GET /api/latest`
- `GET /api/history/:location`
- Frontend dashboard displays:
- Current safety status
- Latest environmental measurements per location

**Repository:**  
https://github.com/RuaaThamer/rideau-canal-dashboard

---

### Azure App Service Deployment

- Deployed on **Azure App Service (Linux, Node.js)**
- Continuous deployment using **GitHub Actions**
- Secure environment variable configuration
- Live dashboard URL:  
https://rideau-canal-dashboard-app.azurewebsites.net

---

## Repository Links

- **IoT Sensor Simulation:**  
https://github.com/RuaaThamer/rideau-canal-sensor-simulation

- **Web Dashboard Application:**  
https://github.com/RuaaThamer/rideau-canal-dashboard

- **Live Dashboard Deployment:**  
https://rideau-canal-dashboard-app.azurewebsites.net

---

## Video Demonstration

A demonstration video link can be added here if required by the course.

*(Placeholder for YouTube or video hosting link)*

---

## Setup Instructions

### Prerequisites

- Python 3.x
- Node.js 18+
- Azure subscription
- GitHub account

---

### High‑Level Setup Steps

1. Deploy Azure IoT Hub and register IoT devices
2. Run the IoT sensor simulator locally
3. Create an Azure Stream Analytics job and configure inputs and outputs
4. Create Azure Cosmos DB and Blob Storage resources
5. Deploy the web dashboard using Azure App Service and GitHub Actions

Detailed setup instructions are provided in each component repository.

---

## Results and Analysis

### Sample Outputs

- Real‑time safety status displayed for each canal location
- Aggregated data stored in Azure Cosmos DB
- Historical data archived in Azure Blob Storage

Screenshots demonstrating system results are available in the `screenshots/` folder.

---

### System Performance Observations

- Stream Analytics processes data reliably in real time
- Dashboard updates reflect the latest aggregated conditions
- Cloud‑native deployment scales without performance issues

---

## Challenges and Solutions

### Technical Challenges

- Stream Analytics windowing and aggregation logic
- Partition‑aware queries in Cosmos DB
- Azure App Service deployment configuration
- Environment variable and CI/CD management

---

### Solutions

- Correct configuration of tumbling windows and aggregation rules
- Use of partition‑key‑aware Cosmos DB queries
- Proper use of `process.env.PORT` for Azure compatibility
- Troubleshooting deployments using GitHub Actions and Azure Log Stream

---

## AI Tools Disclosure

I used Gemini Pro for code generation and Microsoft Copilot for project documentation and checklist management. I also leveraged AI for troubleshooting. All system design, configuration, and deployment activities were implemented and verified by me personally.

---

## References

- Microsoft Azure Documentation
- Azure IoT Hub Documentation
- Azure Stream Analytics Documentation
- Azure Cosmos DB Node.js SDK
- Express.js Documentation

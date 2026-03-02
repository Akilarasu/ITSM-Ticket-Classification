# ITSM-Ticket-Classification

## Business Objective

This project applies machine learning techniques to historical IT Service Management (ITSM) data to improve operational efficiency, risk identification, and workload planning.  

Using structured incident and change management data, multiple predictive models were developed to:

- High-priority incident prediction
- Incident volume forecasting
- Auto-tagging and smart routing
- Change failure prediction

## Dataset Description

The dataset contains ITSM ticket-level information including:

- Incident ID
- Impact
- Urgency
- Priority
- Assignment group
- Category
- Reassignment count
- Open & close timestamps
- Change request details

## Exploratory Data Analysis

Key findings:

- Priority distribution imbalance
- Logical inconsistencies between Impact and Urgency
- Reassignment increases resolution time
- Certain configuration items have higher failure rates

## Models Built

### High Priority Prediction
Type: Multi-class classification  
Goal: Identify critical incidents early  

### Incident Volume Forecasting
Type: Time series forecasting  
Goal: Predict workload for resource planning  

### Auto-Tagging & Smart Routing
Type: Multi-class classification using structured ticket attributes 
Goal: Predict assignment group / category to reduce manual triaging  

### Change Failure Prediction
Type: Binary classification  
Goal: Reduce production outages  

## Tech Stack

### Programming
- Python

### Data Processing & Analysis
- Pandas
- NumPy

### Machine Learning
- Scikit-learn
- XGBoost
- LightGBM

### Time Series Forecasting
- SARIMA (Statsmodels)
- Prophet

### Data Visualization
- Matplotlib
- Seaborn

### Database
- SQL

## Business Impact

- Early identification of high-priority incidents improves SLA adherence.
- Forecasting improves workforce planning and capacity management.
- Automated routing reduces manual triaging overhead.
- Change risk prediction reduces production outages.

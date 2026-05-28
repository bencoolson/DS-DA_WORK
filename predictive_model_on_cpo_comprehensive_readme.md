# Predictive Model on Cost Per Order (CPO)

## Project Overview
This project focuses on building an intelligent predictive analytics system for delivery operations using machine learning. The notebook develops predictive models capable of estimating:

• Cost Per Order (CPO)
• Courier Waiting Time
• Operational Inefficiencies
• Delivery Optimization Opportunities
• Scenario-Based Business Simulations

The project applies data science, feature engineering, predictive modelling, operational analytics, and business intelligence techniques to uncover hidden inefficiencies in delivery logistics.

The workflow combines:

• Data preprocessing
• Feature engineering
• Machine learning pipelines
• Model evaluation
• Feature importance analysis
• Residual analysis
• Optimization recommendations
• Scenario simulations
• Data visualization

The final output is a business-focused analytics system capable of supporting operational decision-making in logistics and delivery environments.

---

# Project Objectives

The major objectives of this project are:

1. Predict delivery Cost Per Order (CPO)
2. Predict courier waiting time
3. Detect inefficient delivery stores
4. Understand operational cost drivers
5. Generate optimization recommendations
6. Simulate operational scenarios
7. Provide management-level business insights
8. Support data-driven decision making

---

# Business Problem Statement

Delivery companies often struggle with:

• Rising operational costs
• High courier waiting times
• Underpriced delivery fees
• Store inefficiencies
• Poor routing decisions
• Uneven city performance

Without predictive analytics, it becomes difficult to identify:

• Why some stores perform poorly
• Which factors increase operational costs
• How operational changes affect business performance
• Which cities require optimization

This project solves these problems using machine learning and predictive analytics.

---

# Technologies Used

## Programming Language

• Python

## Data Science Libraries

• Pandas
• NumPy
• Matplotlib
• Seaborn

## Machine Learning Libraries

• Scikit-learn

## Machine Learning Components

• RandomForestRegressor
• Pipeline
• ColumnTransformer
• StandardScaler
• OneHotEncoder
• train_test_split

---

# Dataset Description

The dataset contains operational delivery information such as:

| Feature | Description |
|---|---|
| city | Delivery city |
| store_code | Store identifier |
| order_id | Order identifier |
| basket_size | Customer basket value |
| delivery_fee | Fee charged for delivery |
| cost_per_order_cpo | Actual operational delivery cost |
| courier_waiting_time_mins | Courier waiting duration |
| distance_in_km_pick_up_to_delivery | Delivery distance |
| date | Transaction date |

The dataset is used to train predictive models and analyze delivery operations.

---

# Complete Workflow Architecture

## Step 1: Importing Libraries

The notebook begins by importing all required Python libraries.

### Purpose

This stage prepares the environment for:

• Data manipulation
• Data visualization
• Machine learning
• Model evaluation

### Major Libraries Imported

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

Machine learning libraries from Scikit-learn are also imported.

---

# Step 2: Loading the Dataset

The dataset is loaded into a Pandas DataFrame.

```python
df_raw = pd.read_csv("Internship casestudy week 2.csv", skiprows=1)
```

### Purpose

This stage:

• Reads the CSV file
• Handles formatting issues
• Creates the initial working dataset

### Key Operation

The dataset contains a blank first row, therefore:

```python
skiprows=1
```

is used to correctly structure the data.

---

# Step 3: Data Cleaning

Raw data usually contains inconsistencies and formatting problems.

This stage cleans the dataset.

## Column Cleaning

Column names are standardized by:

• Removing spaces
• Converting text to lowercase
• Removing brackets
• Creating machine-learning-friendly column names

Example:

```python
.str.replace(" ", "_", regex=False)
```

## Duplicate Removal

Duplicate columns are removed to avoid modelling conflicts.

## Currency Conversion

Currency symbols such as:

```python
€
```

are removed and converted into numeric values.

## Datatype Conversion

Features are converted into proper data types:

• Numeric fields → float/int
• Date fields → datetime

---

# Step 4: Feature Engineering

Feature engineering creates new variables that improve predictive performance.

This is one of the most important stages of the workflow.

## Features Created

### 1. Fee Minus CPO

```python
fee_minus_cpo = delivery_fee - cost_per_order_cpo
```

### Purpose

Identifies whether delivery fees cover operational costs.

Positive values:

• Profitable delivery

Negative values:

• Underpriced delivery

---

### 2. Order Volume Per Store

```python
order_volume_store
```

### Purpose

Measures operational workload per store.

Stores with higher order volume may experience:

• Delays
• Congestion
• Longer waiting time

---

### 3. Day of Week

```python
day_of_week
```

### Purpose

Captures weekly delivery patterns.

Example:

• Weekends may have higher demand
• Certain days may experience delays

---

### 4. Distance Band

Delivery distances are grouped into categories.

### Purpose

Improves operational segmentation and analysis.

---

# Step 5: Cost Prediction Engine

The first machine learning system predicts:

## Cost Per Order (CPO)

### Features Used

```python
cost_features = [
    "city",
    "store_code",
    "basket_size",
    "delivery_fee",
    "distance_in_km_pick_up_to_delivery",
    "day_of_week",
    "order_volume_store"
]
```

### Target Variable

```python
cost_target = "cost_per_order_cpo"
```

---

# Step 6: Data Preprocessing Pipeline

Machine learning models require properly formatted data.

A preprocessing pipeline is created using:

```python
ColumnTransformer
```

## Numeric Features

Numeric features are standardized using:

```python
StandardScaler()
```

### Purpose

Ensures numerical stability during modelling.

---

## Categorical Features

Categorical features are encoded using:

```python
OneHotEncoder(handle_unknown="ignore")
```

### Purpose

Converts text variables into machine-readable format.

---

# Step 7: Random Forest Regression Model

The project uses:

## RandomForestRegressor

```python
RandomForestRegressor(
    n_estimators=300,
    random_state=42,
    min_samples_leaf=3
)
```

---

# Why Random Forest?

Random Forest was selected because:

• It handles nonlinear relationships
• It performs well with mixed feature types
• It reduces overfitting
• It provides feature importance scores
• It works effectively on operational datasets

---

# Step 8: Train-Test Split

The dataset is divided into:

• Training data
• Testing data

```python
train_test_split(test_size=0.2)
```

### Purpose

Allows proper model evaluation on unseen data.

---

# Step 9: Model Training

The pipeline is trained using:

```python
cost_pipeline.fit(Xc_train, yc_train)
```

### Workflow During Training

1. Preprocessing executes automatically
2. Features are transformed
3. Random Forest learns relationships
4. Decision trees are built internally
5. Predictions become possible

---

# Step 10: Model Evaluation

Predictions are generated:

```python
cost_pred = cost_pipeline.predict(Xc_test)
```

## Evaluation Metrics

### Mean Absolute Error (MAE)

Measures average prediction error.

Lower MAE indicates:

• Better prediction accuracy

---

### R² Score

Measures how well the model explains variance.

Higher R² indicates:

• Stronger predictive performance

---

# Step 11: Waiting Time Prediction Model

A second machine learning system predicts:

## Courier Waiting Time

The workflow is similar to the CPO model:

1. Feature selection
2. Train-test split
3. Pipeline creation
4. Random Forest training
5. Evaluation

---

# Step 12: Feature Importance Analysis

The project extracts feature importance scores from the Random Forest models.

```python
feature_importances_
```

---

# Purpose of Feature Importance

This analysis identifies:

• Which variables increase delivery cost
• Which variables influence waiting time
• Operational drivers of inefficiency

---

# Business Value

Management can use this information to:

• Improve routing
• Reduce operational cost
• Optimize delivery pricing
• Improve store operations

---

# Step 13: Inefficiency Analysis Using Residuals

Residuals are calculated using:

```python
Residual = Actual Cost - Predicted Cost
```

---

# Interpretation

## Positive Residual

Actual cost is higher than expected.

Possible causes:

• Poor operations
• Routing inefficiencies
• Delays
• Congestion

---

## Negative Residual

Operations are more efficient than expected.

---

# Store-Level Analysis

Stores are grouped and summarized to identify:

• High-cost stores
• Inefficient stores
• Underperforming locations

---

# Step 14: Optimization Recommendations

The notebook automatically generates business recommendations.

## Examples

• Review routing strategy
• Improve courier allocation
• Increase delivery fees where necessary
• Reduce congestion
• Optimize store workload

---

# Step 15: Scenario Impact Analysis

The system performs simulation analysis.

## Scenarios Simulated

### Scenario 1

Reduce delivery distance by 10%

### Scenario 2

Reduce delivery distance by 20%

### Scenario 3

Increase delivery fee by 10%

### Scenario 4

Reduce store volume pressure by 15%

---

# Purpose of Scenario Analysis

This stage helps management understand:

• What operational changes improve profitability
• What reduces waiting time
• Which interventions have the greatest impact

---

# Step 16: Data Visualization

The notebook creates several visual analytics dashboards.

## Visualizations Included

### Actual vs Predicted Cost

Measures model prediction quality.

### Actual vs Predicted Waiting Time

Shows prediction accuracy.

### Feature Importance Charts

Displays key operational drivers.

### City Cost Comparison

Compares delivery costs across cities.

### City Waiting Time Comparison

Shows city-level delays.

### Store Efficiency Scatterplots

Identifies inefficient stores.

### Scenario Impact Charts

Visualizes operational simulations.

---

# Final Management Summary

The notebook concludes with a business-oriented management interpretation.

The summary explains:

• Model performance
• Operational insights
• Cost drivers
• Waiting time patterns
• Optimization opportunities
• Strategic recommendations

---

# End-to-End Workflow Summary

Below is the complete project workflow:

```text
Raw Dataset
    ↓
Data Cleaning
    ↓
Feature Engineering
    ↓
Preprocessing Pipeline
    ↓
Train-Test Split
    ↓
Random Forest Training
    ↓
Prediction Generation
    ↓
Model Evaluation
    ↓
Feature Importance Analysis
    ↓
Residual Analysis
    ↓
Store Inefficiency Detection
    ↓
Optimization Recommendations
    ↓
Scenario Simulations
    ↓
Data Visualization
    ↓
Management Insights
```

---

# Machine Learning Workflow Explanation

## Input Layer

Operational delivery data enters the system.

---

## Processing Layer

Data cleaning and feature engineering occur.

---

## Machine Learning Layer

Random Forest models learn operational patterns.

---

## Prediction Layer

The models predict:

• Cost per order
• Waiting time

---

## Analytics Layer

The system performs:

• Feature importance analysis
• Residual analysis
• Scenario simulation

---

## Business Intelligence Layer

Insights are transformed into:

• Operational recommendations
• Optimization strategies
• Management reports

---

# Key Insights Generated by the Project

The project can reveal:

• Which cities have the highest operational costs
• Which stores are inefficient
• Whether delivery fees cover operational expenses
• How distance affects cost
• How store volume affects waiting time
• Which operational changes reduce cost

---

# Strengths of the Project

## Machine Learning Integration

Uses predictive analytics instead of traditional reporting.

## Business Intelligence Capability

Transforms raw data into operational decisions.

## Operational Optimization

Provides actionable recommendations.

## Scenario Simulation

Allows management to test operational strategies.

## Explainability

Feature importance improves transparency.

---

# Possible Future Improvements

The project can be extended using:

• XGBoost
• LightGBM
• Deep Learning
• Real-time prediction APIs
• Power BI dashboards
• Geospatial analytics
• Demand forecasting
• Route optimization algorithms
• Reinforcement learning

---

# Folder Structure Recommendation

```text
project/
│
├── data/
│   └── raw_dataset.csv
│
├── notebooks/
│   └── predictive_model_on_CPO.ipynb
│
├── outputs/
│   ├── charts/
│   ├── reports/
│   └── scenario_analysis/
│
├── models/
│   ├── cost_model.pkl
│   └── waiting_time_model.pkl
│
├── README.md
│
└── requirements.txt
```

---

# Installation Guide

## Clone the Repository

```bash
git clone <repository_url>
```

---

## Navigate into the Project Folder

```bash
cd project_folder
```

---

## Install Dependencies

```bash
pip install -r requirements.txt
```

---

# Running the Notebook

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```text
predictive_model_on_CPO.ipynb
```

Run all cells sequentially.

---

# Expected Outputs

The notebook generates:

• Predictive models
• Evaluation metrics
• Feature importance charts
• Operational recommendations
• Scenario simulations
• Business insights
• Visualization dashboards

---

# Conclusion

This project demonstrates how machine learning and business intelligence can transform delivery operations.

By combining predictive modelling, feature engineering, operational analytics, and scenario simulations, the system provides a complete analytics framework capable of:

• Predicting operational cost
• Identifying inefficiencies
• Improving delivery performance
• Supporting strategic business decisions

The project represents a strong real-world application of:

• Data Science
• Machine Learning
• Predictive Analytics
• Logistics Intelligence
• Operational Optimization
• Business Intelligence

---

# Author

Benjamin Ossai

Data Scientist | Machine Learning Enthusiast | Business Intelligence Researcher


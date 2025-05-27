# NYC Taxi Trip Analysis Project

## Overview
This project analyzes New York City taxi trip data to gain insights into trip patterns, revenue generation, and passenger tipping behavior. The analysis combines trip data (`taxitripdata.csv`) with geographic zone information (`taxizonegeo.csv`) to provide a comprehensive view of NYC taxi operations.

## Project Structure
```
nyc-taxi-analysis/
├── data/
│   ├── taxitripdata.csv          # Raw trip data
│   ├── taxizonegeo.csv           # Zone geographic data
├── notebooks/
│   └── preditctionSparkML.ipynb  # Jupyter notebook with analysis                 
├── README.md                     # This file
```

## Data Processing
### Data Cleaning & Engineering
1. **Initial Exploration**: Examined both datasets for structure, missing values, and data quality issues
2. **Handling Missing Values**:
   - Explicit NULLs and implicit missing values (zeroes, empty strings) addressed
   - Appropriate imputation or removal based on context
3. **Data Quality**:
   - Removed duplicate records
   - Dropped non-informative columns
4. **Feature Engineering**:
   - Calculated trip duration in minutes
   - Computed total trip cost (fare_amount + extra + mta_tax + tip_amount + tolls_amount)
   - Integrated zone-based location data from `taxizonegeo.csv`
   - Created time-of-day categories (morning, afternoon, evening)

## Analytical Queries
Implemented using Spark SQL/DataFrame API:
1. Most common payment type per time of day
2. Borough revenue generation and trip volume comparison
3. Average tip amount per passenger count
4. Best 5 pickup locations and optimal times
5. Top 5 longest trips with details
6. Most frequent inter-borough travel flows

## Machine Learning Task
### Trip Profiling: Predict Likelihood of High Tipping
**Target Variable**:
- `high_tip`: 1 if tip_amount > 0.15 × fare_amount, 0 otherwise

**Feature Engineering**:
- Created features: passenger_count, trip_distance, trip_duration_minutes, pickup_hour, fare_amount
- Additional engineered features: fare_per_mile, pickup/dropoff borough (encoded)
- Combined features using VectorAssembler

**Models Implemented**:
1. Logistic Regression
2. Decision Tree Classifier
3. Random Forest Classifier

**Evaluation**:
- Split data into training (70%) and testing (30%) sets
- Evaluated using accuracy and other relevant metrics
- Identified most important features for each model

## Technologies Used
- Apache Spark (PySpark) for data processing and analytics
- Spark MLlib for machine learning
- Cassandra/MongoDB (optional) for data storage
- Jupyter Notebooks for interactive analysis
- Python 3.x with data science stack (pandas, numpy, matplotlib, etc.)

## Getting Started
1. Clone this repository
2. Install dependencies: `pip install -r requirements.txt`
3. Place raw data files in the `data/` directory
4. Run processing scripts in order:
   - `data_cleaning.py`
   - `analytical_queries.py`
   - `ml_models.py`
5. Explore the Jupyter notebook for interactive analysis

## Results
Findings from the analysis are documented in the Jupyter notebook, including:
- Key insights from analytical queries
- Performance comparison of ML models
- Visualization of important patterns and relationships

## Future Work
- Real-time analysis of streaming taxi data
- Integration with additional data sources (weather, events)
- Deployment of ML model as a predictive service

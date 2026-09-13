# Bikes4Britain – UK Cycling Traffic Analysis & Forecasting

## 📌 Project Overview

Bikes4Britain is an organization aiming to improve cycling infrastructure across the United Kingdom.

The organization is interested in understanding how the number of cyclists has changed over time and how cycling traffic differs across different locations.

This project analyzes cycling traffic data to identify:

- Changes in cycling activity over time
- Locations with increasing cycling traffic
- Locations with high cycling volumes
- Locations where cycling represents a significant proportion of traffic
- Cycling commuter patterns
- Daily, weekly, and yearly temporal patterns
- Seasonal trends
- Locations suitable for detailed time-series analysis and forecasting

The project also uses time-series analysis and forecasting techniques to investigate future cycling trends.

---

# 🎯 Desired Outcomes

The expected output of this project is a combination of:

- Line charts
- Time-series visualizations
- Statistical analysis
- Forecasting results
- Written insights and conclusions

The analysis aims to provide useful information that could help Bikes4Britain better understand cycling activity and support decisions related to cycling infrastructure.

---

# 📊 Data Source

The data was originally obtained from the UK Department for Transport's Road Traffic website.

**Data Source:**  
https://roadtraffic.dft.gov.uk/downloads

The project also includes a data dictionary document describing the available variables.

**Data Dictionary:**  
https://mng.bz/4ajw

---

# 📖 Data Dictionary

The detailed data dictionary is included in the project files.

It describes the variables available in the cycling traffic dataset and provides information about the meaning and structure of each column.

---

# 🛠️ Required Tools

The project uses the following Python libraries:

- **Pandas** – Data exploration, cleaning, transformation, and aggregation
- **Matplotlib** – Data visualization
- **Statsmodels** – Time-series analysis and decomposition
- **pmdarima** – Automatic selection of forecasting models

---

# 🔎 Project Workflow

## 1. Investigate Data Granularity

The first step is to understand what one row of data represents.

Questions include:

- Does one row represent one location per hour?
- Is the data recorded daily or weekly?
- Are there multiple time series representing different locations?

Understanding the granularity is important because it determines how the data should be transformed and aggregated.

---

## 2. Understand Geographic and Time Coverage

The dataset contains multiple time series from different locations.

The analysis investigates:

- Which locations are represented?
- How many observations are available for each location?
- What is the earliest and latest available date?
- Do all locations have the same amount of historical data?
- Which locations have sufficiently long time coverage?

---

## 3. Identify Gaps in the Time Series

Time-series completeness is investigated for each location.

The analysis checks whether:

- Measurements occur at constant intervals.
- Locations have missing periods.
- There are gaps in the time series.
- The available observations are sufficient for time-series analysis and forecasting.

Locations with incomplete records may need to be excluded or their missing periods handled through appropriate methods such as smoothing or estimation.

---

## 4. Investigate Missing Data

Missing values are investigated across the dataset.

Where appropriate, missing values in selected columns are filled with **0**.

This step ensures that missing information is handled consistently before further analysis.

---

## 5. Combine Duplicate Rows

Duplicate observations are investigated and combined where necessary.

For duplicate rows, measurements are combined by calculating the **average value**.

This prevents duplicate observations from distorting later aggregations and analysis.

---

# 🚲 Investigating Cycling Traffic

## 6. Investigate the Distribution of Cycling Traffic

The distribution of bicycle counts is analyzed to understand typical cycling volumes.

For example:

> What is the typical number of bikes recorded in one hour?

This analysis helps identify:

- Typical hourly cycling volumes
- Locations with unusually high cycling traffic
- Potential anomalies and outliers

---

## 7. Identify Locations Where Cycling Is on the Rise

Locations are analyzed over time to identify areas experiencing increasing cycling traffic.

This can help highlight locations where cycling activity is growing and may indicate areas where additional cycling infrastructure could be valuable.

---

## 8. Identify Locations Where Cycling Is a Significant Percentage of Traffic

The analysis investigates locations where bicycles represent a significant proportion of total traffic.

This provides another way to identify locations where cycling plays an important role in transportation.

---

## 9. Identify Locations With High Cycling Commuter Traffic

Cycling traffic patterns are investigated to identify locations with high commuter activity.

Particular attention is given to recurring patterns during commuting hours, such as:

- Morning peaks
- Evening peaks
- Weekday traffic

---

# 🕐 Time-Series Transformation

The original data may contain measurements at a higher frequency, such as hourly observations.

To make the data easier to analyze, time series can be reshaped into different levels of granularity.

For example:

```text
Hourly Data
     ↓
Daily Aggregation
     ↓
Weekly / Monthly Analysis
```

---

📋 Project Progress

The project currently includes the following analysis steps:

```text

    Investigate missing data

    Fill missing values in selected columns with 0

    Investigate time-series granularity

    Determine whether multiple time series exist across locations

    Combine duplicate rows by averaging measurements

    Investigate date coverage

    Investigate gaps in the time series

    Filter to locations with long coverage and no gaps

    Investigate the distribution of cycling traffic

    Identify locations where cycling is on the rise

    Identify locations where cycling represents a significant percentage of traffic

    Identify locations with high cycling commuter traffic

    Reshape time-series data to different levels of granularity

    Filter data to locations of interest

    Visualize time series using line charts

    Investigate the distribution of repeated measurements

    Investigate individual data points for anomalies

    Decompose time series to identify trends and seasonality

    Identify temporal patterns

    Find time series of interest using multiple criteria

    Forecast selected time series into the future

---
🔄 project Workflow

```text 

Raw Cycling Traffic Data
        ↓
Data Quality Investigation
        ↓
Missing Value Handling
        ↓
Investigate Data Granularity
        ↓
Combine Duplicate Rows
        ↓
Investigate Geographic Coverage
        ↓
Investigate Time Coverage
        ↓
Identify Gaps
        ↓
Filter Suitable Locations
        ↓
Investigate Cycling Traffic Distribution
        ↓
Analyze Temporal Patterns
        ↓
Identify Trends & Seasonality
        ↓
Investigate Anomalies
        ↓
Select Locations of Interest
        ↓
Time-Series Forecasting
        ↓
Visualizations & Insights

```

---
# 🚀Installation & Usage

1. Clone the Repository

```bash
git clone <your-repository-url>
cd <your-project-folder>
```
2. Create a Virtual Environment
Windows

```bash
python -m venv venv
```
macOS / Linux

```bash
python3 -m venv venv
```


3. Activate the Virtual Environment
Windows

```bash
venv\Scripts\activate
```
macOS / Linux

```bash
source venv/bin/activate
```


4. Install Dependencies

```bash 
pip install -r requirements.txt
```

5. Run the Streamlit Application

```bash 
streamlit run app.py
```
The application will open in your browser.


6. Deactivate the Virtual Environment
When finished : 

```bash
deactivate
```


---

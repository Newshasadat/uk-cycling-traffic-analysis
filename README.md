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
# main variable :

| Count_point_id | A unique reference for the road link that links the AADFs to the road network |
| Direction_of_travel | Direction of travel | 
| Year | Counts are shown for each year from 2000 onwards |
| Count_date | The date when the actual count took place |
| Hour | The time when the counts in question took place, where 7 represents between 7 a.m. and 8 a.m., and 17 represents  between 5 p.m. and 6 p.m. |
| Region_id | Website region identifier |
| Region_name | The name of the region that the count point (CP) sits within |
| Region_ons_code | The Office for National Statistics code identifier for the region |
| Pedal_cycles | Counts for pedal cycles |
| All_motor_vehicles | Counts for all motor vehicles |


---

# 🛠️ Required Tools

The project uses the following Python libraries:

- **Pandas** – Data exploration, cleaning, transformation, and aggregation
- **Matplotlib** – Data visualization
- **Statsmodels** – Time-series analysis and decomposition
- **pmdarima** – Automatic selection of forecasting models

---

# 🔎 Project Workflow

- Investigating time series data for completeness (are time series measured at different locations, or do all locations have the same amount of data?)
- Establishing the granularity of the time series (is it hourly, daily, or weekly?
Are there, in fact, multiple time series in the data, at different locations?)
- Understanding the coverage of the data (what period does the data cover?)
- Investigating whether the time series has gaps
- Reshaping time series data to be at a different level of granularity (summa
rizing hourly data at a daily level)
- Visualizing time series with appropriate charts (most often, line charts)
- Calculating the distribution of the repeated measurement (for “Number of bikes seen in an hour,” what are the typical hourly counts?)
- Diving down to the individual data point level to investigate anomalies
- Decomposing a time series to identify whether it has a trend or seasonality
- Identifying temporal patterns within time series (cycling locations with a high level of traffic in the morning)
- Finding time series of interest based on multiple criteria
- Forecasting a time series into the future to predict future trends


---
# 📋 project progress

```text 

Raw Cycling Traffic Data
        ↓
Data Quality Investigation
        ↓
Missing Value Handling
        ↓
Investigate Data Granularity
        ↓
Combine duplicate rows
        ↓
Investigate Time Coverage
        ↓
Investigate Geographic Coverage
        ↓
Identify Gaps
        ↓
Filter Suitable Locations
        ↓
Investigate Cycling Traffic Distribution
        ↓
Identify Trends 
        ↓
Investigate certain characteristics 
        ↓
Analyze Temporal Patterns
        ↓
Select Locations of Interest
        ↓
Time-Series Forecasting
        ↓
Visualizations & Insights

```
---

# 📋 Project Progress

The project currently includes the following analysis steps:



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
# analyse steps

## 1. Investigate missing data : Fill missing values in some columns with 0

## 2.  Investigate granularity of the data :

It is important to establish what one row of our data represents and which combination of columns uniquely identifies it.

We identified the following composite key:

`\\\["Count\\\_point\\\_id", "Year", "Count\\\_date", "hour", "Direction\\\_of\\\_travel"]`

However, the dataset contains duplicate rows with the same key. We handle these by grouping duplicate records and averaging their measurement values.

The `Road\\\_name` and `Link\\\_length` columns contain missing values. To avoid issues during deduplication, we temporarily replace missing values with placeholders, perform the deduplication, and then restore them as missing values. We use `"PLACEHOLDER"` for `Road\\\_name` and a numeric value not already present in the data for `Link\\\_length`.

## 3. Investigate date coverage : Only keep locations with long coverage 
3.1 What is the date range of the data in general?
3.2 Does the date range vary across smaller time series (per location)?
3.3 Are there consistent measurement intervals in the data?
We first examine the overall date range and how coverage varies across locations 
Histogram showing coverage in years across different locations
Number of locations with one day of data across regions
Number of count points by region (total location)
calculate  percentage of the total number of locations in each region to get a fair comparison
As it stands, the percentage of locations that only have data on a single date is consistent across the regions . we will assume we are satisfied that the
existence of single-day locations is just something that happens everywhere and is not something to address directly.

## 4. INVESTIGATING GAPS IN TIME SERIES
Are there gaps in any of the time series of the different locations?
Different locations have data covering different periods. We identify gaps by comparing each year with the previous year and excluding location IDs with gaps. We focus on locations with at least 10 years of continuous data. This leaves just over 1,400 location IDs with one measurement date per location per year.
The day of the week can affect traffic patterns. Our remaining data contains measurements mainly from Tuesday to Friday, fewer on Monday, and none on weekends, reducing concerns about weekday-versus-weekend effects.
However, measurements are not always taken on the same date or at the same time of year. Seasonal differences may therefore introduce bias, particularly in cycling data. We identify locations where measurements consistently occurred in the same month. Applying this condition reduces the dataset by about half, leaving just under 700 time series.

## 5.  Export filtered data to parquet

## 6. Investigate distribution of cycling traffic 
Distribution of total cycling traffic
Descriptive statistics for the total cycling traffic values

6.1 FINDING TIME SERIES THAT CONTAIN UPWARD TRENDS :
Find locations where cycling is on the rise :
Our first step is to define what we mean by “on the rise.” Do we want to see cycling increase year-on-year consistently for a location to qualify? Since we only have a day’s worth of data each year, there will be noise, so this criterion might be too strict. Let’s look for locations where the latest measurement figure was higher than the first. It’s a crude proxy for “increase in cycling,” but we can filter the data down to the locations with the largest increase.
Defines a function to calculate the difference between the first and last values encountered in a group
Defines a function to calculate the change as a percentage (Accounts for division-by-zero errors ) 
Applies these two functions to every location ID group ( Absolute and percentage difference of cycling totals for each location ) 

6.2 IDENTIFYING TIME SERIES WITH CERTAIN CHARACTERISTICS : 
Find locations where cycling is a significant percentage of traffic
 Filter the traffic data to the last observed date for each location ID.
 Calculate the total traffic by adding the relevant columns together.
 Group the data by location ID to reduce the granularity to one row per location.
 Sum the total traffic column and the bikes column.
 Calculate cycling as a percentage for each location 
 A specific location with a high cycling traffic percentage


6.3 IDENTIFYING TEMPORAL PATTERNS WITHIN TIME SERIES : 
Find locations with high cycling commuter traffic : 
To investigate commuting patterns, we will do two things:
6.3.1  Look at the most popular times of day for cycling at each location. In other words, what hour(s) of the day do people cycle the most?
6.3.2 Once we understand this, we will identify locations where cycling traffic is highest during commuting hours.
1 Filter the cycling data to the most recent year for each location—This will give us an up to-date view on cycling patterns.
2 Calculate the percentage of bike traffic that occurred in each hour of the day—Using a percentage means comparable results regardless of the popularity of the location.
3 Visualize the distribution of these percentage values by hour—Using our “start at the end” approach, we imagine the final visualization. In this case, it will be a series of box plots, each representing an hour of the day and individual points representing the percentage of bike traffic in that hour of the day for a location.


## 7. COMBINING CRITERIA TO IDENTIFY TIME SERIES OF INTEREST : Filter data to locations of interest : 
Decide on cutoffs for all metrics 

## 8. FORECASTING TIME SERIES
plot for Actual vs. predicted values for a particular location’s time series


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

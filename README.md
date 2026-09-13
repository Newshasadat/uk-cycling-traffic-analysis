

# Bikes4Britain – Cycling Traffic Analysis

## Problem Statement

Bikes4Britain, which aims to improve cycling infrastructure in the United Kingdom, is interested in seeing how the number of cyclists has changed over time and across different areas.

---

## Data Source

Data originally taken from:

https://roadtraffic.dft.gov.uk/downloads

---

## Data Dictionary

The data dictionary document is included in the project files.

https://mng.bz/4ajw

---

## Desired Outcomes

The output of this project is likely to be a combination of line charts and conversations.

---

## Required Tools

- **Pandas** and **Matplotlib** libraries for data exploration and visualization.
- **Statsmodels** library when investigating time-specific aspects of the data.
- **pmdarima** module for automatically choosing the best forecasting model.

---

# Project Workflow

## 1. Investigate the Granularity of Our Data

What does one row represent?

Is it one row per location per day or something else?

The granularity of data is one of the first things to investigate because it informs all other data transformations, like aggregations.

---

## 2. Understand the Coverage of the Data

Understand the coverage of the data both geographically and in time.

For example, because the dataset is not a single time series but many, we need to know if every available location has the same amount of data.

---

## 3. Identify Gaps in the Time Series

Does every location have measurements at constant intervals?

This is important to ensure we have enough of a sample at each location and is also a critical requirement for forecasting.

Most forecasting algorithms do not work with gaps in the data or inconsistent intervals.

---

## 4. Investigate the Distribution of Bicycle Counts

What is a typical cycling volume for one row of data?

Knowing this will immediately help identify the places with the highest cycling traffic.

---

## 5. Look at Temporal Patterns

This includes looking at how cycling traffic fluctuates:

- At different times of day
- On different days of the week
- Across multiple years

Questions to investigate:

- Are there seasonal patterns we can identify?
- Which locations are showing a growing trend in cycling traffic?

---

## 6. Reduce the Search Space

We may not be able to analyze every location in equal detail because of gaps.

We may have to filter the data down to locations that have more complete records across a longer time horizon, especially if we are interested in looking for temporal patterns and forecasting.

---

# 🔎 Project Progress

## 1. Data Quality Investigation

The first step was to investigate the completeness and quality of the property sales data.

This included:

- Identifying missing values.
- Investigating missing street names.
- Investigating missing postcodes.
- Detecting potential outliers in property prices.

### Missing Values

- Missing street names were replaced with a placeholder.
- Records with missing postcodes were retained because they may still contain useful geographic information.

---

## 2. Geographic Investigation

The geographic structure of the dataset was investigated to understand the different address levels available.

The analysis considered:

- Postcode
- Street
- Locality
- Town/City
- District
- County

Understanding this hierarchy was important for determining how geographic filters could be implemented in the application.

---

## 3. Identifying Welsh Properties

Since the original dataset contains property transactions across England and Wales, additional government geographic data was used to distinguish Welsh property transactions from English transactions.

This allowed the project to extract the relevant property transactions located in Wales.

---

## 4. Property Type Analysis

Property type was one of the main stakeholder requirements.

The analysis investigated:

- How sale prices vary between property types.
- Which property types are more popular.
- Whether property type popularity varies geographically.
- Whether price differences between property types vary across different areas.

Property categories were also renamed to make them easier to understand within the application.

For example:

- D → Detached
- S → Semi-detached
- T → Terraced
- F → Flats/Maisonettes
- O → Other

---

## 5. Property Price Analysis

Property prices were investigated to understand their distribution and identify potential outliers.

The analysis included:

- Examining the distribution of sale prices.
- Identifying unusually high property prices.
- Removing extreme high values where appropriate.
- Retaining lower property prices to avoid unnecessarily removing valid transactions.

---

## 6. Choosing Visualizations

Several visualizations were investigated and selected based on their usefulness for the potential application.

The main visualizations include:

### Transactions Over Time

Shows how the number of property transactions changes over time.

### Price by Property Type

Compares property prices across different property types.

### Ridgeline Plot of Price by County

Shows the distribution of property prices across different Welsh counties.

---

# 🧹 Data Preparation

The project followed a data preparation process that included:

1. Merging multiple years of property sales data.
2. Investigating missing values.
3. Handling missing street names.
4. Retaining records with missing postcodes.
5. Investigating price distributions.
6. Identifying and removing extreme high-price outliers.
7. Renaming property categories.
8. Enhancing geographic information using external government data.
9. Extracting Welsh property transactions.
10. Exporting the cleaned Welsh data to Parquet format.

---

# 💾 Data Export

After cleaning and filtering the data, the relevant Welsh property transactions were exported to **Parquet format**.

The exported dataset is used by the Streamlit proof-of-concept application.

Using a processed Parquet dataset allows the application to work with the cleaned Welsh property data efficiently.

---

# 🌐 Streamlit Proof of Concept

The project includes a proof-of-concept application built using **Streamlit**.

The purpose of the application is to demonstrate how the analyzed property data could be presented to stakeholders and potential users.

## Application Requirements

The application should:

- Use real Welsh property data.
- Allow users to interact with the data.
- Dynamically update visualizations based on user input.
- Dynamically update metrics based on user selections.
- Use available geographic information.
- Generate filter options directly from the available data.

For example, county filters should be created from the actual counties available in the dataset rather than using manually defined values.

---

# 📱 Application Layout

The application is structured around:

1. County breakdown
2. User filters
3. Key metrics
4. Interactive visualizations

The goal is to provide users with an intuitive way to explore property prices and sales patterns across Wales.

---

# 📈 Visualizations Included

The proof-of-concept application focuses on the following visualizations:

### 1. Transactions Over Time

Allows users to understand historical changes in property transaction activity.

### 2. Price by Property Type

Allows users to compare property prices across:

- Detached
- Semi-detached
- Terraced
- Flats/Maisonettes
- Other

### 3. Ridgeline Plot of Price by County

Allows users to compare the distribution of property prices across Welsh counties.

---

# 🧩 Helper Functions

Helper functions were created to keep the application code organized and reusable.

These functions provide functionality that can be used by the application without being tightly coupled to the main Streamlit application code.

This improves:

- Code organization
- Reusability
- Maintainability
- Readability

---

# 🗺️ Geographic Hierarchy

The geographic information in the dataset provides several levels of location detail:

```text
County
   ↓
District
   ↓
Town/City
   ↓
Locality
   ↓
Street
   ↓
Postcode
   ↓
Property

```

---


# Project Workflow

```text

Raw Land Registry Data
        ↓
Merge Multiple Years
        ↓
Data Quality Investigation
        ↓
Missing Value Handling
        ↓
Outlier Investigation
        ↓
Geographic Investigation
        ↓
Identify Welsh Properties
        ↓
Property Type Analysis
        ↓
Price Analysis
        ↓
Select Useful Visualizations
        ↓
Export Clean Welsh Data
        ↓
Build Streamlit Proof of Concept
        ↓
Interactive Property Market Application

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
🎯 Final Outcome

The final outcome of this project is a Streamlit proof-of-concept application that demonstrates how Welsh property sales data can be transformed into an interactive property market exploration tool.

The project provides insights into:

Property prices
Property types
Transaction trends
Geographic differences
County-level price distributions
Potential street-level analysis

The proof of concept also helps evaluate whether the available Land Registry data is sufficient to support the development of a more complete property market product for CymruHomes Connect.

# Welsh Property Market Analysis & App Proof of Concept

## 📌 Project Overview

CymruHomes Connect is a property company specializing in homes in Wales. The company wants to expand its business through data-driven insights and provide customers with information about the Welsh property market through a new application.

The proposed application will use historical property sales data to allow users to explore property prices in areas of interest.

The main goal of this project is to investigate whether the available data is suitable for building a useful property market application, with a particular focus on:

- Property types
- Property prices
- Geographic patterns
- Street-level information
- Differences between areas across Wales

---

## 🎯 Desired Outcomes

The project aims to:

- Identify what types of analysis could be included in a potential property market application.
- Investigate whether the available data is sufficient to build a useful product.
- Provide recommendations for additional data sources that could improve the application.
- Build a proof of concept to demonstrate the potential application to stakeholders.
- Consider both stakeholder requirements and potential future user preferences.

---

## 📊 Data Source

The project uses the UK Government **Land Registry Price Paid Data**, which contains publicly available historical property sales information.

**Source:**  
https://mng.bz/yWvB

The dataset contains information about property transactions, prices, dates, locations, property types, and other address-related information.

---

## 📖 Data Dictionary

| Column | Description |
|---|---|
| Transaction Unique Identifier | Reference number generated automatically for each published sale. |
| Price | Sale price stated on the transfer deed. |
| Date of Transfer | Date the sale was completed, as stated on the transfer deed. |
| Postcode | Postal code of the property address. |
| Property Type | Type of property: D = Detached, S = Semi-detached, T = Terraced, F = Flats/Maisonettes, O = Other. |
| Old/New | Indicates whether the property is newly built (Y) or an established building (N). |
| Duration | Property tenure: F = Freehold, L = Leasehold. |
| PAON | Primary Addressable Object Name, usually the house number or name. |
| SAON | Secondary Addressable Object Name, used when a property is part of a larger building, such as a flat. |
| Street | Street name of the property. |
| Locality | Additional location information, such as a district within a city. |
| Town/City | Town or city where the property is located. |
| District | Administrative district of the property. |
| County | County where the property is located. |
| Category Type | A = Standard Price Paid entry, B = Additional Price Paid entry. |
| Record Status | Indicates additions, changes, or deletions in monthly files. Yearly files contain the latest version of all records. |

### Category Type

- **A:** Standard Price Paid entry, including a single residential property sold for full market value.
- **B:** Additional Price Paid entry, including repossessions, transfers under power of sale, identifiable buy-to-lets, and transfers to non-private individuals.

---

## 🛠️ Tools & Technologies

The project uses:

- **Python**
- **Pandas** – Data exploration and manipulation
- **Matplotlib** – Data visualization
- **Seaborn** – Statistical visualization
- **Ridgeplot** – Ridgeline visualizations
- **Parquet** – Efficient storage of processed property data

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

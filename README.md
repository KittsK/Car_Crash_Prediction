# Chicago Traffic Crash Analysis

## Overview
This project focuses on conducting a comprehensive analysis of traffic crash data from the City of Chicago. The goal is to preprocess a large, complex dataset, engineer meaningful features, and perform in-depth exploratory data analysis (EDA) to uncover key patterns, risk factors, and contributing causes of accidents across the city. The final processed dataset is prepared for advanced machine learning tasks.

## 💾 Data Sources and Preparation

The analysis utilizes a comprehensive dataset containing detailed information on millions of traffic crashes and the units/people involved.

### Initial Data Assessment
* The primary dataset initially contained over**2,000,000 crash records** with 48 columns.
* An associated dataset containing details about the units and people involved in the crashes was merged to enrich the main data model.
* All column names were converted to **lowercase** for ease of manipulation.

### Data Cleaning and Missing Value Strategy
A meticulous data cleaning process was executed to handle sparsity and standardize categorical entries:

1.  **Irrelevant Feature Removal:** Columns related to post-crash outcomes (e.g., various injury counts, damage severity) and high-cardinality fields (e.g., vehicle make, model, ID numbers) were dropped to focus on causal factors.
2.  **Missing Value Management:**
    * Columns with low missing percentages (under 5%) such as `street_direction`, `location`, `unit_type`, `travel_direction`, and `sex` were cleaned using the `dropna()` method to retain maximum data quality.
    * Columns with excessively high null values (e.g., **over 20% missing**) that were deemed unlikely to provide significant predictive power (including `vehicle_year`, `age`, and various driver/unit-specific condition records like `bac_result`, `physical_condition`, `driver_vision`, and `driver_action`) were removed to create a robust model base.

## ⚙️ Feature Engineering

Several new and transformed features were created to extract higher-level context and better represent complex categorical data.

| Engineered Feature | Description | Source Column(s) |
| :--- | :--- | :--- |
| **`cause_group`** | Simplified categorical groups for the primary causes of crashes, condensing 40 unique categories into a more manageable set. | `prim_contributory_cause` |
| **`trafficway_type`** | Grouped 20 granular trafficway types into 4 major categories: **Intersections**, **Single/Dual Carriageways**, **Non-standard/Access Roads**, and **Other/Unknown** to analyze crashes by road design. | `trafficway_type` |
| **`crash_day_of_week`** | Converted the numeric day-of-week codes (1-7) into meaningful weekday names (e.g., Monday, Sunday) for better interpretability. | `crash_day_of_week` |
| **`time_of_day`** | Categorized `crash_hour` into standard time blocks (e.g., 'Morning Rush', 'Late Night') to identify time-based crash trends. | `crash_hour` |

## 📈 Exploratory Data Analysis (EDA)

Univariate and initial bivariate analysis was performed on key features to understand the distribution of crashes.

### Key Univariate Findings:

* **Speed Limit:** The analysis of `posted_speed_limit` provided insight into the typical maximum speeds at the location of crashes.
* **Weather and Road Conditions:** Visualizations confirmed that the vast majority of crashes occur under **'CLEAR'** weather conditions and on **'DRY'** road surfaces, indicating that human factors or traffic density may outweigh environmental factors as primary causes for most accidents.
* **Crash Frequency by Type:** A count plot of **`first_crash_type`** was generated to rank the most common types of collisions (e.g., Rear End, Turning, Sideswipe).
* **Units Involved:** A bar plot of **`num_units`** revealed the overwhelming frequency of 2-unit crashes compared to those involving 3 or more vehicles.

### Geospatial Visualization
Preliminary work was done to use the available **latitude** and **longitude** data to map crash locations. A scatterplot was prepared to visualize the geographical distribution of accidents, with points colored by **`first_crash_type`** to quickly identify if certain crash types cluster regionally (e.g., more turning accidents downtown versus rear-end accidents on major expressways).

---

## 🚀 Next Steps

The highly cleaned and engineered data model, featuring standardized categorical data and enriched time/location features, is now finalized and ready for the next phase of the project.
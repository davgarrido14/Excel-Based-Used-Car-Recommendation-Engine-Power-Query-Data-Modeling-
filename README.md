# Excel‑Based Used Car Recommendation Engine (Power Query + Data Modeling)

This project is a full end‑to‑end used‑car evaluation system built entirely in **Excel** using **Power Query**, custom logic, and structured data modeling.  
It transforms raw vehicle listings into a clean, intelligent recommendation engine that classifies each car into actionable categories such as **Top Choice**, **Good Choice**, **Acceptable**, and **Avoid**.

---

## 🚗 Project Overview

The goal of this project is to evaluate used cars based on:
- Reliability (brand‑level reliability tiers)
- Model year
- Mileage
- Accident history
- Ownership history (one owner vs multiple owners)

Using Power Query, the dataset is cleaned, merged, enriched, and classified into meaningful purchase recommendations.

---

## 🔧 Key Features

### **1. Power Query Data Pipeline**
- Imported raw car listings
- Cleaned inconsistent fields (year, mileage, accident flags, ownership)
- Merged external reliability dataset by brand
- Added calculated columns for:
  - Decade
  - Mileage buckets
  - Accident status normalization
  - Ownership normalization

### **2. Reliability Integration**
A separate reliability table was created and merged into the main dataset.  
Each brand is assigned:
- **Exceptional Reliability**
- **Above Average Reliability**
- **Average Reliability**
- **Below Average / Poor Reliability** (if applicable)

This allows the recommendation engine to use brand‑level quality signals.

---

## 🧠 Purchase Recommendation Engine

A custom Power Query column applies multi‑layer logic to classify each vehicle.

### **Rules:**

#### 1. Accident History
- Any car with an accident → **Avoid**

#### 2. Ownership History
- Multiple owners → cannot be Top or Good Choice  
- At best → **Acceptable**

#### 3. Reliability + Year + Mileage Logic

## Purchase Recommendation Logic

### Business rules

**1. Accident Status**  
- Any accident → **Avoid**

**2. Ownership History**  
- Multiple owners → cannot be Top or Good Choice  
- At best → **Acceptable**

**3. Reliability, Year, Mileage tiers**

- **Top Choice**  
  - Exceptional Reliability  
  - Year ≥ 2014  
  - Mileage < 25,000  

- **Good Choice**  
  - Above Average Reliability  
  - Year ≥ 2012  
  - Mileage < 60,000  

- **Acceptable**  
  - Average Reliability  
  - Year ≥ 2010  
  - Mileage < 100,000  

- **Avoid**  
  - Everything else  

### Power Query M Code

```m
=
if [Accident Status] <> "No Accident" then "Avoid"

else if [One Owner] <> "One Owner" then "Acceptable"

else if [Reliability] = "Exceptional Reliability"
    and [year] >= 2014
    and [mileage] < 25000
then "Top Choice"

else if [Reliability] = "Above Average Reliability"
    and [year] >= 2012
    and [mileage] < 60000
then "Good Choice"

else if [Reliability] = "Average Reliability"
    and [year] >= 2010
    and [mileage] < 100000
then "Acceptable"

else "Avoid"
```

## Power Query Implementation Details
Data sources
Raw listings table
Brand reliability table

### Steps performed
Standardized column names and data types

Normalized accident and ownership fields

Merged reliability table

### Added calculated fields:

Decade

Mileage buckets

Purchase Recommendation

Loaded final query to Excel for pivoting

## Price Analysis
The workbook includes multiple price‑focused pivot tables:

1. Fuel Type → Average Price
Shows how fuel type affects pricing.

2. Mileage Bucket → Average Price
Reveals depreciation patterns by mileage range.

3. Mileage × Fuel Type → Average Price
Cross‑analysis showing how mileage impacts price differently across fuel types.

These pivots help identify pricing trends and value opportunities.

## Volume Analysis
1. Brand → Quantity
Shows which brands dominate the dataset.

2. Fuel Type → Quantity
Reveals market distribution of fuel types.

3. Decade → Quantity
Shows how many vehicles come from each decade.

These pivots help understand supply distribution and inventory composition.

Risk Analysis
1. Accident Status → Quantity
Shows how many vehicles have accident history.

2. Accident Status → Average Price
Reveals how accidents affect pricing.

3. Seller Rating → Quantity
Shows distribution of seller quality.

4. Seller Rating → Average Price
Shows how seller reputation influences pricing.

These insights help identify risk factors and pricing penalties.

## Quality and Ownership Analysis
1. One Owner → Quantity
Shows how many vehicles have single ownership.

2. One Owner → Average Price
Reveals the premium associated with single‑owner vehicles.

3. Personal Use Only → Quantity
Shows how many vehicles were not used commercially.

4. Personal Use Only → Average Price
Shows the pricing impact of personal‑use history.

## These pivots help evaluate vehicle quality and ownership patterns.

## Advanced Pricing and Revenue Modeling
This project includes a comprehensive pricing and revenue analysis framework that extends beyond basic averages. It incorporates adjusted ASP calculations, revenue forecasting, depreciation modeling, and fuel‑type‑specific pricing intelligence to support strategic decision‑making.

## Base Average Selling Price by Fuel Type
A baseline ASP table was created for the major fuel types:

Gasoline

Hybrid

Diesel

E85 Flex Fuel

Electric

For each fuel type, the model calculates:

Raw Average Selling Price

Adjusted ASP after applying discounts and premiums

Volume counts for revenue modeling

This establishes a consistent pricing foundation for downstream analysis.

ASP Adjustments
To simulate real‑world pricing behavior, the model applies a set of business‑driven adjustments:

Accident Discount: −8 percent

Low Seller Rating Discount: −3 percent

One‑Owner Premium: +3 percent

Personal Use Premium: +1 percent

These adjustments allow the system to reflect how condition, ownership, and seller quality influence market value.

Revenue Forecast by Fuel Type
Using the adjusted ASP and base volume for each fuel type, the model generates a revenue forecast.
For each fuel category, the system computes:

Base Volume

Adjusted ASP

Projected Revenue

This provides a clear view of which fuel types contribute the most revenue and how pricing adjustments impact total value.

## Depreciation Modeling by Mileage Bucket
A depreciation table was built to analyze how vehicle value changes across mileage ranges.
For each mileage bucket, the model includes:

Average Value

Observed Depreciation

Forecasted Depreciation

This helps identify where depreciation accelerates, stabilizes, or becomes nonlinear, supporting long‑term value analysis.



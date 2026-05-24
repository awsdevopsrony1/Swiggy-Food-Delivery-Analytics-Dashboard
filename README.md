# 🍊 Swiggy Food Delivery Analytics Dashboard

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power%20Query-217346?style=for-the-badge&logo=microsoft&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

An end-to-end interactive Power BI dashboard built on a large, multi-table Swiggy dataset — covering order trends, restaurant performance, user behavior, and city-wise delivery insights.

---

## 📌 Project Overview

Swiggy is one of India's largest food delivery platforms. This project analyzes Swiggy's business operations using a real-world multi-table dataset. The goal was to clean raw data, build a proper data model, and create an interactive dashboard that allows stakeholders to explore key business metrics across **4 report pages**.

---

## 🖥️ Dashboard Pages

### 1️⃣ Overview
High-level business summary with key KPIs and trends.

| Visual | Description |
|--------|-------------|
| KPI Cards | Orders Count, Users Count, Top 10% Customers, Rating Count, Sales Value, Price |
| Bar Chart | Top N Sales by City (dynamic ranking) |
| Line Chart | Total Quantity Amount over Years |
| Slicer | Food Type (Veg / Non-Veg / Other) |

---

### 2️⃣ User Performance
Deep dive into customer demographics and behavior.

| Visual | Description |
|--------|-------------|
| KPI Cards | User Count, Current Year Sales, Top 10% Customers, Previous Year Sales |
| Column Chart | User Count by Age Group |
| Bar Chart | Sales Value by Marital Status |
| Slicers | Gender, Year |

---

### 3️⃣ City Overview
Geographic and city-level performance breakdown.

| Visual | Description |
|--------|-------------|
| KPI Cards | Total Cities, Current Year Sales, Top 10% Customers, Previous Year Sales |
| Bar Charts | Sales by City, Users by City, Ratings by City |
| Map Visual | City-wise Sales Value (bubble size = revenue) |
| Table | City, Sales Value, Orders Count, Current Year Sales |
| Slicer | City |

---

### 4️⃣ Restaurant Analysis
Restaurant-level performance, cuisine trends, and pricing analysis.

| Visual | Description |
|--------|-------------|
| KPI Cards | Restaurant Count, Current Year Sales, Avg Rating, Previous Year Sales |
| Bar Charts | Restaurants by City, Top Restaurants by Rating |
| Donut Charts | Food Type Distribution, Cuisine Distribution |
| Area Chart | Cuisine vs Price |
| Slicer | Restaurant Name |

---

## 🗂️ Data Model

The project follows a **Star Schema** with the following tables:

```
Orders (Fact Table)
    ├── Users (Dimension)
    ├── Restaurants (Dimension)
    ├── City (Dimension)
    └── Date Table (Time Intelligence)
```

- `Orders` is the central fact table linked to all dimension tables via foreign keys
- A custom **Date Table** was created using `CALENDAR()` DAX function and marked as a Date Table to enable time intelligence functions

---

## 🧹 Data Cleaning Steps

All cleaning was performed in **Power Query Editor**:

- Removed duplicate rows across all tables
- Handled missing/null values (replaced with 0 or appropriate defaults)
- Corrected data types — dates stored as text, numeric IDs as strings
- Standardized inconsistent city name spellings
- Split and merged columns to normalize data structure
- Removed irrelevant/blank columns

---

## 📐 Key DAX Measures

```dax
-- Current Year Sales
Current_year_sales = TOTALYTD(SUM(Orders[Sales_Value]), Dates[Date])

-- Previous Year Sales
previous_year_sales = CALCULATE(SUM(Orders[Sales_Value]), SAMEPERIODLASTYEAR(Dates[Date]))

-- Average Rating
Avg Rating = AVERAGE(Restaurant[Rating])

-- Top 10% Customers
Top10%customers = 
    CALCULATE(
        COUNTROWS(Users),
        TOPN(INT(COUNTROWS(Users) * 0.1), Users, [Sales Value], DESC)
    )

-- Top N Sales (Dynamic)
Top N sales = 
    IF(
        RANKX(ALL(Orders[City]), [Sales Value]) <= SELECTEDVALUE(TopN[Value]),
        [Sales Value]
    )
```

---

## 🛠️ Tools & Technologies

| Tool | Usage |
|------|-------|
| Power BI Desktop | Dashboard development & publishing |
| Power Query Editor | Data cleaning & transformation (ETL) |
| DAX | Calculated columns, measures, KPIs |
| Data Modeling | Star schema, table relationships |

---

## 💡 Key Business Insights

- Identified **top revenue-generating cities** and peak order hours for targeted marketing
- Uncovered **cuisine preference trends** and restaurant performance gaps
- Analyzed **customer demographics** (age, gender, marital status) to surface retention opportunities
- Compared **year-over-year sales** to track business growth trends
- Mapped **city-wise delivery ratings** to highlight service quality gaps

---

## 📁 Repository Structure

```
📦 Swiggy-Food-Delivery-Analytics-Dashboard
 ┣ 📄 DASHBAORD_OF_SWIGGY.pbix      ← Power BI Dashboard file
 ┣ 📄 README.md                      ← Project documentation
```

---

## 🚀 How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/awsdevopsrony1/Swiggy-Food-Delivery-Analytics-Dashboard.git
   ```
2. Open `DASHBAORD_OF_SWIGGY.pbix` in **Power BI Desktop**
3. Navigate through the 4 report pages using the bottom tabs
4. Use the slicers to filter data dynamically

> **Requirements:** Power BI Desktop (free) — [Download here](https://powerbi.microsoft.com/desktop/)

---

## 👤 Author

**Parth Patoliya**  
Data Analyst | Power BI Developer  
📧 [Gmail](#) | 💼 [LinkedIn](#) | 🐙 [GitHub](#) | 🗂️ [Project Portfolio](#)

---

## ⭐ If you found this project helpful, give it a star!

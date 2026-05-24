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
High-level business summary — Orders Count, Users Count, Top 10% Customers, Rating Count, Sales Value by Food Type (Veg / Non-Veg / Others), Top N Sales by City, and Total Quantity Amount trend over years.

![Overview](overview_png.png)

---

### 2️⃣ User Performance
Customer demographics and behavior — User Count by Age group, Sales by Marital Status, Current Year vs Previous Year Sales, filtered by Gender and Year.

![User Performance](user_performance_png.png)

---

### 3️⃣ City Overview
Geographic breakdown — Top 5 City Wise Sales, User Count by City, Rating Count by City, India Map visual, and a detailed City summary table with Sales, Orders, and Current Year Sales.

![City Overview](city_overview_png.png)

---

### 4️⃣ Restaurant Analysis
Restaurant-level performance — Restaurant Count by City, Top Restaurants by Rating, Food Type distribution (Veg vs Non-Veg), Cuisine distribution donut chart, and Price of Cuisine area chart.

![Restaurant Analysis](restaurant_analysis_png.png)

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

- **Tirupati** is the top revenue city with ₹42.5M in sales and 243 orders
- **149K total orders** placed across **821 cities** on the platform
- **Non-Veg dominates** restaurant listings at 69.83% vs Veg at 30.17%
- **North Indian & Indian Chinese** are the most popular cuisines (24% each)
- **Domino's Pizza** leads in ratings with 442 ratings among all restaurants
- **Single users** generate significantly more sales (₹40,825K) vs married users (₹15,691K)
- **Bikaner** has the highest user count per city at 2K orders

---

## 📁 Repository Structure

```
📦 Swiggy-Food-Delivery-Analytics-Dashboard
 ┣ 📄 DASHBAORD_OF_SWIGGY.pbix         ← Power BI Dashboard file
 ┣ 🖼️ overview_png.png                  ← Overview page screenshot
 ┣ 🖼️ user_performance_png.png          ← User Performance page screenshot
 ┣ 🖼️ city_overview_png.png             ← City Overview page screenshot
 ┣ 🖼️ restaurant_analysis_png.png       ← Restaurant Analysis page screenshot
 ┣ 📄 README.md                         ← Project documentation
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

⭐ If you found this project helpful, give it a star!

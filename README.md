# 🧸 Maven Toys Sales Analysis | Power BI

An end-to-end **Power BI business intelligence project** analyzing Maven Toys sales, profitability, inventory, product performance, and store performance across multiple locations.

This project demonstrates practical skills in **Power BI, DAX, data modeling, dashboard development, KPI tracking, and business analysis**.

---

## 📌 Project Overview

The **Maven Toys Sales Analysis** project explores sales data from **2022–2023** to identify trends and business opportunities across:

- Products
- Product Categories
- Stores
- Store Locations
- Cities
- Revenue
- Profitability
- Inventory
- Time

The dashboard is designed to help business users quickly understand overall performance while also allowing deeper analysis at the **product, category, and store level**.

---

## 🎯 Business Objectives

The main objectives of this project are to:

- Identify top-performing **products and categories**
- Analyze revenue contribution by **store and location**
- Track sales performance across **year, quarter, and month**
- Evaluate overall **profitability and profit margins**
- Monitor inventory levels and turnover
- Identify fast-moving and slow-moving products
- Support product planning and store optimization decisions
- Provide an interactive self-service reporting experience

---

## 🔗 Power BI Project File

📊 [View / Download Maven Toys Sales Analysis](https://github.com/pradesh101/Maven_Toys_Sales_Project_Analysis/blob/main/Maven_Toys_Sales_Analysis.pbix)

---

## 🧩 Data Model

The project uses a **star-schema-inspired relational data model** designed for efficient filtering, aggregation, and analysis in Power BI.

### Sales – Fact Table

| Column | Description |
|---|---|
| Sale_ID | Unique sales transaction identifier |
| Date | Date of transaction |
| Year | Sales year |
| Product_ID | Product identifier |
| Store_ID | Store identifier |
| Units | Number of units sold |

### Products – Dimension Table

| Column | Description |
|---|---|
| Product_ID | Unique product identifier |
| Product_Name | Product name |
| Product_Category | Product category |
| Product_Price | Product selling price |
| Product_Cost | Product cost |

### Stores – Dimension Table

| Column | Description |
|---|---|
| Store_ID | Unique store identifier |
| Store_Name | Store name |
| Store_City | City where the store is located |
| Store_Location | Store location type |

### Inventory – Fact / Bridge Table

| Column | Description |
|---|---|
| Product_ID | Product identifier |
| Store_ID | Store identifier |
| Stock_On_Hand | Current inventory quantity |

---

## 🔗 Table Relationships

The main relationships used in the data model are:

```text
Products (1) ──────── (*) Sales
Stores   (1) ──────── (*) Sales

Products (1) ──────── (*) Inventory
Stores   (1) ──────── (*) Inventory
```

This structure enables accurate aggregation and filtering across products, stores, inventory, and sales.

---

## 🗂️ Data Model Preview

![Data Model](https://github.com/Yash-Yennewar/Maven_Toys_Sales_Project_Analysis/raw/main/Screenshots/Datamodel.png)

---

## 🧮 DAX Measures

Several DAX measures were created to calculate business KPIs and support dashboard analysis.

### Total Revenue

```DAX
Total_Revenue =
SUMX(
    Sales,
    Sales[Units] * RELATED(Products[Product_Price])
)
```

### Total Profit

```DAX
Total_Profit =
SUMX(
    Sales,
    Sales[Units] *
    (
        RELATED(Products[Product_Price]) -
        RELATED(Products[Product_Cost])
    )
)
```

### Profit Margin %

```DAX
Profit_Margin_% =
DIVIDE(
    [Total_Profit],
    [Total_Revenue],
    0
)
```

### Order Count

```DAX
Order_Count =
DISTINCTCOUNT(Sales[Sale_ID])
```

### Highest Revenue Product

```DAX
Highest_Revenue_ProductName =
VAR ProductRevenue =
    SUMMARIZE(
        Products,
        Products[Product_Name],
        "TotalRevenue",
        CALCULATE(
            SUMX(
                Sales,
                Sales[Units] * RELATED(Products[Product_Price])
            )
        )
    )

VAR TopProduct =
    TOPN(
        1,
        ProductRevenue,
        [TotalRevenue],
        DESC
    )

RETURN
    MAXX(
        TopProduct,
        Products[Product_Name]
    )
```

---

# 📊 Dashboard 1 – Executive Sales Overview

The first dashboard provides a high-level overview of overall business performance.

## Key KPIs

| KPI | Value |
|---|---:|
| 💰 Total Revenue | **$14.44M** |
| 📈 Total Profit | **$4.01M** |
| 📦 Total Units Sold | **1.09M** |
| 💹 Profit Margin | **27.79%** |
| 🧾 Total Orders | **829K** |

---

## Visualizations

The executive dashboard includes:

- Revenue trend by **Year, Quarter, and Month**
- Revenue contribution by **Store Location**
- Revenue breakdown by **Product Category**
- Geographic sales analysis by **Store City**
- KPI cards for sales and profitability metrics

---

## Key Insights

- **Downtown stores generate approximately 57% of total revenue**, making them the strongest-performing store location.
- The **Toys category** is one of the largest revenue contributors.
- Monthly revenue patterns reveal noticeable **seasonal sales trends**.
- Geographic analysis helps identify high-performing cities and store locations.

---

## Dashboard Preview

![Executive Dashboard](https://github.com/Yash-Yennewar/Maven_Toys_Sales_Project_Analysis/raw/main/Screenshots/Dashboard.png)

---

# 📊 Dashboard 2 – Category & Store Sales Analysis

The second dashboard provides a deeper analysis of product, category, inventory, and store-level performance.

## Key Metrics

- **35 Total Products**
- **50 Total Stores**
- **Highest Revenue Product: Lego Bricks**
- Sales per Store
- Average Order Value
- Inventory Turnover
- Average Inventory

---

## Product-Level Analysis

The dashboard analyzes individual products using metrics such as:

- Revenue
- Profit
- Profit Margin
- Order Count
- Cost
- Units Sold

This helps identify products that generate strong revenue while also maintaining healthy profitability.

---

## Store-Level Analysis

Store performance is evaluated using:

- Total Orders
- Units Sold
- Average Order Value
- Revenue
- Store Location

This allows users to compare store efficiency and identify potential opportunities for improvement.

---

## Key Insights

- **Lego Bricks** is the highest revenue-generating product.
- Some stores generate a high number of orders but have a lower **Average Order Value**, indicating potential upselling opportunities.
- Inventory turnover helps distinguish between **fast-moving and slow-moving products**.
- Store location significantly influences sales performance.
- Product and store-level comparisons can support inventory allocation and promotion planning.

---

## Dashboard Preview

![Category and Store Dashboard](https://github.com/Yash-Yennewar/Maven_Toys_Sales_Project_Analysis/raw/main/Screenshots/Dashboard1.png)

---

# 🎛️ Dashboard Interactivity

The Power BI report includes interactive filtering and cross-filtering functionality.

### Available Slicers

- Year
  - 2022
  - 2023
- Product Category
- Store Location

### Interactive Features

- Cross-filtering between visuals
- Dynamic KPI updates
- Drill-down by time
- Category-level filtering
- Store-level filtering
- Product-level analysis

These features allow users to perform flexible **self-service business analysis** directly from the dashboard.

---

# 📈 Key Business Takeaways

Based on the analysis, several business recommendations can be identified:

### 1. Prioritize High-Margin Products

Focus inventory, marketing, and promotions on products that generate both strong revenue and high profit margins.

### 2. Optimize Downtown Stores

Since Downtown locations contribute the largest share of revenue, these stores should receive strong inventory availability and operational support.

### 3. Improve Lower-Performing Locations

Store locations with lower revenue contribution should be analyzed further for differences in product mix, customer demand, and sales strategy.

### 4. Improve Inventory Efficiency

Inventory turnover can be used to identify slow-moving products and reduce unnecessary inventory holding costs.

### 5. Increase Average Order Value

Stores with high transaction volume but lower average order value may benefit from:

- Product bundling
- Cross-selling
- Upselling
- Targeted promotions

### 6. Use Seasonal Trends for Planning

Historical monthly and quarterly sales trends can help improve:

- Inventory planning
- Demand forecasting
- Seasonal promotions
- Product availability

---

# 🛠️ Tools & Technologies

This project was developed using:

- **Power BI Desktop**
- **DAX – Data Analysis Expressions**
- **Data Modeling**
- **Relational Data Models**
- **Power BI Maps**
- **Data Visualization**
- **Business Intelligence**
- **Maven Analytics Dataset**

---

# 📂 Repository Structure

```text
Maven_Toys_Sales_Project_Analysis/
│
├── Maven_Toys_Sales_Analysis.pbix
│
├── README.md
│
└── Screenshots/
    ├── Datamodel.png
    ├── Dashboard.png
    └── Dashboard1.png
```

---

# 🚀 Skills Demonstrated

This project demonstrates practical experience with:

- Power BI Dashboard Development
- Data Cleaning and Transformation
- Data Modeling
- Star Schema Design
- DAX Measures
- KPI Development
- Revenue Analysis
- Profitability Analysis
- Inventory Analysis
- Store Performance Analysis
- Product Performance Analysis
- Data Visualization
- Business Storytelling
- Data-Driven Decision Making

---

# 📌 Project Summary

The **Maven Toys Sales Analysis** project provides an interactive business intelligence solution for analyzing sales, profitability, inventory, products, and store performance.

By combining **Power BI dashboards, DAX calculations, relational data modeling, and business-focused KPIs**, the project transforms raw transactional data into actionable insights that can support better decisions in:

- Inventory planning
- Product strategy
- Store optimization
- Profitability management
- Sales forecasting
- Business performance monitoring

---

## 👤 Author

**Pradesh Gwachha**

Power BI | Data Analytics | Business Intelligence

---

⭐ If you found this project useful, consider giving the repository a **star**.

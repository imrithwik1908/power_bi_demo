# Power BI Dashboard Documentation: E-Commerce Analytics

This document outlines the steps to create a comprehensive Power BI Dashboard using a fake e-commerce dataset. The dataset is generated in Python and includes a variety of parameters to enable robust analysis and visualizations. The document also demonstrates the use of DAX expressions for deriving insights, creating advanced measures, and utilizing them for visualizations. Spaces are left for images to aid visual representation.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Dataset Structure](#dataset-structure)
3. [Loading Data into Power BI](#loading-data-into-power-bi)
4. [Data Modeling and Relationships](#data-modeling-and-relationships)
5. [Creating Visualizations](#creating-visualizations)
   - [Visualization 1: Sales Trend Analysis](#visualization-1-sales-trend-analysis)
   - [Visualization 2: Profit by Product Category](#visualization-2-profit-by-product-category)
   - [Visualization 3: Top 10 Customers by Sales](#visualization-3-top-10-customers-by-sales)
   - [Visualization 4: Average Discount by Product](#visualization-4-average-discount-by-product)
   - [Visualization 5: Delivery Time Analysis](#visualization-5-delivery-time-analysis)
6. [Advanced DAX Expressions](#advanced-dax-expressions)
7. [Final Dashboard Overview](#final-dashboard-overview)
8. [Future Enhancements](#future-enhancements)

---

## Project Overview

This project demonstrates the creation of a professional Power BI dashboard for analyzing e-commerce performance. The dataset includes various parameters to facilitate comprehensive analysis.

### Dataset Parameters:
- **Order Details**: Order ID, Product ID, Customer ID, Order Date, Delivery Date.
- **Product Metrics**: Price, Quantity, Discount, Sales, Profit.

### Objectives:
- Showcase key e-commerce metrics through interactive visualizations.
- Use advanced DAX expressions for deriving deeper insights.
- Present a polished and professional Power BI report.

---

## Dataset Structure

### Dataset Columns:

| Column Name       | Description                                     |
|-------------------|-------------------------------------------------|
| Order ID          | Unique identifier for each order               |
| Customer ID       | Unique identifier for each customer            |
| Product ID        | Unique identifier for each product             |
| Order Date        | Date when the order was placed                 |
| Delivery Date     | Date when the order was delivered              |
| Price             | Unit price of the product                      |
| Quantity          | Number of units ordered                        |
| Discount          | Discount applied to the order (percentage)     |
| Sales             | Total sales amount after discount              |
| Profit            | Profit earned on the order                     |

### Dataset Characteristics:
- Orders are simulated for the last two years.
- Discounts are applied randomly, with values between 0% and 30%.
- Sales and profits are calculated based on quantity, price, and discount.

---

## Loading Data into Power BI

### Instructions:
1. Open **Power BI Desktop**.
2. Click on **Get Data > Text/CSV**.
3. Select the `ecommerce_data.csv` file.
4. Review the data preview and click **Load**.

---

## Data Modeling and Relationships

### Steps:
1. Navigate to the **Model View** in Power BI.
2. Create relationships between tables if additional tables are added:
   - `Customer ID` (Orders Table) -> `Customer ID` (Customer Details Table).
   - `Product ID` (Orders Table) -> `Product ID` (Product Details Table).
3. Ensure the relationship cardinality is set correctly (e.g., One-to-Many).

---

## Creating Visualizations

### Visualization 1: Sales Trend Analysis
#### Steps:
1. Add a **Line Chart** to the canvas.
2. Drag **Order Date** to the X-Axis.
3. Drag **Sales** (measure) to the Y-Axis.
4. Set the X-Axis to display data by Month.

#### DAX Measure:
```dax
Total Sales = SUM(Orders[Sales])
```

**[Space for Image: Sales Trend Analysis Visualization]**

### Visualization 2: Profit by Product Category
#### Steps:
1. Add a **Clustered Bar Chart**.
2. Drag **Product ID** to the X-Axis.
3. Drag **Profit** (measure) to the Y-Axis.
4. Sort the chart by Profit in descending order.

#### DAX Measure:
```dax
Total Profit = SUM(Orders[Profit])
```

**[Space for Image: Profit by Product Category Visualization]**

### Visualization 3: Top 10 Customers by Sales
#### Steps:
1. Add a **Table** to the canvas.
2. Drag **Customer ID** and **Sales** to the table.
3. Use a DAX measure to filter the top 10 customers by sales:
   ```dax
   Top 10 Customers = 
   TOPN(10, 
        SUMMARIZE(Orders, Orders[Customer ID], "Customer Sales", SUM(Orders[Sales])), 
        [Customer Sales], DESC)
   ```
4. Apply the measure to the visualization.

**[Space for Image: Top 10 Customers Visualization]**

### Visualization 4: Average Discount by Product
#### Steps:
1. Add a **Bar Chart**.
2. Drag **Product ID** to the X-Axis.
3. Drag **Average Discount** (DAX measure) to the Y-Axis.

#### DAX Measure:
```dax
Average Discount = AVERAGE(Orders[Discount])
```

**[Space for Image: Average Discount by Product Visualization]**

### Visualization 5: Delivery Time Analysis
#### Steps:
1. Add a **Histogram** to the canvas.
2. Create a calculated column to compute delivery time:
   ```dax
   Delivery Time = DATEDIFF(Orders[Order Date], Orders[Delivery Date], DAY)
   ```
3. Drag **Delivery Time** to the X-Axis.
4. Drag **Order Count** (DAX measure) to the Y-Axis.

#### DAX Measure:
```dax
Order Count = COUNT(Orders[Order ID])
```

**[Space for Image: Delivery Time Analysis Visualization]**

---

## Advanced DAX Expressions

### Additional Measures

#### Sales Growth:
```dax
Sales Growth = 
DIVIDE( 
    [Total Sales] - CALCULATE([Total Sales], DATEADD(Orders[Order Date], -1, MONTH)), 
    CALCULATE([Total Sales], DATEADD(Orders[Order Date], -1, MONTH))
)
```

#### Profit Margin:
```dax
Profit Margin = DIVIDE([Total Profit], [Total Sales])
```

#### Discount Impact:
```dax
Discount Impact = SUMX(Orders, Orders[Discount] * Orders[Quantity])
```

### Using Measures in Visualizations

1. **Sales Growth Analysis**:
   - Add a Line Chart.
   - X-Axis: Order Date.
   - Y-Axis: Sales Growth (DAX measure).

**[Space for Image: Sales Growth Visualization]**

2. **Profit Margin by Product**:
   - Add a Bar Chart.
   - X-Axis: Product ID.
   - Y-Axis: Profit Margin (DAX measure).

**[Space for Image: Profit Margin Visualization]**

---

## Final Dashboard Overview

### Pages:
1. **Page 1: Overview**:
   - Total Sales (Card).
   - Total Profit (Card).
   - Sales Trend (Line Chart).

2. **Page 2: Customer Insights**:
   - Top 10 Customers (Table).
   - Average Discount by Product (Bar Chart).

3. **Page 3: Product Insights**:
   - Profit by Product Category (Bar Chart).
   - Delivery Time Analysis (Histogram).

**[Space for Images of Each Page]**

---

## Future Enhancements

- Add advanced predictive analytics using Python or R scripts.
- Incorporate additional DAX measures for segmentation analysis.
- Improve interactivity with slicers and filters for dynamic insights.

---

This documentation serves as a comprehensive guide to create and enhance an e-commerce analytics dashboard in Power BI. Insert screenshots at designated spaces to provide visual context.

# Power BI Dashboard Documentation: E-Commerce Analytics

This document outlines the steps to create a comprehensive Power BI Dashboard using a fake e-commerce dataset. The dataset is generated in Python and includes a variety of parameters to enable robust analysis and visualizations. The document also demonstrates the use of DAX expressions for deriving insights, creating advanced measures, and utilizing them for visualizations. Spaces are left for images to aid visual representation.

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Dataset Generation](#dataset-generation)
3. [Loading Data into Power BI](#loading-data-into-power-bi)
4. [Data Modeling and Relationships](#data-modeling-and-relationships)
5. [Creating Visualizations](#creating-visualizations)
   - [Visualization 1: Sales Trend Analysis](#visualization-1-sales-trend-analysis)
   - [Visualization 2: Profit by Product Category](#visualization-2-profit-by-product-category)
   - [Visualization 3: Top 10 Customers by Sales](#visualization-3-top-10-customers-by-sales)
   - [Visualization 4: Sales by Region](#visualization-4-sales-by-region)
6. [Advanced DAX Expressions](#advanced-dax-expressions)
   - [Creating Measures](#creating-measures)
   - [Using Measures in Visualizations](#using-measures-in-visualizations)
7. [Final Dashboard Overview](#final-dashboard-overview)
8. [Future Enhancements](#future-enhancements)

---

## Project Overview

This project demonstrates the creation of a professional Power BI dashboard for analyzing e-commerce performance. The dataset includes various parameters to facilitate comprehensive analysis.

### Dataset Parameters:
- **Order Details**: Order ID, Product ID, Customer ID, Order Date, Delivery Date.
- **Product Details**: Product Category, Sub-category, Price, Quantity.
- **Customer Details**: Age, Gender, Location.
- **Sales Metrics**: Total Sales, Profit, Discounts.

### Objectives:
- Showcase key e-commerce metrics through interactive visualizations.
- Use advanced DAX expressions for deriving deeper insights.
- Present a polished and professional Power BI report.

---

## Dataset Generation

Generate the dataset using Python. Save it as a CSV file for use in Power BI. Below is the detailed script:

### Python Script:

```python
import pandas as pd
import random
import numpy as np
from faker import Faker

fake = Faker()

# Generate Orders Data
num_records = 1000
orders = []
for _ in range(num_records):
    order_id = fake.uuid4()
    customer_id = random.randint(1000, 2000)
    product_id = random.randint(1, 100)
    order_date = fake.date_between(start_date="-2y", end_date="today")
    delivery_date = fake.date_between(start_date=order_date, end_date="+15d")
    price = round(random.uniform(10, 200), 2)
    quantity = random.randint(1, 5)
    discount = round(random.uniform(0, 0.3), 2)
    sales = price * quantity * (1 - discount)
    profit = sales * round(random.uniform(0.1, 0.3), 2)
    orders.append([order_id, customer_id, product_id, order_date, delivery_date, price, quantity, discount, sales, profit])

# Create DataFrame
columns = ["Order ID", "Customer ID", "Product ID", "Order Date", "Delivery Date", "Price", "Quantity", "Discount", "Sales", "Profit"]
orders_df = pd.DataFrame(orders, columns=columns)

# Save to CSV
orders_df.to_csv("ecommerce_data.csv", index=False)
```

### Steps to Run the Script:
1. Install required libraries: `pip install pandas faker`.
2. Copy the script into a Python file (e.g., `generate_data.py`).
3. Run the script to generate `ecommerce_data.csv`.

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
3. Drag **Total Sales** (measure) to the Y-Axis.
4. Set the X-Axis to display data by Month.

**[Space for Image: Sales Trend Analysis Visualization]**

### Visualization 2: Profit by Product Category
#### Steps:
1. Add a **Clustered Bar Chart**.
2. Drag **Product Category** to the X-Axis.
3. Drag **Profit** (measure) to the Y-Axis.
4. Sort the chart by Profit in descending order.

**[Space for Image: Profit by Product Category Visualization]**

---

## Advanced DAX Expressions

### Creating Measures
#### Total Sales:
```dax
Total Sales = SUM(Orders[Sales])
```

#### Total Profit:
```dax
Total Profit = SUM(Orders[Profit])
```

#### Sales Growth:
```dax
Sales Growth = 
DIVIDE( 
    [Total Sales] - CALCULATE([Total Sales], DATEADD('Orders'[Order Date], -1, MONTH)), 
    CALCULATE([Total Sales], DATEADD('Orders'[Order Date], -1, MONTH))
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

2. **Profit Margin by Category**:
   - Add a Bar Chart.
   - X-Axis: Product Category.
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
   - Sales by Region (Map).

3. **Page 3: Product Insights**:
   - Profit by Product Category (Bar Chart).
   - Sales and Profit Margins (Combo Chart).

**[Space for Images of Each Page]**

---

## Future Enhancements

- Add advanced predictive analytics using Python or R scripts.
- Incorporate additional DAX measures for segmentation analysis.
- Improve interactivity with slicers and filters for dynamic insights.

---

This documentation serves as a comprehensive guide to create and enhance an e-commerce analytics dashboard in Power BI. Insert screenshots at designated spaces to provide visual context.

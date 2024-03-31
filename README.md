# Pizza Sales Analysis

### Project Overview

This data analysis project aims to provide insights into the Pizza Sales performance over the past years. By analyzing various aspects of the Pizza Sales data, we seek to identify trends, make data-driven recommendations, and gain a deeper understanding of the sales's performance.

### Data Sources

Pizza Sales Data: The primary dataset used for this analysis is the "pizza_sales.csv" file, containing detailed information about each sales made.

### Tools

- Excel - Data Cleaning [Download here](https://microsoft.com)
- SQL Server - Data Analysis
- PowerBI - Creating reports


### Data Cleaning/Preparation

In the initial data preparation phase, i performed the following tasks:
1. Data loading and inspection.
2. Handling missing values.
3. Data cleaning and formatting.


### Exploratory Data Analysis

EDA involved exploring the pizza sales data to answer key questions such as:

- Daily and Monthly trends for total orders.
- Percentage of sales by pizza category.
- Percentage of sales by pizza sizes.
- Total pizzas sold by pizza category.
- Top 5 best sellers by Revenue, Total Quantity and Total Orders.
- Bottom/Least 5 sellers by Revenue, Total Quantity and Total Orders


### Data Analysis



```sql
-- Total Revenue:
SELECT SUM(total_price) AS Total_Revenue
FROM Pizza_sales;

-- Average Order Value:
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS Avg_Order_Value
FROM Pizza_sales;

-- Total Pizza Sold:
SELECT SUM(quantity) AS Total_pizza_sold
FROM Pizza_sales;

-- Total Order:
SELECT COUNT(DISTINCT Order_id) AS Total_orders
FROM Pizza_sales;

-- Average Pizzas Per Order:
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales;



--For Visualization(PowerBI)


-- Daily Trend for Orders:
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);

-- Monthly Trend for Orders:
SELECT DATENAME(MONTH, order_date) AS month_name, COUNT(DISTINCT order_id) AS total_orders
FROM pizza_sales
GROUP BY DATENAME(MONTH, order_date);

-- % Of Sales by Pizzas Category:
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue, CAST(SUM(total_price) * 100 / 
                                                                                                            (SELECT SUM(total_price)
                                                                                                            FROM pizza_sales) AS DECIMAL(10,2)) AS Per_total_sales
FROM Pizza_sales
GROUP BY pizza_category;

-- % Of Sales by Pizzas Size:
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) AS total_revenue, CAST(SUM(total_price) * 100 /
								                                                                                        (SELECTSUM(total_price)
                                                                                                        FROM pizza_sales) AS DECIMAL(10,2)) AS per_total_sales
FROM Pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;

-- Total Pizzas Sold by Pizza Category:
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;

-- Top 5 Pizzas by Revenue:
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;

-- Bottom 5 Pizzas by Revenue:
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC;

-- Top 5 Pizzas by Quantity:
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC;

--  Bottom 5 Pizzas by Quantity:
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC;

-- Top 5 Pizzas by Total Orders:
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC;

-- Borrom 5 Pizzas by Total Orders
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC;

```


















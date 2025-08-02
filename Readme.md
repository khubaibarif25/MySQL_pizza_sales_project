# 🍕 Pizza Sales Data Analysis (MySQL Project)

## 📌 Overview
This SQL project focuses on analyzing sales data from a fictional pizza restaurant to derive business insights and inform decision-making. Using SQL queries, the project uncovers patterns in order volume, revenue, and customer behavior based on date, time, and pizza categories.

## 🎯 Objectives
- Analyze total orders, revenue, and sales trends.
- Identify best-selling and least-selling pizzas.
- Uncover time-based and category-based ordering patterns.
- Provide data-driven insights for business growth.

## 🗂️ Database Structure
The database consists of three main tables:

1. **orders**
   - Contains order-level details including `order_id` and `order_date`.
   
2. **order_details**
   - Links orders with specific pizzas and quantities sold.
   - Fields include `order_details_id`, `order_id`, `pizza_id`, and `quantity`.

3. **pizzas**
   - Contains details about each pizza such as `pizza_type_id`, `size`, `price`, etc.

4. **pizza_types**
   - Stores metadata for each pizza like `name`, `category`, and `ingredients`.

## 🔧 Tools Used
- **MySQL** for querying and data analysis
- **MySQL Workbench** or **XAMPP/phpMyAdmin** (recommended for local testing)
- CSV data (imported into MySQL database)

## 📊 Key SQL Operations
- `JOIN` operations to combine multiple tables
- `GROUP BY` for aggregation
- `ORDER BY` for ranking sales
- `DATE_FORMAT` and `DAYNAME` for time-based analysis
- `LIMIT` to find top-selling or bottom-selling items
- Aggregate functions: `SUM()`, `COUNT()`, `AVG()`

## 📈 Insights Generated

1. **Total Number of Orders**
   ```sql
   SELECT COUNT(order_id) AS total_orders FROM orders; 

2. ** Total Revenue**
SELECT ROUND(SUM(od.quantity * p.price), 2) AS total_revenue
FROM order_details od
JOIN pizzas p ON p.pizza_id = od.pizza_id; 

3. **Average Order Value**

SELECT ROUND(SUM(od.quantity * p.price) / COUNT(DISTINCT od.order_id), 2) AS avg_order_value
FROM order_details od
JOIN pizzas p ON p.pizza_id = od.pizza_id;

4. **Top 5 Best-Selling Pizzas**

SELECT pt.name, SUM(od.quantity) AS total_sold
FROM order_details od
JOIN pizzas p ON p.pizza_id = od.pizza_id
JOIN pizza_types pt ON pt.pizza_type_id = p.pizza_type_id
GROUP BY pt.name
ORDER BY total_sold DESC
LIMIT 5; 

5. **Hourly Order Distribution**
SELECT HOUR(order_time) AS hour, COUNT(order_id) AS total_orders
FROM orders
GROUP BY HOUR(order_time)
ORDER BY hour;



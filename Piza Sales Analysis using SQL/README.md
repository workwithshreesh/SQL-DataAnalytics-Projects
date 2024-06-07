# Pizza Sales Analysis Project

## Overview

This project involves analyzing pizza sales data using SQL to answer key business questions. The analysis is divided into three sections: Basic, Intermediate, and Advanced, each with specific objectives to uncover insights related to total orders, revenue, popular pizza types, and order distribution.

## Basic Analysis

### Objectives

1. **Retrieve the total number of orders placed.**
2. **Calculate the total revenue generated from pizza sales.**
3. **Identify the highest-priced pizza.**
4. **Identify the most common pizza size ordered.**
5. **List the top 5 most ordered pizza types along with their quantities.**

### SQL Queries

1. **Total Number of Orders:**
   ```sql
   SELECT COUNT(*) AS total_orders
   FROM orders;
   ```

2. **Total Revenue from Pizza Sales:**
   ```sql
   SELECT SUM(price * quantity) AS total_revenue
   FROM order_details;
   ```

3. **Highest-Priced Pizza:**
   ```sql
   SELECT pizza_name, MAX(price) AS highest_price
   FROM pizzas
   GROUP BY pizza_name
   ORDER BY highest_price DESC
   LIMIT 1;
   ```

4. **Most Common Pizza Size Ordered:**
   ```sql
   SELECT size, COUNT(size) AS count
   FROM order_details
   GROUP BY size
   ORDER BY count DESC
   LIMIT 1;
   ```

5. **Top 5 Most Ordered Pizza Types:**
   ```sql
   SELECT pizza_name, SUM(quantity) AS total_quantity
   FROM order_details
   GROUP BY pizza_name
   ORDER BY total_quantity DESC
   LIMIT 5;
   ```

## Intermediate Analysis

### Objectives

1. **Total quantity of each pizza category ordered.**
2. **Distribution of orders by hour of the day.**
3. **Category-wise distribution of pizzas.**
4. **Average number of pizzas ordered per day.**
5. **Top 3 most ordered pizza types based on revenue.**

### SQL Queries

1. **Total Quantity of Each Pizza Category:**
   ```sql
   SELECT category, SUM(quantity) AS total_quantity
   FROM order_details
   JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
   GROUP BY category;
   ```

2. **Distribution of Orders by Hour:**
   ```sql
   SELECT HOUR(order_time) AS hour, COUNT(*) AS total_orders
   FROM orders
   GROUP BY hour
   ORDER BY hour;
   ```

3. **Category-wise Distribution of Pizzas:**
   ```sql
   SELECT category, COUNT(*) AS total_orders
   FROM order_details
   JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
   GROUP BY category;
   ```

4. **Average Number of Pizzas Ordered Per Day:**
   ```sql
   SELECT order_date, AVG(quantity) AS avg_pizzas
   FROM order_details
   JOIN orders ON order_details.order_id = orders.order_id
   GROUP BY order_date;
   ```

5. **Top 3 Most Ordered Pizza Types by Revenue:**
   ```sql
   SELECT pizza_name, SUM(price * quantity) AS total_revenue
   FROM order_details
   GROUP BY pizza_name
   ORDER BY total_revenue DESC
   LIMIT 3;
   ```

## Advanced Analysis

### Objectives

1. **Percentage contribution of each pizza type to total revenue.**
2. **Cumulative revenue generated over time.**
3. **Top 3 most ordered pizza types based on revenue for each pizza category.**

### SQL Queries

1. **Percentage Contribution of Each Pizza Type to Total Revenue:**
   ```sql
   SELECT pizza_name, 
          (SUM(price * quantity) / (SELECT SUM(price * quantity) FROM order_details)) * 100 AS revenue_percentage
   FROM order_details
   GROUP BY pizza_name;
   ```

2. **Cumulative Revenue Over Time:**
   ```sql
   SELECT order_date, 
          SUM(price * quantity) OVER (ORDER BY order_date) AS cumulative_revenue
   FROM orders
   JOIN order_details ON orders.order_id = order_details.order_id;
   ```

3. **Top 3 Most Ordered Pizza Types by Revenue for Each Category:**
   ```sql
   SELECT category, pizza_name, SUM(price * quantity) AS total_revenue
   FROM order_details
   JOIN pizzas ON order_details.pizza_id = pizzas.pizza_id
   GROUP BY category, pizza_name
   ORDER BY category, total_revenue DESC
   LIMIT 3;
   ```

## Conclusion

This project demonstrates the use of SQL for data analysis in a business context, providing insights into pizza sales performance and customer ordering patterns. The structured approach from basic to advanced analysis allows us to extract meaningful information that can drive business decisions and strategy.

## Repository Structure

- **/queries**: Contains all the SQL query files.
- **/data**: Placeholder for raw data files.
- **/results**: Contains results from SQL queries.
- **README.md**: Project documentation.

---

If you found this project helpful, please give it a star and follow the repository for more data analysis projects!

Happy querying!

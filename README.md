# Retail Sales Analysis SQL Project

## Project Overview

**Project Title**: Retail Sales Analysis  
**Level**: Beginner  
**Database**: `YourDatabaseName`

This project is my attempt to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data.The project involves setting up a retail sales database, performing data preprocessing and data analysis.

## Objectives

1. **Set up a retail sales database**: Create and populate a retail sales database with the provided sales data.
2. **Data Cleaning**: Identify and remove any records with missing or null values.
3. **Exploratory Data Analysis (EDA)**: Perform basic exploratory data analysis to understand the dataset.
4. **Business Analysis**: Use SQL to derive insights from the sales data.

## Project Structure

### 1. Database Setup

- **Database Creation**: The project starts by creating a database named `YourDatabaseName`.
- **Table Creation**: A table named `retail_sales` is created to store the sales data. The table structure includes columns for transaction ID, sale date, sale time, customer ID, gender, age, product category, quantity sold, price per unit, cost of goods sold (COGS), and total sale amount.

```sql
CREATE DATABASE YourDatabaseName;

CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,
    customer_id INT,	
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,	
    cogs FLOAT,
    total_sale FLOAT
);
```

### 2. Data Exploration & Cleaning

- **Record Count**: Determine the total number of records in the dataset.
- **Customer Count**: Find out how many unique customers are in the dataset.
- **Category Count**: Identify all unique product categories in the dataset.
- **Null Value Check**: Check for any null values in the dataset and delete records with missing data.
- **Duplicate Check**: Check for any duplicate values in the dataset and delete records with missing data.

```sql
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;


SELECT * FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;


SELECT transactions_id,COUNT(*) 
	FROM retail_sales
	group by transactions_id
	having count(*)>1
```

### 3. Data Analysis & Findings

The following SQL queries were developed to derive specific business insights:

1. **Write a SQL query to retrieve total sales**:
```sql
SELECT sum(total_sale)
from retail_sales as TotalSales;
```

2. **Write a SQL query to retrieve sales by year**:
```sql
  SELECT YEAR(sale_date) as Years
	,sum(total_sale) as Sales
	from retail_sales
	group by year(sale_date)
	order by Sales desc
```

3. **Write a SQL query to calculate the total sales for each category.**:
```sql
    SELECT 
    category,
    SUM(total_sale) as net_sale,
    FROM retail_sales
    GROUP BY category
    order by sales desc
```

4. **Write a SQL query to find the total quantity sold.**:
```sql
SELECT sum(quantiy)
from retail_sales as Total_Quan
```

5. **Write a SQL query to find total quantity by year.**:
```sql
  SELECT year(sale_date) as Years
	,sum(quantiy) as Quantity
	from retail_sales
	group by year(sale_date)
	order by Quantity desc
```

6. **Write a SQL query to find the total quantity sold by category.**:
```sql
  SELECT category as Category
	,sum(quantiy) as Quantity
	from retail_sales
	group by category
	order by Quantity desc
```

7. **Write a SQL query to find Quantity sold by gender**:
```sql
  SELECT gender
	,sum(quantiy) as Quantity
	from retail_sales
	group by gender
	order by Quantity desc
```

8. **Write a SQL query to find the top 10 customers by quantity **:
```sql
  SELECT top 10 customer_id as Customers
	,sum(quantiy) as Quantity
	from retail_sales
	group by customer_id
	order by Quantity desc
```

9. **Write a SQL query to find the top 10 customers by sales value**:
```sql
  Select top 10 customer_id as Customers
	,sum(total_sale) as Sales
	from retail_sales
	group by customer_id
	order by Sales desc
```

10. **Write a SQL query to find sales by gender**:
```sql
  SELECT  gender
	,sum(total_sale) as Sales
	from retail_sales
	group by gender
	order by Sales desc
```

11. **Write a SQL query to find total cost of sales**:
```sql
  SELECT sum(cogs)
  from retail_sales as Total_Cos
```

12. **Write a SQL query to find gross margin**:
```sql
  SELECT 
	sum(total_sale) - sum(cogs) as Gross_Profit
	from retail_sales
```

13. **Write a SQL query to find gross profit percentage**:
```sql
  SELECT 
	year(sale_date) as Years
	,round((sum(total_sale) - sum(cogs))*1.0/sum(total_sale)*100,2) as Gross_Profit_per
	from retail_sales
	group by year(sale_date)
```

14. **Write a SQL query to find total cost by category**:
```sql
  select year(sale_date) as Years
	,category
	,sum(cogs) as Total_Cogs
	from retail_sales
	group by year(sale_date),category
```

## Findings

- **Customer Demographics**: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
- **Sales Trends**: Monthly analysis shows variations in sales, helping identify peak seasons.
- **Customer Insights**: The analysis identifies the top-spending customers and the most popular product categories.


## Conclusion

The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.


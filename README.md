# sql_Retail_sales_project
This project is designed to demonstrate SQL skills and techniques typically used by data analysts to explore, clean, and analyze retail sales data. The project involves setting up a retail sales database, performing exploratory data analysis (EDA), and answering specific business questions through SQL queries. This project is ideal for those who are starting their journey in data analysis and want to build a solid foundation in SQL.

<h1>Objectives</h1>
<h2>Set up a retail sales database:</h2> <p>Create and populate a retail sales database with the provided sales data.</p>
<h2>Data Cleaning:</h2> <p>Identify and remove any records with missing or null values.</p>
<h2>Exploratory Data Analysis (EDA):</h2><p>Perform basic exploratory data analysis to understand the dataset.</p>
<h2>Business Analysis:</h2><p> Use SQL to answer specific business questions and derive insights from the sales data.</p>

<h1>Project Structure</h1>
<h3>1. Database Setup</h3>
<li>Database Creation: The project starts by creating a database named retail_sales.</li>
<li>Table Creation: i am just importing flat file in our sql server and then perform the required task</li>

<h1>2. Data Exploration & Cleaning</h1>
<p>Record Count: Determine the total number of records in the dataset.</p>
<p>Customer Count: Find out how many unique customers are in the dataset.</p>
<p>Category Count: Identify all unique product categories in the dataset.</p>
<p>Null Value Check: Check for any null values in the dataset and delete records with missing data.</p>

<h1>3. Data Analysis & Findings</h1>
The following SQL queries were developed to answer specific business questions:

Write a SQL query to retrieve all columns for sales made on '2022-11-05:
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than or equal to 4 in the month of Nov-2022:
SELECT *
FROM retail_sales
WHERE category = 'Clothing'
  AND quantity >= 4
  AND MONTH(sale_date) = 11
  AND YEAR(sale_date) = 2022;
Write a SQL query to calculate the total sales (total_sale) for each category.:
SELECT 
    category,
    SUM(total_sale) as net_sale,
    COUNT(*) as total_orders
FROM retail_sales
GROUP BY 1
Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.:
SELECT
    ROUND(AVG(age), 2) as avg_age
FROM retail_sales
WHERE category = 'Beauty'
Write a SQL query to find all transactions where the total_sale is greater than 1000.:
SELECT * FROM retail_sales
WHERE total_sale > 1000
Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.:
SELECT 
    category,
    gender,
    COUNT(*) as total_transaction
FROM retail_sales
GROUP BY 
    category,
    gender
ORDER BY category
Write a SQL query to calculate the average sale for each month. Find out best selling month in each year:
SELECT 
    sales_year,
    sales_month,
    avg_sale
FROM 
(
    SELECT 
        YEAR(sale_date)  AS sales_year,
        MONTH(sale_date) AS sales_month,
        AVG(total_sale)  AS avg_sale,
        RANK() OVER (
            PARTITION BY YEAR(sale_date)
            ORDER BY AVG(total_sale) DESC
        ) AS rnk
    FROM retail_sales
    GROUP BY 
        YEAR(sale_date),
        MONTH(sale_date)
) as t1
WHERE rnk = 1
ORDER BY sales_year;
**Write a SQL query to find the top 5 customers based on the highest total sales **:
SELECT Top 5
    customer_id,
    SUM(total_sale) as total_sales
FROM retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
Write a SQL query to find the number of unique customers who purchased items from each category.:
SELECT 
    category,    
    COUNT(DISTINCT customer_id) as cnt_unique_cs
FROM retail_sales
GROUP BY category
Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17):
;WITH hourly_sale
AS
(
SELECT *,
    CASE
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift
FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) as total_orders    
FROM hourly_sale
GROUP BY shift
<h1>Findings</h1>
Customer Demographics: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
High-Value Transactions: Several transactions had a total sale amount greater than 1000, indicating premium purchases.
Sales Trends: Monthly analysis shows variations in sales, helping identify peak seasons.
Customer Insights: The analysis identifies the top-spending customers and the most popular product categories.
<h2>Reports</h2>
Sales Summary: A detailed report summarizing total sales, customer demographics, and category performance.
Trend Analysis: Insights into sales trends across different months and shifts.
Customer Insights: Reports on top customers and unique customer counts per category.
<h1>Conclusion</h1>
This project serves as a comprehensive introduction to SQL for data analysts, covering database setup, data cleaning, exploratory data analysis, and business-driven SQL queries. The findings from this project can help drive business decisions by understanding sales patterns, customer behavior, and product performance.

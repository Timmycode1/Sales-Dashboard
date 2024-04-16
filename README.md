# Product Sales Analysis


## Project Overview

Welcome to our Sales Analysis Dashboard project! This interactive dashboard provides comprehensive insights into sales performance and customer behavior. Explore Total Sales, Profit, and Quantity metrics with year-on-year comparisons, and delve into sales trends by product subcategory and customer insights by order volume. With flexible filtering options by year, category, subcategory, region, and more, this dashboard empowers users to make informed business decisions and drive growth.

## Data Source

The sales data used in this dashboard is sourced from Sale_data.csv, a comprehensive database capturing sales transactions across multiple regions and product categories. The dataset span from January to December. 

## Tools
- MYSQL: it was used for querying and extracting data from the database. SQL queries were used to retrieve specific subsets of data that was required for the analysis.
- Microsoft Excel: Used for data cleaning and exploration. Excel was useful in performing quick data checks and validating results before importing the data into Tableau for visualization
- Tableau: is was used for designing and building interactive dashboards that was used in thevisualization of the sales data and performance metrics. Tableau's calculated field function was used in calculating the neccessary KPIs and drag-and-drop interface capabilities enabled us to create dynamic charts, graphs, and KPIs.

## Data Cleaning/Preparation


Our dataset includes sales data spanning from January to December, capturing Total Sales, Profit, and Quantity metrics, as well as customer-related metrics such as Total Customers and Total Sales per Customer.

#### Data Cleaning Steps
- **Handling Missing Values:** Removed rows with missing values and imputed missing values for numerical columns using mean or median.
- **Data Type Conversion:** Converted date columns to datetime format and ensured consistency in data types for numerical and categorical variables.
- **Removing Duplicates:** Identified and removed duplicate records from the dataset to maintain data integrity.
- **Standardizing Data Formats:** Standardized product names, region names, and customer categories to ensure consistency.
- **Addressing Outliers:** Identified and handled outliers in the dataset using winsorization technique.
- **Data Transformation:** Aggregated data at monthly intervals and created derived variables for analysis.
- **Handling Data Integrity Issues:** Checked for and resolved inconsistencies between related columns to maintain data integrity.
- **Data Validation:** Cross-referenced data against external sources and performed logic checks to ensure accuracy.

#### Results
The data cleaning process resulted in a clean and structured dataset ready for analysis. Outliers were addressed, missing values were imputed, and data integrity issues were resolved, ensuring the reliability of our analysis.

## Exploratory Data Analysis (EDA) Questions
- How do Total Sales, Total Profit, and Total Quantity vary over time?
- How does performance (Total Sales, Total Profit, Total Quantity) in the current year compare to the previous year?
- Which product subcategories contribute the most to sales and profit?
- How many customers were there each month, and what was their average spending per customer?
- How do customer segments differ in terms of profitability?
- How does sales performance vary by region, state, and city?
- Which regions have the highest sales and profitability?
- What are the top-selling product categories and subcategories?
- Are there any notable trends or patterns in sales and profit by category and subcategory?
- Are there any significant correlations between sales metrics (Total Sales, Total Profit, Total Quantity) and other variables?


## Data Analysis with SQL

This contain SQL code snippets used for data analysis in the sales analysis project.



```sql
-- Extracting sales data for analysis
SELECT *
FROM sales_data
WHERE date BETWEEN '2021-01-01' AND '2021-12-31';

-- Aggregating sales data by month
SELECT MONTH(date) AS month, 
       SUM(total_sales) AS total_sales,
       SUM(total_profit) AS total_profit
FROM sales_data
GROUP BY MONTH(date)
ORDER BY month;

-- Filtering sales data by product category and subcategory
SELECT *
FROM sales_data
WHERE category = 'Furniture' AND subcategory = 'Chairs';

-- Joining sales and customer tables to analyze customer orders
SELECT s.*, c.customer_name
FROM sales_data s
INNER JOIN customers c ON s.customer_id = c.customer_id;

-- Calculating year-on-year growth in total sales
SELECT YEAR(date) AS year, 
       SUM(total_sales) AS total_sales,
       (SUM(total_sales) - LAG(SUM(total_sales), 1) OVER (ORDER BY YEAR(date))) / LAG(SUM(total_sales), 1) OVER (ORDER BY YEAR(date)) AS yoy_growth
FROM sales_data
GROUP BY YEAR(date)
ORDER BY year;

-- Identifying top-selling products by total quantity sold
SELECT product_name, SUM(quantity) AS total_quantity
FROM sales_data
GROUP BY product_name
ORDER BY total_quantity DESC
LIMIT 10;

-- Analyzing customer behavior by counting the number of orders per customer
SELECT customer_id, COUNT(DISTINCT order_id) AS num_orders
FROM sales_data
GROUP BY customer_id
ORDER BY num_orders DESC;

```
## Dashboard
Explore our dynamic sales analysis dashboard:
- [sales-project](https://github.com/Timmycode1/Sales-Dashboard/blob/main/Sales%20Project.twbx)

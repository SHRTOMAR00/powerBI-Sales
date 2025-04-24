# Sales Insights Project Using MySQL
This project involves performing data analysis on sales data using **MySQL**. The analysis includes data extraction, cleaning, transformation, and insights generation using SQL queries.
---
## Project Overview
This project includes:
- Extracting customer and transaction data
- Filtering sales data by location, date, and currency
- Calculating total revenue across different dimensions
- Identifying product performance in specific markets
- Normalizing currency values for consistent analysis
---
## Tools Used
- **MySQL** – Data querying and analysis
- **CSV/Excel** – Source data format
- **Power BI (optional)** – Used only for additional transformation or visualization
---
### Data Analysis Using SQL

1. Show all customer records

    `SELECT * FROM customers;`

1. Show total number of customers

    `SELECT count(*) FROM customers;`

1. Show transactions for Chennai market (market code for chennai is Mark001

    `SELECT * FROM transactions where market_code='Mark001';`

1. Show distrinct product codes that were sold in chennai

    `SELECT distinct product_code FROM transactions where market_code='Mark001';`

1. Show transactions where currency is US dollars

    `SELECT * from transactions where currency="USD"`

1. Show transactions in 2020 join by date table

    `SELECT transactions.*, date.* FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020;`

1. Show total revenue in year 2020,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and transactions.currency="INR\r" or transactions.currency="USD\r";`
	
1. Show total revenue in year 2020, January Month,

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020 and and date.month_name="January" and (transactions.currency="INR\r" or transactions.currency="USD\r");`

1. Show total revenue in year 2020 in Chennai

    `SELECT SUM(transactions.sales_amount) FROM transactions INNER JOIN date ON transactions.order_date=date.date where date.year=2020
and transactions.market_code="Mark001";`


Data Analysis Using Power BI
============================

1. Formula to create norm_amount column

`= Table.AddColumn(#"Filtered Rows", "norm_amount", each if [currency] = "USD" or [currency] ="USD#(cr)" then [sales_amount]*75 else [sales_amount], type any)`

1. Filters and Logic Summary
   Location Filter: market_code = 'Mark001' (Chennai market)

	•	Currency Filter: Only include INR and USD currencies

	•	Time Filters:

	◦	Year filter: date.year = 2020

	◦	Month filter: date.month_name = 'January'

	•	Product Filter: DISTINCT product_code to remove duplicates 

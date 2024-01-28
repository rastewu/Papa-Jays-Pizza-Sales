# Papa-Jays-Pizza-Sales

### Project Overview
This project is based on a comprehensive dataset, encapsulated in four CSV files, which details a full year of sales activity for a pizza outlet named Papa Jays Pizza, located in Baltimore County, Maryland. The primary objective of this analysis is to derive actionable insights that will aid in strategic decision-making to augment sales and enhance business operations.
The analysis was conducted using Microsoft SQL Server, ensuring robust data management and manipulation. The data is meticulously organized into four distinct tables. Throughout this project, a variety of SQL techniques were employed, including the implementation of elementary joins and sub-queries. The findings and visualizations are presented through Power BI, offering an intuitive and interactive representation of key metrics and trends relevant to the pizza outlet’s performance.
---

### Data Visualization
Data visualization was performed using Microsoft Power BI.


### Data Sources
This analysis comprises of 4 .csv datasets related to Pizza Sales
- Order_details.csv, Ordes.csv, Pizza_types.csv & Pizzas.csv
[Link to Dataset]( https://www.kaggle.com/datasets/mysarahmadbhat/pizza-place-sales)

### Tools
•	Microsoft SQL Server 2022: Utilized for its advanced data management capabilities, SQL Server was the primary tool for storing, querying, and manipulating the dataset. Its robust environment enabled efficient handling of complex queries and data operations.
•	Power BI: This powerful business analytics tool was employed to create dynamic and interactive visualizations. Power BI facilitated the transformation of raw data into meaningful insights, presented through a range of visual formats such as charts, graphs, and dashboards. This enhanced the interpretability and accessibility of the analysis results.
•	CSV Files: The raw dataset was provided in the form of four CSV files. These files were the foundational elements of the project, containing a year's worth of sales data for the pizza outlet. 


### Data Cleaning/Preparation
The following tasks were performed during the initial data preparation phase using SQL Server
•	Order_Details Table:
	- Changed the data types for order_details_id, order_id & quantity fields to integer.
  - Set primary key on order_details_id
•	Orders Table:
  - Changed the data types for order_id fields to integer.
  - Set primary key on order_id.
• Pizza_types Table:
  - Changed the data types for Pizza_type_id field to integer.
  - Set primary key on Pizza_type_id.
•	Pizzas Table:
  - Set primary key on Pizza_id.


### Exploratory Data Analysis
Preceding the EDA process, let’s explore our tables in the Pizza_Sales database using the following SQL commands:

```sql
USE Pizza_Sales  --connects to the Pizza_Sales Database

select *
from Pizza_Sales..order_details  --Views the entire content of the order_details table

select *
from Pizza_Sales..orders

select *
from Pizza_Sales..pizza_types

select *
from Pizza_Sales..pizzas
```

- KPIs
1.	Total Revenue (How much money did we make this year?)
2.	Average Order Value
3.	Total Pizzas Sold
4.	Total Orders
5.	Average Pizzas per Order

QUESTIONS TO ANSWER
1.	Daily Trends for Total Orders
2.	Hourly Trend for Total Orders
3.	Percentage of Sales by Pizza Category
4.	Percentage of Sales by Pizza Size
5.	Total Pizzas Sold by Pizza Category
6.	Top 5 Best Sellers by Total Pizzas Sold
7.	Bottom 5 Worst Sellers by Total Pizzas Sold

 ### Queries Used 
### KPIs
 ```sql
--1) Total Revenue (How much money did we make this year?)
SELECT round(SUM(Quantity*Price),2) AS TotalRevenue
FROM Pizza_Sales..order_details od
JOIN Pizza_Sales..pizzas p
ON od.pizza_id=p.pizza_id
 

--2)Avera ge Order Value
--total order value/order count
SELECT round(SUM(quantity*price)/COUNT(DISTINCT od.order_id),2) AS [Average Order Value]
FROM Pizza_Sales..order_details od
JOIN Pizza_Sales..pizzas p
ON od.pizza_id=p.pizza_id

--3) Total Pizzas Sold
SELECT SUM(Quantity) AS [Total Pizzas Sold]
FROM Pizza_Sales..order_details

--4)	Total Orders
SELECT COUNT(DISTINCT Order_Id) AS [Total Orders]
FROM Pizza_Sales..orders

--5) Average Pizzas per Order
--pizzas sold/number of pizzas
SELECT SUM(Quantity)/COUNT(DISTINCT order_id) AS [Average Pizzas Per Order]
FROM Pizza_Sales..order_details


--QUESTIONS TO ANSWER
--1) Daily Trends for Total Orders
--select * from Pizza_Sales..orders
SELECT FORMAT(date, 'ddd') AS DayOfWeek, COUNT(DISTINCT order_id) AS  Total_Orders 
FROM Pizza_Sales..orders
GROUP BY FORMAT(date, 'ddd')
ORDER BY Total_Orders DESC
 

--2) Hourly Trend for Total Orders
--Select * from Pizza_Sales..orders
SELECT DATEPART(HOUR,time) AS [Hour], COUNT(DISTINCT order_id) AS CountOfOrders
FROM Pizza_Sales..orders
GROUP BY DATEPART(HOUR,time)
ORDER BY [Hour]  

--3) Percentage of Sales by Pizza Category
--a: calculate total revenue by Category
--% of Sales as (a:/total revenue)*100

SELECT
	category,
	SUM(quantity*Price) AS Revenue,
	ROUND((SUM(quantity*Price)*100/(
		SELECT SUM(quantity*Price) 
		FROM order_details od
		JOIN pizzas p ON od.pizza_id=p.pizza_id)
	),2) AS PercentageOfSales
FROM order_details od
JOIN pizzas p ON od.pizza_id=p.pizza_id
JOIN pizza_types pt ON p.pizza_type_id=pt.pizza_type_id
GROUP BY category
ORDER BY PercentageOfSales DESC

--4)	Percentage of Sales by Pizza Size
SELECT 
	size
	,ROUND(SUM(od.quantity*p.price),2) AS Sales
	,ROUND(SUM(od.quantity*p.price)*100/(SELECT SUM(quantity*price)  
	 FROM order_details od
	JOIN pizzas p ON od.pizza_id=p.pizza_id),2) as PercentageOfSalesByPizzaSize
	 FROM order_details od
	 JOIN pizzas p ON od.pizza_id=p.pizza_id  
	 GROUP BY size
	 ORDER BY Sales DESC

--5) Total Pizzas Sold by Pizza Category
SELECT 
	category
	,SUM(quantity) TotalPizzasSold 
FROM order_details od
JOIN pizzas p ON od.pizza_id=p.pizza_id
JOIN pizza_types pt ON p.pizza_type_id=pt.pizza_type_id
GROUP BY category
ORDER BY TotalPizzasSold DESC


--6) Top 5 Best Sellers by Total Pizzas Sold
SELECT TOP 5
	name
	,SUM(quantity) TotalPizzasSold 
FROM order_details od
JOIN pizzas p ON od.pizza_id=p.pizza_id
JOIN pizza_types pt ON p.pizza_type_id=pt.pizza_type_id
GROUP BY name
ORDER BY TotalPizzasSold DESC


--7) Bottom 5 Worst Sellers by Total Pizzas Sold
SELECT TOP 5
	name
	,SUM(quantity) TotalPizzasSold 
FROM order_details od
JOIN pizzas p ON od.pizza_id=p.pizza_id
JOIN pizza_types pt ON p.pizza_type_id=pt.pizza_type_id
GROUP BY name
ORDER BY TotalPizzasSold ASC


		
```

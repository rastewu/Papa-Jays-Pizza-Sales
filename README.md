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

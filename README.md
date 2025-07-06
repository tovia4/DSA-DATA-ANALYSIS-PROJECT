### MY PROJECT DOCUMENTATION.
I started my data analysis jurney class with Incubator Hub, where i learnt very interesting topics ranging 
from MS Excel, Sql and PowerBI.
Kultra Mega Stores Inventory
Project Overview
Kultra Mega Stores specializes in office supplies and furniture, serving a diverse customer base
that includes individual consumers, small retail businesses, and large corporate clients across
three Nigerian states. I was assigned to support the Abuja division. The Business Manager
provided a dataset containing order records from 2009 to 2012 and tasked me with analyzing
the data to extract and present key insights and findings.
Data Source: The dataset was sourced from (Digital Skillup Africa) Incubator Hub
Method and Tools
Data Cleaning: Conducted in Microsoft Excel to eliminate errors, handle missing values, and
ensure the dataset was properly structured for analysis.
Data Exploration: Utilized SQL queries in SQL Server Management Studio (SSMS) to explore
data patterns, distributions, and relationships.
GitHub: Used as a platform to document and showcase the project as part of my professional
portfolio.
Data Analysis
---Which product category had the highest sales?
``` SQL
SELECT Product_Category, 
Count(Order_ID) as Frequency_of_Purchase,
Round(SUM(Sales), 2) AS Hightest_Bought
From KMS_Sql_Case
Group BY Product_Category
Order By Hightest_Bought DESC;
```

--- What are the Top 3 and Bottom 3 regions in terms of sales?
``` SQL
SELECT TOP 3
Region, Round(SUM(Sales), 00) AS TotalSales
From KMS_Sql_Case
Group By Region
Order By TotalSales DESC;

SELECT BOTTOM 3
Region, Round(SUM(Sales), 00) AS TotalSales
From KMS_Sql_Case
Group By Region
Order By TotalSales ASC;
```

---What were the total sales of appliances in Ontario?
``` SQL
SELECT Count(*) as Count_of_sales,
Round(SUM(Sales), 00) 
AS Total_Sales_In_Ontario
FROM  KMS_Sql_Case
WHERE Product_Sub_Category = 'Appliances' 
AND Region = 'Ontario'
Group By Product_Sub_Category,
Region;
```

---Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers?
``` SQL
SELECT TOP 10
Order_ID, Customer_Name, 
SUM(Sales) AS TotalSales
FROM KMS_Sql_Case
Group By Order_ID, Customer_Name
Order By
TotalSales ASC;
```

---KMS incurred the most shipping cost using which shipping method?
``` SQL
SELECT Ship_Mode, Round(SUM(Shipping_Cost), 2) 
AS Total_Shipping_Cost
FROM KMS_Sql_Case
Group By Ship_Mode
Order By Total_Shipping_Cost DESC;
```

--- Who are the most valuable customers, and what products or services do they typically purchase?
``` SQL
SELECT TOP 10
Customer_Name, Count(*) AS Count_of_Purchase,
Product_Sub_Category
FROM KMS_Sql_Case
Group By Customer_Name, Product_Sub_Category
Order By
Count_of_Purchase DESC;
```

--- Which small business customer had the highest sales?
``` SQL
SELECT TOP 10
Customer_Name,
ROUND(SUM(Sales), 2) AS TotalSales
FROM  KMS_Sql_Case
WHERE Customer_Segment = 'Small Business'
Group By Customer_Name
Order By
TotalSales DESC;
```

--- Which Corporate Customer placed the most number of orders in 2009 – 2012?
``` SQL
SELECT TOP 10
Customer_Name, Count(Order_Quantity) AS Count_of_Quantity
From KMS_Sql_Case
WHERE Customer_Segment = 'Corporate' 
AND Order_Date BETWEEN '2009-01-01' AND '2012-12-31'
Group By Customer_Name
Order By Count_of_Quantity DESC;
```

--- Which consumer customer was the most profitable one?
``` SQL
SELECT TOP 10
Customer_Name, SUM(Profit) AS Total_Profit
FROM KMS_Sql_Case
WHERE Customer_Segment = 'Consumer' 
Group By Customer_Name
Order By Total_Profit DESC;
```

--- Which customer returned items, and what segment do they belong to?
``` SQL
SELECT Customer_Name, Customer_Segment, 
SUM(Order_Quantity) AS Total_Quantity
FROM KMS_Sql_Case
Group By Customer_Name, Customer_Segment
HAVING SUM(Order_Quantity) < 0
Order By Total_Quantity DESC;
```

--- If the delivery truck is the most economical but the slowest shipping method and
--Express Air is the fastest but the most expensive one, do you think the company
--appropriately spent shipping costs based on the Order Priority? Explain your answer
```SQL
SELECT Order_Priority,
Ship_Mode,
COUNT(*) AS Num_Orders,
ROUND(SUM(Sales), 00) AS Total_Sales,
ROUND(SUM(Profit), 00) AS Total_Profit
FROM KMS_Sql_Case
GROUP BY Order_Priority, Ship_Mode
ORDER BY Order_Priority, Ship_Mode;
```

Explaination:
The company did not appropriately spend shipping costs based on Order Priority.
-- Express Air, the most expensive shipping mode, was used for small and Not Specified priority orders, 
--which conflicting cost-efficiency principles. Delivery Truck, the slowest method, was occasionally used for High or Critical orders.
-- The company did not always match shipping cost with urgency, suggesting potential inefficiencies in logistics planning.


CONCLUSION :
This project reveals that Technology and Office Supplies are Kultra Mega Stores’
highest-performing product categories. The Corporate and Consumer segments contribute the
most to revenue, highlighting an opportunity for targeted strategies to drive additional sales.
Instances of negative profit suggest potential product returns, signaling the need to enhance
customer satisfaction. By focusing on best-selling products, high-value customer segments, and
minimizing returns, Kultra Mega Stores can significantly improve overall business performance.

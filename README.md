# KULTRA-MEGA-STORE-(KMS)
## DSA Capstone Project

##### --Create database
### CREATE DATABASE KMS_SQLData [Download here](https://www.linkedin.com/in/terungwa-emmanuel-455a66245)

##### -- use database
### USE KMS_SQLData

##### -- Import table
##### -- KMSSQLData.csv

##### -- retrieve table
### SELECT *
#### FROM KMSSQLData

### -- Question 1
##### -- top product category with the highest sales
### SELECT TOP 1 [Product_Category],
### SUM([Sales]) AS TotalSales
### FROM
#### KMSSQLData
### GROUP BY
#### [Product_Category]
### ORDER BY
#### TotalSales DESC;

##### -- Question 2
##### -- Top 3 and bottom 3 regions in terms of sales
##### -- Top 3 regions by sales
### SELECT TOP 3
    [Region],
### SUM([Sales]) AS TotalSales
### FROM
    KMSSQLData
### GROUP BY
    [Region]
### ORDER BY
    TotalSales DESC;

##### -- Bottom 3 regions by sales
### SELECT TOP 3
    [Region],
    SUM([Sales]) AS TotalSales
### FROM
    KMSSQLData
### GROUP BY
    [Region]
### ORDER BY
    TotalSales ASC;

##### -- Question 3
##### -- total sales of appliances in Ontario
### SELECT
### SUM([Sales]) AS TotalApplianceSales_Ontario
### FROM
    KMSSQLData
### WHERE
    [Product_Sub_Category] = 'Appliances'
### AND [Province] = 'Ontario';

##### -- Question 4
##### -- Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers
##### -- Bottom 10
### SELECT TOP 10
    [Customer_Name],
### SUM([Sales]) AS TotalSales
### FROM   KMSSQLData
### GROUP BY    [Customer_Name]
### ORDER BY     TotalSales ASC;

##### -- Question 5
##### -- KMS incured the most shipping cost using which shipping method
##### -- top shipping method
### SELECT TOP 1
    [Ship_Mode],
    SUM([Shipping_Cost]) AS TotalShippingCost
### FROM
    KMSSQLData
### GROUP BY
    [Ship_Mode]
### ORDER BY
    TotalShippingCost DESC;

##### -- CASE SCENARIO II
##### -- Question 6
##### -- most valuable customers, and what products or services do they typically purchase
##### -- top 10 most valuable customers
##### -- Top 10 Valuable Customers by Total Sales
SELECT TOP 10
    [Customer_Name],
    SUM(Sales) AS TotalSales,
    SUM(Profit) AS TotalProfit
### FROM KMSSQLData
### GROUP BY [Customer_Name]
### ORDER BY TotalSales DESC;

##### -- customers names, product and services.
### SELECT TOP 10
    [Customer_Name],
    [Product_Category],
	[Product_Sub_Category],
### SUM([Sales]) AS  TotalSales,
### SUM([Profit]) AS  TotalProfit
### FROM   KMSSQLData
### WHERE
    [Customer_Name] IN (
### SELECT TOP 10   [Customer_Name]
### FROM   KMSSQLData
### GROUP BY    [Customer_Name]
### ORDER BY  SUM([Sales]) DESC
    )
### GROUP BY
    [Customer_Name], [Product_Category], [Product_Sub_Category]
### ORDER BY
    [Customer_Name], TotalSales DESC;

##### -- Question 7
##### -- small business customer that had the highest sales
### SELECT TOP 1
    [Customer_Name],
### SUM([Sales]) AS TotalSales
### FROM
    KMSSQLData
### WHERE
    [Customer_Segment] = 'Small Business'
### GROUP BY
    [Customer_Name]
### ORDER BY
    TotalSales DESC;

##### -- Question 8
##### -- Corporate Customer that placed the most number of orders in 2009-2012
### SELECT TOP 1
    [Customer_Name],
    COUNT(DISTINCT [Order_ID]) AS TotalOrders
### FROM
    KMSSQLData
### WHERE
    [Customer_Segment] = 'Corporate'
### AND TRY_CAST([Order_Date] AS DATE) BETWEEN '2009-01-01' AND '2012-12-31'
### GROUP BY
    [Customer_Name]
### ORDER BY
    TotalOrders DESC;

##### -- Question 9
##### -- Consumer customer that was the most profitable 
### SELECT TOP 1
    [Customer_Name],
### SUM([Profit]) AS TotalProfit
### FROM
    KMSSQLData
### WHERE
    [Customer_Segment] = 'Consumer'
### GROUP BY
    [Customer_Name]
### ORDER BY
    TotalProfit DESC;

##### -- Question 10
##### -- customer returned items, and what segment do they belong
##### -- customer with low profit or loss which indicate returns
### SELECT DISTINCT
    [Customer_Name],
    [Customer_Segment],
    SUM([Profit]) AS TotalProfit
### FROM
    KMSSQLData
### GROUP BY
    [Customer_Name], [Customer_Segment]
### HAVING SUM([Profit]) < 0
### ORDER BY TotalProfit;

##### -- Question 11, Analysis of result
##### -- High/Critical Priority orders use faster methods, even if costly
##### -- Low Priority orders use economical shipping, saving cost
### SELECT
    [Order_Priority],
    [Ship_Mode],
### COUNT(*) AS TotalOrders,
### SUM([Shipping_Cost]) AS TotalShippingCost,
### AVG([Shipping_Cost]) AS AvgShippingCost
### FROM
    KMSSQLData
### GROUP BY
    [Order_Priority], [Ship_Mode]
### ORDER BY
    [Order_Priority], [Ship_Mode];

# KULTRA-MEGA-STORE-(KMS)
## DSA Capstone Project [Download here](https://github.com/EMMA-max-bit/KULTRA-MEGA-STORE-KMS-/blob/main/DSA_KMS%20Capstone-Project%20Report.pdf)

##### --Create database
### CREATE DATABASE KMS_SQLData [Download here](https://github.com/EMMA-max-bit/KULTRA-MEGA-STORE-KMS-/blob/main/SQLqueryKMS_DSA_Project.sql)

##### -- use database
USE KMS_SQLData

##### -- Import table
##### -- KMSSQLData.csv

##### -- retrieve table
SELECT *
FROM KMSSQLData

### -- Question 1
##### -- top product category with the highest sales
SELECT TOP 1 [Product_Category],

SUM([Sales]) AS TotalSales

FROM

KMSSQLData

GROUP BY

[Product_Category]

ORDER BY

TotalSales DESC; [Download here](https://github.com/EMMA-max-bit/KULTRA-MEGA-STORE-KMS-/blob/main/ANSWER%20TO%20Q1.gif)

##### -- Question 2
##### -- Top 3 and bottom 3 regions in terms of sales
##### -- Top 3 regions by sales
SELECT TOP 3

   [Region],
   
SUM([Sales]) AS TotalSales

   FROM
   
KMSSQLData

GROUP BY

    [Region]
    
ORDER BY
TotalSales DESC; [Download here](https://github.com/EMMA-max-bit/KULTRA-MEGA-STORE-KMS-/blob/main/ANSWER%20TO%20Q2.gif)

##### -- Bottom 3 regions by sales
SELECT TOP 3

    [Region],
    
    SUM([Sales]) AS TotalSales
    
FROM

    KMSSQLData
    
GROUP BY

    [Region]
    
ORDER BY

    TotalSales ASC;

##### -- Question 3
##### -- total sales of appliances in Ontario

SELECT

SUM([Sales]) AS

    TotalApplianceSales_Ontario
    
FROM
    KMSSQLData
    
WHERE
    [Product_Sub_Category] = 'Appliances'
    
AND [Province] = 'Ontario'; [Download](https://github.com/EMMA-max-bit/KULTRA-MEGA-STORE-KMS-/blob/main/ANSWER%20TO%20Q3.gif)

##### -- Question 4
##### -- Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers
##### -- Bottom 10

SELECT TOP 10

    [Customer_Name],
    
SUM([Sales]) AS

	TotalSales
 
FROM   KMSSQLData

GROUP BY   
	[Customer_Name]
 
ORDER BY     
	TotalSales ASC; [Download here](https://github.com/EMMA-max-bit/KULTRA-MEGA-STORE-KMS-/blob/main/ANSWER%20TO%20Q4.gif)
 

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
    
FROM 
	KMSSQLData
 
GROUP BY 
	[Customer_Name]
 
ORDER BY 
	TotalSales DESC;

##### -- customers names, product and services.

SELECT TOP 10
    [Customer_Name],
    
    [Product_Category],
    
    [Product_Sub_Category],
    
SUM([Sales]) 
AS
TotalSales,
 
SUM([Profit])

AS  
TotalProfit
 
 FROM   
	KMSSQLData
 
WHERE
    	[Customer_Name] IN (
     
SELECT TOP 10   
	[Customer_Name]
FROM   
	KMSSQLData
 
GROUP BY    
	[Customer_Name]
 
ORDER BY

SUM([Sales]) DESC

    )
    
GROUP BY

    [Customer_Name], [Product_Category], [Product_Sub_Category]
    
ORDER BY
    [Customer_Name], TotalSales DESC;
    [Download here](https://github.com/EMMA-max-bit/KULTRA-MEGA-STORE-KMS-/blob/main/ANSWER%20TO%20Q6.gif)

##### -- Question 7
##### -- small business customer that had the highest sales
#### SELECT TOP 1
    [Customer_Name],
#### SUM([Sales]) AS 
	TotalSales
#### FROM
       KMSSQLData
#### WHERE
    [Customer_Segment] = 'Small Business'
#### GROUP BY
    [Customer_Name]
#### ORDER BY
    TotalSales DESC;

##### -- Question 8
##### -- Corporate Customer that placed the most number of orders in 2009-2012
#### SELECT TOP 1
    [Customer_Name],
    COUNT(DISTINCT [Order_ID]) AS TotalOrders
#### FROM
    KMSSQLData
#### WHERE
    [Customer_Segment] = 'Corporate'
#### AND TRY_CAST([Order_Date] AS DATE) 
#### BETWEEN     '2009-01-01' AND '2012-12-31'
#### GROUP BY
    [Customer_Name]
#### ORDER BY
    TotalOrders DESC;

##### -- Question 9
##### -- Consumer customer that was the most profitable 
#### SELECT TOP 1
    [Customer_Name],
#### SUM([Profit]) AS TotalProfit
#### FROM
    KMSSQLData
#### WHERE
    [Customer_Segment] = 'Consumer'
#### GROUP BY
    [Customer_Name]
#### ORDER BY
    TotalProfit DESC;

##### -- Question 10
##### -- customer returned items, and what segment do they belong
##### -- customer with low profit or loss which indicate returns

SELECT DISTINCT
    [Customer_Name],
    [Customer_Segment],
    SUM([Profit]) AS TotalProfit
    
FROM
    KMSSQLData
    
GROUP BY
    [Customer_Name], [Customer_Segment]
    
HAVING SUM([Profit]) < 0

ORDER BY TotalProfit; [Download here](https://github.com/EMMA-max-bit/KULTRA-MEGA-STORE-KMS-/blob/main/ANSWER%20Q10.pdf)

##### -- Question 11, Analysis of result

##### -- High/Critical Priority orders use faster methods, even if costly
##### -- Low Priority orders use economical shipping, saving cost

SELECT
    [Order_Priority],
    [Ship_Mode],
    
COUNT(*) AS TotalOrders,

SUM([Shipping_Cost]) AS TotalShippingCost,

AVG([Shipping_Cost]) AS AvgShippingCost

FROM
    KMSSQLData
    
GROUP BY
    [Order_Priority], [Ship_Mode]
    
ORDER BY
    [Order_Priority], [Ship_Mode]; [Download here](https://github.com/EMMA-max-bit/KULTRA-MEGA-STORE-KMS-/blob/main/ANSWER%20TO%20Q11.gif)


## Executive Summary
This report presents a comprehensive analysis of the provided KMS sales data, addressing key business questions and offering actionable insights to optimize sales strategies, improve customer profitability, and enhance operational efficiency. The analysis covers various aspects of the business, including product performance, regional sales, customer segmentation, and shipping logistics. By leveraging the insights derived from this data, KMS can make informed decisions to drive revenue growth and strengthen customer relationships.

## Introduction
In today's competitive business landscape, data-driven decision-making is paramount for sustained growth and success. This capstone project aims to analyze the sales data of KMS to identify trends, patterns, and opportunities that can inform strategic business initiatives. The dataset includes detailed information on orders, products, customers, and shipping, providing a rich foundation for in-depth analysis. The primary objective is to answer specific business questions posed by KMS management, thereby providing a clear roadmap for enhancing overall business performance.

## Dataset Overview
The dataset used for this analysis, Kultra Mega Stores (KMS) - KMSSQLData.csv, contains a wide array of sales-related information from 2009 to 2012, Key columns include:
##### Row ID: Unique identifier for each record.
##### Order ID: Identifier for each order.
##### Order Date: Date when the order was placed.
##### Order Priority: Priority level of the order (e.g., Low, Medium, High, Critical, Not Specified).
##### Order Quantity: Number of units ordered.
##### Sales: Total sales amount for the order.
##### Discount: Discount applied to the order.
##### Ship Mode: Method of shipping (e.g., Regular Air, Express Air, Delivery Truck).
##### Profit: Profit generated from the order.
##### Unit Price: Price per unit of the product.
##### Shipping Cost: Cost incurred for shipping the order.
##### Customer Name: Name of the customer.
##### Province: Province where the customer is located.
##### Region: Geographical region of the customer.
##### Customer Segment: Segment to which the customer belongs (e.g., Small Business, Consumer, Corporate, Home Office).
##### Product Category: Broad category of the product.
##### Product Sub-Category: Specific sub-category of the product.
##### Product Name: Name of the product.
##### Product Container: Type of container used for the product.
##### Product Base Margin: Base margin of the product.
##### Ship Date: Date when the order was shipped.
##### This dataset provides a comprehensive view of KMS's sales operations, enabling a detailed examination of various business facets.

##  Analysis and Findings
This section presents the findings from the data analysis, addressing each of the business questions outlined in the project scope. The analysis was performed using the business analytical tool SQL SERVER.

# Question 1
## 1 Top Product Category by Sales

Identifying the top-performing product categories is crucial for strategic inventory management and marketing efforts. The analysis reveals the following:
Finding: The top product category with the highest sales is Technology.
Below is the SQL query for the analysis [Download here]()

## 2 Regional Sales Performance

Understanding regional sales performance helps in allocating resources effectively and tailoring marketing strategies to specific geographical areas. The analysis identified the top 3 and bottom 3 regions in terms of sales:
The analyis reviews the top 3 Regions by Sales are West ($3 597 549.2755), Ontario ($3 063 212.4795) and Prarie ($2 837 304.6015)

##### Bottom 3 Regions by Sales are Nunavut ($116 376.4835). Northwest Territories ($800 847.3295) and Yukon ($975 867.371)
These findings highlight significant disparities in sales performance across regions. The West, Ontario, and Prarie regions are strongholds for KMS, while the Northern territories (Yukon, Northwest Territories, Nunavut) represent areas with lower sales. This suggests a need for targeted strategies to boost sales in underperforming regions, potentially through localized marketing campaigns or adjustments to product offerings.

## 3. Total Sales of Appliances in Ontario

A specific inquiry was made regarding the sales performance of appliances in the province of Ontario. The finding shows that the total sales of appliances in Ontario is $202 346.84
This specific data point can be used for regional sales targets and inventory planning for appliance products within Ontario.

## 4. Bottom 10 Customers by Sales and Revenue Enhancement Strategies
Understanding the lowest-contributing customers is vital for developing strategies to improve their engagement and spending. The analysis identified the bottom 10 customers by sales:

##### The analysis find the bottom 10 customers by sales as follows:
#### Jeremy Farry		$85.72
#### Natalie Decherney		$125.90
#### Nicole Fjeld		$153.03
#### Katrina Edelman		$180.76
#### Dorothy Dickinson		$198.08
#### Christine Kargatis		$293.22
#### Eric Murdock		$343.328
#### Chris Mcafee		$350.18
#### Rick Huthwaite		$415.82
#### Mark Hamilton		$450.99

## 5. Most Costly Shipping Method

##### Optimizing shipping costs is essential for improving profit margins. The analysis identified the shipping method with the highest incurred cost:
The shipping method with the most shipping cost is Delivery Truck ($51 971.939)
This finding is significant because while Delivery Truck might be a frequently used option, its cumulative cost is the highest. KMS should investigate the volume of shipments via Delivery by Truck and explore opportunities for cost reduction, such as negotiating better rates with carriers, optimizing package sizes, or encouraging customers to choose more economical shipping options when order priority allows.

## 6. Most Valuable Customers and Their Product Preferences

Identifying and understanding the most valuable customers is key to nurturing long-term relationships and maximizing lifetime value. The analysis identified the top 10 most valuable customers by sales and the products they typically purchase which are found in the pdf above.

## 7. Small Business Customer with Highest Sales

Focusing on specific customer segments can reveal unique opportunities. The analysis identified the small business customer with the highest sales:
The analysis finding shows that the small business customer with the highest sales is Dennis Kane with sales of $75 967.5905. He represents a highly successful small business client for KMS.

## 8. Corporate Customer with Most Orders (2009-2012)

Analyzing order frequency within specific segments and timeframes provides insights into consistent engagement. The analysis identified the corporate customer who placed the most orders between 2009 and 2012:

The analysis finds out that corporate customer who placed the most orders between 2009 and 2012 is Adam Hart with 18 orders.
Adam Hart's consistent ordering behavior indicates a strong and reliable corporate relationship. KMS should ensure continued satisfaction for this customer and explore opportunities for expanding their business, potentially through upselling or cross-selling additional services or products relevant to corporate needs.

## 9. Most Profitable Consumer Customer

Profitability is a key metric for evaluating customer value in any business. The analysis identified the consumer customer who was the most profitable. Emily Phan with a profit of $34 005.44 and Emily Phan represents an ideal consumer customer for KMS. Understanding her purchasing habits, product preferences, and engagement patterns can help KMS identify and target similar high-profit consumer segments.

## 10. Customers with Low Profit or Loss (Indicating Returns)
 Identifying customers associated with low or negative profit margins can indicate issues such as frequent returns or high service costs. The analysis identified customers with low profit or loss:
The analysis finding reviews that there are 308 customers with low or negative profit, potentially indicating returns or high service costs. Some examples include:

#### Julia West (Home Office):		 -$13 057.20
#### Laurel Workman (Home Office):	 -$12 587.05

## 11 Shipping Cost Analysis by Order Priority and Ship Mode

An in-depth analysis of shipping costs based on order priority and shipping mode provides critical insights for logistics optimization.
The analysis of shipping costs by order priority and ship mode reveals the following findings [Download here]()

## Recommendations from the findings;

#### 1.Negotiate with Carriers: Given the high volume of Regular Air shipments, KMS should negotiate better rates with its carriers for this shipping mode.
#### 2.Optimize Shipping Choices: For low and medium priority orders, KMS managements should explore if customers can be incentivized to choose slightly slower but more cost-effective shipping options, or if there are opportunities to consolidate shipments.
#### 3.Analyze Item Characteristics: Investigate the types of products typically shipped via Delivery Truck to understand if alternative shipping methods or packaging could reduce costs for certain items.
#### 4.Dynamic Shipping Options: KMS should implement a system that dynamically suggests the most cost-effective shipping option to customers based on order priority, product size/weight, and delivery timeframe.

## Conclusion.

This capstone project has provided valuable insights into KMS's sales data, addressing key business questions and offering actionable recommendations. The analysis highlighted the dominance of technology products, regional sales disparities, opportunities to re-engage low-value customers, and areas for shipping cost optimization. By implementing the suggested strategies, KMS can enhance its sales performance, improve customer relationships, and increase profitability.


























    

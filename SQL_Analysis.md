###### **Total Revenue**



SELECT SUM(Amount) AS Revenue

FROM retail\_store\_sales;



###### **Category Performance - Highest to Lowest**



SELECT category,

SUM(Amount) AS total\_revenue

FROM retail\_store\_sales

GROUP BY Category

ORDER BY total\_revenue DESC;



###### **Top 10 Purchased Items**



SELECT ItemPurchased,

Sum(Amount) AS TotalRevenue

FROM retail\_store\_sales

GROUP BY ItemPurchased

ORDER BY TotalRevenue DESC

LIMIT 10;



###### **Customer demographics and Avg.spending**



SELECT Gender,

COUNT(CustomerID) AS Count,

AVG(Amount) AS AverageSpending

FROM retail\_store\_sales

GROUP BY Gender;



###### **Payment Method Analysis**



SELECT PaymentMethod,

COUNT(CustomerID) AS Count

FROM retail\_store\_sales

GROUP BY PaymentMethod;



###### **Discount Effectiveness**



SELECT Discount\_Band,

AVG(Amount) AS AverageSpend

FROM retail\_store\_sales

GROUP BY Discount\_Band;



###### **Customer Loyalty Analysis**



SELECT

&#x20;   CASE

&#x09;WHEN PreviousPurchases < 3 THEN 'New'

&#x09;WHEN PreviousPurchases BETWEEN 3 AND 6 THEN 'Regular'

&#x09;ELSE 'Loyal'

&#x20;   END AS Customer\_Type,

&#x20;   AVG(Amount) AS Average\_Spending

FROM retail\_store\_sales

GROUP BY

&#x20;   CASE

&#x09;WHEN PreviousPurchases < 3 THEN 'New'

&#x09;WHEN PreviousPurchases BETWEEN 3 AND 6 THEN 'Regular'

&#x09;ELSE 'Loyal'

&#x20;   END

ORDER BY Average\_Spending DESC;



###### **Spending Category Analysis**



SELECT

&#x20;   CASE

&#x09;WHEN Amount <= 50 THEN 'Low'

&#x09;WHEN Amount BETWEEN 51 AND 250 THEN 'Medium'

&#x09;ELSE 'High'

&#x20;   END AS Spending\_Category,

&#x20;   COUNT(CustomerID) AS CustomerCount

FROM retail\_store\_sales

GROUP BY

&#x20;   CASE

&#x09;WHEN Amount <= 50 THEN 'Low'

&#x09;WHEN Amount BETWEEN 51 AND 250 THEN 'Medium'

&#x09;ELSE 'High'

&#x20;   END;



###### **Product Price Variablility**



SELECT ItemPurchased,

&#x09;MIN(Amount) AS Minimum\_Amount,

&#x09;MAX(Amount) AS Maximum\_Amount,

&#x09;ROUND(MAX(Amount) - MIN(Amount),2) AS Price\_Variation

FROM retail\_store\_sales

GROUP BY ItemPurchased

ORDER BY Price\_Variation DESC;



###### **Highest Rated Categories**



SELECT Category,

Round(Avg(ItemRating),3) AS Average\_Rating

FROM retail\_store\_sales

GROUP BY Category

ORDER BY Average\_Rating DESC;



###### **Age Group Spending Analysis**



SELECT Age\_Band,

Round(Avg(Amount),2) AS Average\_Spending

FROM retail\_store\_sales

GROUP BY Age\_Band;



###### **High Value Customers**



SELECT 

CustomerID, Age, Gender, Amount, Customer\_Type

FROM retail\_store\_sales

WHERE  

Amount > (SELECT Avg(Amount) FROM retail\_store\_sales);



###### **Repeat Purchase Behavior**

**Which category has customers with highest previous purchases on average?**



SELECT Category,

Avg(PreviousPurchases) AS Avg\_PreviousPurchase

FROM retail\_store\_sales

GROUP BY Category

ORDER BY Avg\_PreviousPurchase DESC

LIMIT 1;



###### **Revenue Contribution Analysis**



SELECT Category,

&#x09;Round(Sum(Amount),2) AS Revenue,

&#x20;   Round(Sum(Amount) / (SELECT Sum(Amount) FROM retail\_store\_sales) \*100,2) AS Revenue\_Percentage

FROM retail\_store\_sales

GROUP BY Category

ORDER BY Revenue\_Percentage DESC;



###### **Electronics Product Performance**



SELECT ItemPurchased,

&#x09;Round(Sum(Amount),2) AS Revenue,

&#x20;   Round(Sum(Amount) / (SELECT Sum(Amount) FROM retail\_store\_sales WHERE Category='Electronics') \*100,2) AS Revenue\_Percentage

FROM retail\_store\_sales

WHERE Category='Electronics'

GROUP BY ItemPurchased

ORDER BY Revenue\_Percentage DESC;






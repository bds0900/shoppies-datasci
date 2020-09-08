# Winter 2021 Data Science Intern Challenge 

Please complete the following questions, and provide your thought process/work. You can attach your work in a text file, link, etc. on the application page. Please ensure answers are easily visible for reviewers!


#### Question 1: Given some sample data, write a program to answer the following: [click here to access the required data set](https://docs.google.com/spreadsheets/d/16i38oonuX1y1g7C_UAmiK9GkY7cS-64DfiDMNiR41LM/edit#gid=0)

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

###### a.	Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 
- I guess the calculation concluded above is sum of order amount/ the last order id. Sum of order amount/sum of total items is better way to evaluate the data.

###### b.	What metric would you report for this dataset?
- Order amount and total items

###### c.	What is its value?
-  357.92

#### Question 2: For this question you’ll need to use SQL. [Follow this link](https://www.w3schools.com/SQL/TRYSQL.ASP?FILENAME=TRYSQL_SELECT_ALL) to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

###### a.	How many orders were shipped by Speedy Express in total?

- select Count(OrderID) FROM Orders  
inner join Shippers  
on Orders.ShipperId=Shippers.ShipperId  
where ShipperName="Speedy Express";

###### b.	What is the last name of the employee with the most orders?

- select LastName, a.EmployeeID,a.TotalOrders from  
(select EmployeeID, Sum(Quantity) as TotalOrders from Orders  
inner join OrderDetails  
on OrderDetails.OrderId=Orders.OrderId  
group by Orders.EmployeeId)a  
inner join Employees  
on Employees.EmployeeID=a.EmployeeID  
order by TotalOrders desc
limit 1;

###### c.	What product was ordered the most by customers in Germany?

- select OrderDetails.Quantity, OrderDetails.ProductID, Products.ProductName  
from OrderDetails  
inner join Orders  
on OrderDetails.OrderID=Orders.OrderID  
inner join Products  
on OrderDetails.ProductID=Products.ProductID  
inner join Customers  
on Orders.CustomerID=Customers.CustomerID  
where Country="Germany"  
group by OrderDetails.ProductID  
order by OrderDetails.Quantity desc  
limit 1;

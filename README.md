# Shopify-Technical-Challenge
Winter 2022 Data Science Intern Challenge 

Please complete the following questions, and provide your thought process/work. You can attach your work in a text file, link, etc. on the application page. Please ensure answers are easily visible for reviewers!


Question 1: Given some sample data, write a program to answer the following: click here to access the required data set  

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis.  

a.	Think about what could be going wrong with our calculation. Think about a better way to evaluate this data.     
<b> The only reason I can come up with for such a bizarre answer is that the denominator we calculated for calculating AOV is much smaller than required and the only way we can get a small AOV is by just getting the count of number of rows of total_items instead of summing all the values in the column. This is a very common mistake and one which I have made previously!! <b>   
b.	What metric would you report for this dataset?  
<b> The metrics required for calculating AOV are: sum of order amount and the sum of total items purchased.<b>
c.	What is its value?  
<b> The correct AOV value is $357.92 <b>



Question 2: For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.  

a.	How many orders were shipped by Speedy Express in total?  

* SELECT count(ShipperID) as 'Total Orders' FROM Orders where ShipperID == 1;  

<b> 54 Total Orders by Speedy Express <b>

b.	What is the last name of the employee with the most orders?  
* SELECT Employees.LastName, Orders.EmployeeID, count(Orders.EmployeeID) as 'Number of Orders' from Orders
JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID 
GROUP BY Employees.EmployeeID;

<b> 40 orders were the maximum made by an employee with EMPID = 4 and Last Name Peacock <b>

c.	What product was ordered the most by customers in Germany?    
* SELECT Orders.OrderID, Customers.Country, OrderDetails.Quantity, Products.ProductName, (OrderDetails.Quantity * Count(*)) as 'Total Ordered' from Orders, OrderDetails
join Customers on Orders.CustomerID = Customers.CustomerID
join Products on OrderDetails.ProductID = Products.ProductID 
where Customers.Country = 'Germany' group by Products.ProductName,
order by sum(OrderDetails.Quantity) DESC;  

<b> This statement tells us the the most ordered product in Germany was Camembert Pierrot and Nord-Ost Matjeshering with 12000 total orders each. <b>
  


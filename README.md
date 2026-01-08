Table 1: Customers(CustomerID, CustomerName, City)
Table 2: Orders(OrderID, CustomerID, OrderDate, Amount)
Table 3: Payments(PaymentID, CustomerID, PaymentDate, Amount)
Table 4: Employees(EmployeeID, EmployeeName, ManagerID)
# Question 1: Retrieve all customers who have placed at least one order.
sql
Copy code
SELECT DISTINCT c.*
FROM Customers c
INNER JOIN Orders o
ON c.CustomerID = o.CustomerID;
# Question 2: Retrieve all customers and their orders, including customers who have not placed any orders.
sql
Copy code
SELECT c.CustomerID, c.CustomerName, o.OrderID, o.OrderDate, o.Amount
FROM Customers c
LEFT JOIN Orders o
ON c.CustomerID = o.CustomerID;
# Question 3: Retrieve all orders and their corresponding customers, including orders placed by unknown customers.
sql
Copy code
SELECT o.OrderID, o.OrderDate, o.Amount, c.CustomerName
FROM Orders o
LEFT JOIN Customers c
ON o.CustomerID = c.CustomerID;
# Question 4: Display all customers and orders, whether matched or not.
sql
Copy code
SELECT c.CustomerID, c.CustomerName, o.OrderID, o.OrderDate, o.Amount
FROM Customers c
LEFT JOIN Orders o
ON c.CustomerID = o.CustomerID

UNION

SELECT c.CustomerID, c.CustomerName, o.OrderID, o.OrderDate, o.Amount
FROM Customers c
RIGHT JOIN Orders o
ON c.CustomerID = o.CustomerID;
# Question 5: Find customers who have not placed any orders.
sql
Copy code
SELECT c.*
FROM Customers c
LEFT JOIN Orders o
ON c.CustomerID = o.CustomerID
WHERE o.OrderID IS NULL;
# Question 6: Retrieve customers who made payments but did not place any orders.
sql
Copy code
SELECT DISTINCT c.*
FROM Customers c
INNER JOIN Payments p
ON c.CustomerID = p.CustomerID
LEFT JOIN Orders o
ON c.CustomerID = o.CustomerID
WHERE o.OrderID IS NULL;
# Question 7: Generate a list of all possible combinations between Customers and Orders.
sql
Copy code
SELECT c.CustomerName, o.OrderID
FROM Customers c
CROSS JOIN Orders o;
# Question 8: Show all customers along with order and payment amounts in one table.
sql
Copy code
SELECT c.CustomerName,
       o.Amount AS OrderAmount,
       p.Amount AS PaymentAmount
FROM Customers c
LEFT JOIN Orders o
ON c.CustomerID = o.CustomerID
LEFT JOIN Payments p
ON c.CustomerID = p.CustomerID;
# Question 9: Retrieve all customers who have both placed orders and made payments.
sql
Copy code
SELECT DISTINCT c.*
FROM Customers c
INNER JOIN Orders o
ON c.CustomerID = o.CustomerID
INNER JOIN Payments p
ON c.CustomerID = p.CustomerID;

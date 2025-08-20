# Task_5_SQL_JOINS
# Using Database 'Ecommerce' and new tables 'CUSTOMERS', 'ORDERS' and 'PRODUCTS' for joining multiple tables using MySQL Workbench.


CREATE DATABASE Ecommerce;
USE Ecommerce;

CREATE TABLE Customers(
Customer_id INT PRIMARY KEY NOT NULL,
first_name VARCHAR(50),
last_name VARCHAR(50),
email VARCHAR(100),
City VARCHAR(100)
);

INSERT INTO Customers VALUES
(1, 'Amit', 'Kumar', 'amitkumar@ecommerce.com', 'Lucknow'),
(2, 'Ramesh', 'Khanna', 'rameshkhanna@ecommerce.com', 'Amritsar'),
(3, 'Venkat', 'Iyer', 'venkatiyer@ecommerce.com', 'Chennai'),
(4, 'Rahul', 'Verma', 'rahulverma@ecommerce.com', 'Rohtak'),
(5, 'Anjali', 'Sharma', 'anjalisharma@ecommerce.com', 'Noida'),
(6, 'Kartik', 'Malhotra', 'kartikmalhotra@ecommerce.com', 'Delhi'),
(7, 'Kajal', 'Aggarwal', 'kajalaggrawal@ecommerce.com', 'Tamilnadu'),
(8, 'Shashi', 'Bala', 'shashibala@ecommerce.com', 'Kanpur'),
(9, 'Mala', 'Sinha', 'malasinha@ecommerce.com', 'Varanasi'),
(10, 'Babita', 'Rani', 'babitarani@ecommerce.com', 'Delhi');

SELECT * FROM Customers;

# <img width="615" height="319" alt="image" src="https://github.com/user-attachments/assets/f36ca891-b0d6-4499-8b9c-7fb47b6629c4" />

CREATE TABLE Orders(
Order_id INT PRIMARY KEY NOT NULL,
order_date DATE,
amount DECIMAL(6,2) DEFAULT 100,
product_name VARCHAR(100),
quantity INT,
Customer_id INT,
FOREIGN KEY(Customer_id) REFERENCES Customers(Customer_id)
);

INSERT INTO Orders VALUES
(101, '2025-02-05', 500, 'Keyboard', 3, 4),
(102, '2025-01-17', 600, 'Keyboard', 2, 3),
(103, '2024-12-09', 1500, 'Speaker', 6, 1),
(104, '2024-09-25', 900, 'Mouse', 3, 9),
(105, '2025-03-07', 1900, 'Wires', 1, 7),
(106, '2025-04-11', 2000, 'Monitor', 6, 8),
(107, '2025-05-15', 8000, 'Printer', 9, 1),
(108, '2025-06-13', 5000, 'Phone', 1, 6),
(109, '2025-07-18', 200, 'Mouse', 5, 10);

SELECT * FROM Orders;

# <img width="551" height="279" alt="image" src="https://github.com/user-attachments/assets/be9bd73f-b98b-462a-bb52-0c84c561ea0f" />

CREATE TABLE Products(
product_id INT PRIMARY KEY NOT NULL,
product_category VARCHAR(100),
product_status VARCHAR(50) DEFAULT 'Available',
order_id INT,
FOREIGN KEY(order_id ) REFERENCES Orders(order_id)
);

INSERT INTO Products VALUES
(11, 'Electronics', 'Available', 101),
(12, 'Electronics', 'Not Available', 106),
(13, 'Electronics', 'Not Available', 103),
(14, 'Electronics', 'Available', 101),
(15, 'Electronics', 'Available' ,102);

SELECT * FROM Products;

# <img width="508" height="199" alt="image" src="https://github.com/user-attachments/assets/23ab1671-b999-4458-a8ef-3338c597749c" />


# JOINING 3 Tables by using INNER JOIN:
SELECT * FROM Customers c
INNER JOIN Orders o
ON c.Customer_id = o.Customer_id
INNER JOIN Products p
ON p.order_id = o.order_id;

# <img width="1468" height="171" alt="image" src="https://github.com/user-attachments/assets/b5fcca62-b9b0-4287-ba3e-a3c36d163874" />


# Joining Customers and Orders Table:
SELECT * FROM Customers c
JOIN Orders o
ON o.customer_id = c.customer_id;

# <img width="1111" height="258" alt="image" src="https://github.com/user-attachments/assets/e77873ca-acd5-4743-bd55-d53ef0cf3f1c" />


# Joining Orders and Products Table:
SELECT * FROM Orders o 
JOIN Products p
ON o.order_id = p.order_id;

# <img width="960" height="173" alt="image" src="https://github.com/user-attachments/assets/8f48a4b8-c2dd-4790-83ea-126676cab777" />


# Using LEFT JOIN by joining Customers and Orders Table::
SELECT * FROM Customers c
LEFT JOIN Orders o
ON c.Customer_id = o.Customer_id;

# <img width="1102" height="297" alt="image" src="https://github.com/user-attachments/assets/a62a86d0-ebe3-44a1-b306-f83ade5559ff" />


# Using RIGHT JOIN by joining Customers and Orders Table::
SELECT * FROM Customers c
RIGHT JOIN Orders o
ON c.Customer_id = o.Customer_id;

# <img width="1104" height="245" alt="image" src="https://github.com/user-attachments/assets/58acd7a5-e30f-454c-a1bd-4b2a4b1b7380" />


# Using CROSS JOIN
SELECT * FROM Customers c
CROSS JOIN Orders o;

# <img width="1087" height="691" alt="image" src="https://github.com/user-attachments/assets/f6f7e73c-1d46-4abc-9bd5-8c55d3fbddae" />

# Using FULL JOIN by UNION with Customers and Orders Table::
SELECT *
FROM Customers c
LEFT JOIN Orders o
ON c.Customer_id= o.Customer_id
UNION
SELECT *
FROM Customers c
RIGHT JOIN Orders o
ON c.Customer_id= o.Customer_id; 

# <img width="1107" height="310" alt="image" src="https://github.com/user-attachments/assets/018de4c1-2c61-4e98-aff5-4937341c2e98" />

# Using 'WHERE' clause:
SELECT c.first_name, c.last_name, c.customer_id, c.City FROM Customers c
JOIN Orders o 
ON c.Customer_id = o. Customer_id
WHERE c.City = 'Delhi';

# <img width="370" height="104" alt="image" src="https://github.com/user-attachments/assets/6647c3b3-f253-4d84-a550-a4d3f331c4b7" />

# Using 'AND' operator:
SELECT c.first_name, c.last_name, c.City, o.amount, o.product_name FROM Customers c
JOIN Orders o 
ON c.Customer_id = o. Customer_id
WHERE c.City = 'Delhi' AND o.amount > 900;

# <img width="449" height="88" alt="image" src="https://github.com/user-attachments/assets/cf073577-730a-4ee4-a94b-e2b02fdabbd8" />

# Using 'BETWEEN' operator:
SELECT c.first_name, c.last_name, c.City, o.amount, o.product_name FROM Customers c
JOIN Orders o 
ON c.Customer_id = o. Customer_id
WHERE o.amount BETWEEN 1500 AND 8000;

# <img width="465" height="194" alt="image" src="https://github.com/user-attachments/assets/67419323-9dda-4967-bf37-b4897b96c6d6" />

# Using 'LIKE' operator:
SELECT c.first_name, c.last_name, c.City, o.amount, o.product_name FROM Customers c
LEFT JOIN Orders o 
ON c.Customer_id = o. Customer_id
WHERE c.first_name LIKE 'a%';

# <img width="478" height="130" alt="image" src="https://github.com/user-attachments/assets/667641e2-dd27-43b0-ac11-e0d502350461" />

# Using 'IN' operator:
SELECT c.first_name, c.last_name, o.amount, o.product_name FROM Customers c
LEFT JOIN Orders o 
ON c.Customer_id = o. Customer_id
WHERE c.City IN ('Noida', 'Kanpur', 'Lucknow');

# <img width="401" height="172" alt="image" src="https://github.com/user-attachments/assets/09841cee-eea5-4699-8a4f-7d715920c714" />



# Using Aggregate Functions(COUNT, SUM, MIN, MAX, AVG):
SELECT COUNT(*) AS total_customers
FROM Customers c
INNER JOIN Orders o
ON c.Customer_id = o.Customer_id;

# <img width="167" height="95" alt="image" src="https://github.com/user-attachments/assets/fa304c52-07e0-460e-8c8b-d9c2cbe4d56d" />

SELECT SUM(o.amount) AS total_amount
FROM Customers c
INNER JOIN Orders o
ON c.Customer_id = o.Customer_id;

# <img width="160" height="88" alt="image" src="https://github.com/user-attachments/assets/b62b0373-735d-4979-bb90-1b741021e1d8" />

SELECT MAX(o.amount) AS maximum_amount 
FROM Customers c
INNER JOIN Orders o
ON c.Customer_id = o.Customer_id;

# <img width="177" height="81" alt="image" src="https://github.com/user-attachments/assets/9396ab88-2b3b-4ada-87ed-2a128177dd06" />

SELECT MIN(o.amount) AS minimum_amount 
FROM Customers c
INNER JOIN Orders o
ON c.Customer_id = o.Customer_id;

# <img width="160" height="84" alt="image" src="https://github.com/user-attachments/assets/50fc7609-6b2d-4b89-9b41-c5a42c44eb65" />

SELECT AVG(o.amount) AS avg_amount 
FROM Customers c
INNER JOIN Orders o
ON c.Customer_id = o.Customer_id;

# <img width="173" height="113" alt="image" src="https://github.com/user-attachments/assets/33ad9b67-d8e5-45a5-b054-7e6bbd3d70bb" />



# Using 'ORDER BY' clause and 'LIMIT' clause for finding Highest amount:
SELECT * FROM Customers c
JOIN Orders o 
ON c.Customer_id = o.Customer_id
ORDER BY o.amount desc
LIMIT 1;

# <img width="1091" height="84" alt="image" src="https://github.com/user-attachments/assets/d0442dc6-36c3-455a-8d5c-c50dd1498fff" />

# Using 'ORDER BY' clause and 'LIMIT' clause for finding Highest quantity:
SELECT * FROM Customers c
JOIN Orders o 
ON c.Customer_id = o.Customer_id
ORDER BY o.quantity desc
LIMIT 3;

# <img width="1082" height="123" alt="image" src="https://github.com/user-attachments/assets/5ffa91ca-ef70-4bb2-8bb1-999fceee1265" />

# Using 'GROUP BY' clause for total amount:
SELECT c.City, SUM(o.amount) AS total_amount 
FROM Customers c
INNER JOIN Orders o
ON c.Customer_id = o.Customer_id
GROUP BY c.City;

# <img width="261" height="246" alt="image" src="https://github.com/user-attachments/assets/b68b9a87-b15a-467e-81cb-113db7d3b62e" />

# Using 'CROSS JOIN' with WHERE clause:
SELECT c.customer_id, o.product_name FROM Customers c
CROSS JOIN Orders o
WHERE c.Customer_id IN(1,4);

# <img width="252" height="467" alt="image" src="https://github.com/user-attachments/assets/1bc23740-1cdb-4f91-b3b0-e494b6cde1d3" />







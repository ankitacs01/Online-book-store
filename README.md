# 📚 Online Bookstore Management System – SQL Project

### 👩‍💻 Created by: Ankita Misal

This project is a simple relational database system built for an *Online Bookstore* using SQL. It focuses on organizing books, customers, and orders efficiently, and performing meaningful analysis using SQL queries.

---

## 🗃 Database Tables:

### 1. 📘 Books Table
- BookID (Primary Key)
- Title
- Author
- Genre
- Price
- StockQty

### 2. 👤 Customers Table
- CustomerID (Primary Key)
- FullName
- Email
- Phone
- City

### 3. 📦 Orders Table
- OrderID (Primary Key)
- CustomerID (Foreign Key)
- BookID (Foreign Key)
- OrderDate
- Quantity
- TotalAmount

---

## 📊 Features & Queries:

- View top-selling books
- Calculate revenue by book or genre
- Track orders by customer
- List out-of-stock books
- Find most active customers
- Use of SQL JOINS, GROUP BY, HAVING, and ORDER BY

---

## 🧪 Sample SQL Query

```sql
SELECT c.FullName, COUNT(o.OrderID) AS TotalOrders
FROM Customers c
JOIN Orders o ON c.CustomerID = o.CustomerID
GROUP BY c.FullName
ORDER BY TotalOrders DESC;

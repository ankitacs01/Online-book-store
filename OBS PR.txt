----        ONLINE BOOK STORE   --------

-- CREATE TABLE BOOK --

DROP TABLE IF EXISTS Books;
CREATE TABLE Books (
    Book_ID SERIAL PRIMARY KEY,
    Title VARCHAR(100),
    Author VARCHAR(100),
    Genre VARCHAR(50),
    Published_Year INT,
    Price NUMERIC(10, 2),
    Stock INT
);
 SELECT * FROM Books;

 -- CREATE TABLE CUSTOMER --

DROP TABLE IF EXISTS customers;
CREATE TABLE Customers (
    Customer_ID SERIAL PRIMARY KEY,
    Name VARCHAR(100),
    Email VARCHAR(100),
    Phone VARCHAR(15),
    City VARCHAR(50),
    Country VARCHAR(150)
);
SELECT * FROM Customers;

-- CREATE TABLE ORDERS --

DROP TABLE IF EXISTS orders;
CREATE TABLE Orders (
    Order_ID SERIAL PRIMARY KEY,
    Customer_ID INT REFERENCES Customers(Customer_ID),
    Book_ID INT REFERENCES Books(Book_ID),
    Order_Date DATE,
    Quantity INT,
    Total_Amount NUMERIC(10, 2)
);

SELECT * FROM Books;
SELECT * FROM Customers;
SELECT * FROM Orders;

-- 1) Retrieve all books in the "Fiction" genre:

select * from books
where genre='Fiction';

-- 2) Find books published after the year 1950:

select * from books
where published_year >1950;

-- 3) List all customers from the Canada:

select* from customers
where country='Canada';

-- 4) Show orders placed in November 2023:

SELECT * FROM Orders 
WHERE order_date BETWEEN '2023-11-01' AND '2023-11-30';

-- 5) Retrieve the total stock of books available:

select sum(stock) as total stock
from books;

-- 6) Find the details of the most expensive book:

select *from books order by price desc;   --1 haw asel tr limit 1 lawaych --

-- 7) Show all customers who ordered more than 1 quantity of a book:

select * from orders
where quantity > 1;

-- 8) Retrieve all orders where the total amount exceeds $20:

select * from orders
where total_amount >20;

-- 9) List all genres available in the Books table:

select distinct genre from books;    --distinct repeat aslel show nhi krt unique dakhwt --

-- 10) Find the book with the lowest stock:

select * from books order by stock asc limit 1;

-- 11) Calculate the total revenue generated from all orders:

select sum(total_amount)as revenue from orders;

-----------------  ADVANCE QUESTION  -----------------


select* from orders;
select* from books;
select* from Customers;

-- 1) Retrieve the total number of books sold for each genre:

select b.Genre, sum(o.Quantity) as total_b_sold
from Orders o JOIN Books b 
on o.book_id = b.book_id
group by b.genre;

-- 2) Find the average price of books in the "Fantasy" genre:

select avg(price) from books
where genre ='Fantasy';

-- 3) List customers who have placed at least 2 orders:

select o.customer_id,count(o.quantity)
from orders o join customers c
on o.customer_id = c.customer_id
group by o.customer_id
having count(order_id) >=2;

-- 4) Find the most frequently ordered book:

SELECT o.Book_id, b.title, COUNT(o.order_id) AS ORDER_COUNT
FROM orders o JOIN books b
ON o.book_id=b.book_id
GROUP BY o.book_id, b.title
ORDER BY ORDER_COUNT DESC LIMIT 1;

-- 5) Show the top 3 most expensive books of 'Fantasy' Genre :

select *from books
where genre= 'Fantasy'
order by price DESC LIMIT 3;

-- 6) Retrieve the total quantity of books sold by each author:

select b.author, sum(o.quantity) as total book sold
from books b join orders o
on b.book_id = o.book_id
group by author;

-- 7) List the cities where customers who spent over $30 are located:

select distinct c.city, o.total_amount
from customers c join orders o
on c.customer_id = o.customer_id
where o.total_amount > 30;

-- 8) Find the customer who spent the most on orders:

SELECT c.customer_id, c.name, SUM(o.total_amount) AS Total_Spent
FROM orders o JOIN customers c
ON o.customer_id=c.customer_id
GROUP BY c.customer_id, c.name
ORDER BY Total_spent Desc LIMIT 1;

--9) Calculate the stock remaining after fulfilling all orders:

SELECT b.book_id, b.title, b.stock,
COALESCE(SUM(o.quantity),0)
AS Order_quantity,  
b.stock- COALESCE(SUM(o.quantity),0) AS Remaining_Quantity
FROM books b LEFT JOIN orders o
ON b.book_id=o.book_id
GROUP BY b.book_id 
ORDER BY b.book_id;




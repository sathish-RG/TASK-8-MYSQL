# MYSQL TASK 

## 1) Create database named ecommerce.

### code
```sql
create database ecommerce;
use ecommerce; 
```
## 2) Create three tables: customers, orders, and products.

### creating customers table.
```sql
create table customers (
id int auto_increment primary key,
name varchar(100),
email varchar(100),
address text
);
```
```sql
desc customers;
```
output
```markdown
+---------+--------------+------+-----+---------+----------------+
| Field   | Type         | Null | Key | Default | Extra          |
+---------+--------------+------+-----+---------+----------------+
| id      | int          | NO   | PRI | NULL    | auto_increment |
| name    | varchar(100) | YES  |     | NULL    |                |
| email   | varchar(100) | YES  |     | NULL    |                |
| address | text         | YES  |     | NULL    |                |
+---------+--------------+------+-----+---------+----------------+
```
## creating orders table.
```sql
CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    total_amount DECIMAL(10, 2),
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);
```
```sql
desc orsers;
```
output
```markdown
+--------------+---------------+------+-----+---------+----------------+
| Field        | Type          | Null | Key | Default | Extra          |
+--------------+---------------+------+-----+---------+----------------+
| id           | int           | NO   | PRI | NULL    | auto_increment |
| customer_id  | int           | YES  | MUL | NULL    |                |
| order_date   | date          | YES  |     | NULL    |                |
| total_amount | decimal(10,2) | YES  |     | NULL    |                |
+--------------+---------------+------+-----+---------+----------------+
```

## Creating products table.
```sql
create table products(
    id int auto_increment primary key,
    name varchar(100) not null,
    price decimal(10,2) not null,
    description text
);
```
```sql
desc products;
```
output
```markdown
+-------------+---------------+------+-----+---------+----------------+
| Field       | Type          | Null | Key | Default | Extra          |
+-------------+---------------+------+-----+---------+----------------+
| id          | int           | NO   | PRI | NULL    | auto_increment |
| name        | varchar(100)  | NO   |     | NULL    |                |
| price       | decimal(10,2) | NO   |     | NULL    |                |
| description | text          | YES  |     | NULL    |                |
+-------------+---------------+------+-----+---------+----------------+
```

## 3) Insert data into the tables.
### customer table data insert.
```sql
insert into customers (name,email,address)
values('Sathish','sathish@gmail.com','chennai'),
     ('Balaji','balaji@gmail.com','banglur'),
     ('Ragav','ragave@gmail.com','trichy');
```
```sql 
select * from customers;
```
--Customers table output:
```markdown
output
+----+---------+-------------------+---------+
| id | name    | email             | address |
+----+---------+-------------------+---------+
|  7 | Sathish | sathish@gmail.com | chennai |
|  8 | Balaji  | balaji@gmail.com  | banglur |
|  9 | Ragav   | ragave@gmail.com  | trichy  |
+----+---------+-------------------+---------+
```
### Orders table data insert.
```sql
insert into orders(order_date,total_amount)
values (curdate(),50.00),
       (curdate() - interval 10 day ,75.00),
       (curdate() - interval 40 day ,30.00);
```
```sql 
select * from orders;
```
output
```markdown
+----+-------------+------------+--------------+
| id | customer_id | order_date | total_amount |
+----+-------------+------------+--------------+
| 31 |           7 | 2024-12-25 |        50.00 |
| 32 |           8 | 2024-12-15 |        75.00 |
| 33 |           9 | 2024-11-15 |        30.00 |
+----+-------------+------------+--------------+
```
### products table data insert.
```sql 
insert into products (name,price,description)
values('Product A',30.00,'discription of product A'),
      ('Product B',40.00,'discription of product B'),
      ('Product C',25.00,'discription of product C');
```
```sql 
select * from products;
```
output
```markdown
+----+-----------+-------+--------------------------+
| id | name      | price | description              |
+----+-----------+-------+--------------------------+
|  1 | Product A | 30.00 | discription of product A |
|  2 | Product B | 40.00 | discription of product B |
|  3 | Product C | 25.00 | discription of product C |
+----+-----------+-------+--------------------------+
```
# QUERIES:
## 1) Retrieve all customers who have placed an order in the last 30 days.
```sql
select distinct c.*
from customers c
join orders o on c.id = o.customer_id
where o.order_date >= curdate() - interval 30 day;
```
output
```markdown
+----+---------+-------------------+--------------+
| id | name    | email             | address      |
+----+---------+-------------------+--------------+
|  7 | Sathish | sathish@gmail.com |  chennai     |
|  8 | Balaji  | balaji@gmail.com  |  banglur     |
+----+---------+-------------------+--------------+
```
## 2) Get the total amount of all orders placed by each customer.
```sql
select c.name, SUM(o.total_amount) as total_spent
from customers c
join orders o on c.id = o.customer_id
group by c.id;
```
output
```markdown
+---------+-------------+
| name    | total_spent |
+---------+-------------+
| Sathish |       50.00 |
| Balaji  |       75.00 |
| Ragav   |       30.00 |
+---------+-------------+
```
## 3) Update the price of Product C to 45.00.
```sql
 UPDATE products
    -> SET price = 45.00
    -> WHERE name = 'product c';
```
```sql 
SELECT * FROM products WHERE name = 'product c';
```
output
```markdown
+----+-----------+-------+--------------------------+      
| id | name      | price | description              |      
+----+-----------+-------+--------------------------+      
|  3 | Product C | 45.00 | discription of product C |      
+----+-----------+-------+--------------------------+ 
```     
## 4)  Add a new column discount to the products table.
```sql
alter table products
add column discount decimal(5,2) default 0.00;
```
```sql
select * from products;
```
output
```markdown
+----+-----------+-------+--------------------------+----------+
| id | name      | price | description              | discount |
+----+-----------+-------+--------------------------+----------+
|  1 | Product A | 30.00 | discription of product A |     0.00 |
|  2 | Product B | 40.00 | discription of product B |     0.00 |
|  3 | Product C | 45.00 | discription of product C |     0.00 |
+----+-----------+-------+--------------------------+----------+
```
## 5) Retrieve the top 3 products with the highest price.
```sql
SELECT name, price FROM products 
ORDER BY price DESC
LIMIT 3;
```
output
``` markdown
+-----------+-------+
| name      | price |
+-----------+-------+
| Product C | 45.00 |
| Product B | 40.00 |
| Product A | 30.00 |
+-----------+-------+
```
## 6) Get the names of customers who have ordered Product A.
```sql
SELECT DISTINCT c.name
FROM customers c
JOIN orders o ON c.id = o.customer_id
JOIN order_items oi ON o.id = oi.order_id
JOIN products p ON oi.product_id = p.id
WHERE p.name = 'Product A';
```
output
```markdown
+----------+
| name     |
+----------+
| Sathish  |
| Balaji   |
+----------+
```
## 7) Join the orders and customers tables to retrieve the customer's name and order date for each order.
```sql
select c.name, o.order_date
from orders o
join customers c on o.customer_id = c.id;
```
output
```markdown
+---------+------------+
| name    | order_date |
+---------+------------+
| Sathish | 2024-12-25 |
| Balaji  | 2024-12-15 |
| Ragav   | 2024-11-15 |
+---------+------------+
```
## 8) Retrieve the orders with a total amount greater than 150.00
```sql
select * from orders
where total_amount > 150.00;
```
output
```markdown
+----+-------------+------------+--------------+
| id | customer_id | order_date | total_amount |
+----+-------------+------------+--------------+
| 36 |           7 | 2024-12-25 |       200.00 |
+----+-------------+------------+--------------+
```
## 9) Normalize the database by creating a separate table for order items and updating the orders table to reference the order_items table.
```sql
create table order_items (
    id int auto_increment primary key,
    order_id int,
    product_id int,
    quantity int default 1,
    Foreign key  (order_id) references orders(id),
    Foreign key (product_id) references products(id));
```
output
```markdown
+------------+------+------+-----+---------+-------+
| Field      | Type | Null | Key | Default | Extra |
+------------+------+------+-----+---------+-------+
| order_id   | int  | NO   | PRI | NULL    |       |
| product_id | int  | NO   | PRI | NULL    |       |
| quantity   | int  | YES  |     | NULL    |       |
+------------+------+------+-----+---------+-------+
```
## 10) Retrieve the average total of all orders.
```sql
select AVG(total_amount) as average_order_total
FROM orders;
```
output
```markdown
+---------------------+
| average_order_total |
+---------------------+
|           88.750000 |
+---------------------+
```




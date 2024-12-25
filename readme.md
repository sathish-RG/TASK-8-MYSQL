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
--output
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
--output
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
--output
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
--output
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
--output
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
--output
```markdown
+----+-----------+-------+--------------------------+
| id | name      | price | description              |
+----+-----------+-------+--------------------------+
|  1 | Product A | 30.00 | discription of product A |
|  2 | Product B | 40.00 | discription of product B |
|  3 | Product C | 25.00 | discription of product C |
+----+-----------+-------+--------------------------+
```
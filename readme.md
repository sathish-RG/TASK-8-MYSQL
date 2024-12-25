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
desc customers;
```
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
# Introduction to database's

![Pasted image 20250730170835.png](images/Pasted%20image%2020250730170835.png)

in this exercise i will perform some CRUD operations using SQL (Structured Query Language)



First, let's create a database called 'store':

```SQL
create database store;
```

After we create the database we will use it using `use <database Name>`:

```SQL
use store;
```

Now, we will create the tables:

```SQL 
create table countries(  
    code int primary key,  
    name varchar(20) unique,  
    continent_name varchar(20) not null  
);  
  
create table users(  
    id int primary key,  
    full_name varchar(20),  
    email varchar(20) unique,  
    gender char(1) check (gender IN ('M', 'F')),  
    date_of_birth varchar(15),  
    created_at datetime,  
    country_code int references countries(code)  
);  
  
create table orders(  
    id int primary key,  
    user_id int references users(id),  
    status varchar(6) check(status in ('start','finish')),  
    created_at datetime  
);  
  
#create table products  
create table products(  
    id int primary key ,  
    name varchar(10) not null,  
    price float default 0,  
    status varchar(10) check ( status in ('valid','expired')),  
    created_at datetime  
);  
  
#create table order_products  
create table order_products(  
    order_id int references orders(id),  
    product_id int references products(id),  
    quantity int default 0  
);
```

to show tables:
```SQL
show tables;
```

tables:
![Pasted image 20250730172025.png](images/Pasted%20image%2020250730172025.png)


now lets insert some data using `INSERT INTO`:
```sql
-- 1. Add new row to countries table  
INSERT INTO countries (code, name, continent_name)  
VALUES (966, 'Saudi Arabia', 'Asia');  
  
-- 2. Add new row to users table  
INSERT INTO users (id, full_name, email, gender, date_of_birth, created_at, country_code)  
VALUES (1, 'Mohammed Al-Ahmad', 'mohammed@email.sa', 'M', '1995-08-20', '2025-07-30 10:30:00', 966);  
  
-- 3. Add new row to orders table  
INSERT INTO orders (id, user_id, status, created_at)  
VALUES (1, 1, 'start', '2025-07-30 10:35:00');  
  
-- 4. Add new row to products table  
INSERT INTO products (id, name, price, status, created_at)  
VALUES (1, 'Dates', 45.99, 'valid', '2025-07-30 09:00:00'),  
       (2, 'Oud', 299.99, 'valid', '2025-07-30 09:00:00'),  
       (3, 'Coffee Set', 159.99, 'valid', '2025-07-30 09:00:00');  
  
-- 5. Add new row to order_products table  
INSERT INTO order_products (order_id, product_id, quantity)  
VALUES (1, 1, 3),  
       (1, 2, 1),  
       (1, 3, 2);
```

after that lets update data using `Update`:

```sql
UPDATE countries SET continent_name = 'Middle East' WHERE code = 966;
```


country before updating:
![Pasted image 20250730172421.png](images/Pasted%20image%2020250730172421.png)

country after updating:
![Pasted image 20250730172539.png](images/Pasted%20image%2020250730172539.png)

finally we will perform some deletion using `DELETE`:
```SQL
DELETE FROM products WHERE id = 2;
```


product table before deletion:
![Pasted image 20250730172724.png](images/Pasted%20image%2020250730172724.png)

product table after deletion:
![Pasted image 20250730172920.png](images/Pasted%20image%2020250730172920.png)
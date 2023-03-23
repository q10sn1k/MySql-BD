```
CREATE DATABASE my_database;
Query OK, 1 row affected (0.02 sec)
mysql> USE my_database;
Database changed
mysql> SHOW tables;
Empty set (0.02 sec)
mysql> SHOW DATABASES;

+--------------------+
| Database           |
+--------------------+
| ex                 |
| example            |
| information_schema |
| my_database        |
| mydatabase         |
| mysql              |
| orders_product     |
| performance_schema |         |
| sys                |
| test               |
| users              |
| world              |
+--------------------+
13 rows in set (0.00 sec)

mysql> CREATE DATABASE IF NOT EXISTS mydatabase;
Query OK, 1 row affected, 1 warning (0.00 sec)
mysql> USE my_database

Database changed

mysql> SHOW tables;
Empty set (0.00 sec)
mysql> CREATE TABLE users (
    -> id INT(11) NOT NULL AUTO_INCREMENT,
    -> name VARCHAR(50) NOT NULL,
    -> email VARCHAR(50) NOT NULL,
    -> age INT(11) NOT NULL,
    -> country VARCHAR(50) NOT NULL,
    -> balance FLOAT NOT NULL,
    -> PRIMARY KEY (id)
    -> );
    
Query OK, 0 rows affected, 2 warnings (0.07 sec)
mysql> SHOW TABLES;
+-----------------------+
| Tables_in_my_database |
+-----------------------+
| users                 |
+-----------------------+

1 row in set (0.00 sec)
mysql> DESCRIBE users;
+---------+-------------+------+-----+---------+----------------+
| Field   | Type        | Null | Key | Default | Extra          |
+---------+-------------+------+-----+---------+----------------+
| id      | int         | NO   | PRI | NULL    | auto_increment |
| name    | varchar(50) | NO   |     | NULL    |                |
| email   | varchar(50) | NO   |     | NULL    |                |
| age     | int         | NO   |     | NULL    |                |
| country | varchar(50) | NO   |     | NULL    |                |
| balance | float       | NO   |     | NULL    |                |
+---------+-------------+------+-----+---------+----------------+
6 rows in set (0.01 sec)

mysql> INSERT INTO users (name, email, age, country, balance) VALUES
    -> ('Ivan', 'ivan@example.com', 25, 'RUS', 100000.00);
Query OK, 1 row affected (0.01 sec)
mysql> SELECT * FROM users;
+----+------+------------------+-----+---------+---------+
| id | name | email            | age | country | balance |
+----+------+------------------+-----+---------+---------+
|  1 | Ivan | ivan@example.com |  25 | RUS     |  100000 |
+----+------+------------------+-----+---------+---------+
1 row in set (0.00 sec)

mysql> SELECT id, name, age FROM users;
+----+------+-----+
| id | name | age |
+----+------+-----+
|  1 | Ivan |  25 |
+----+------+-----+
1 row in set (0.00 sec)

mysql> SELECT id, name, email, age, country, balance FROM users;
+----+------+------------------+-----+---------+---------+
| id | name | email            | age | country | balance |
+----+------+------------------+-----+---------+---------+
|  1 | Ivan | ivan@example.com |  25 | RUS     |  100000 |
+----+------+------------------+-----+---------+---------+
1 row in set (0.00 sec)

mysql> SELECT * FROM users;
+----+------+------------------+-----+---------+---------+
| id | name | email            | age | country | balance |
+----+------+------------------+-----+---------+---------+
|  1 | Ivan | ivan@example.com |  25 | RUS     |  100000 |
+----+------+------------------+-----+---------+---------+
1 row in set (0.00 sec)

mysql> INSERT INTO users (name, email, age , country, balance) VALUES
    -> ('Gleb', 'gleb@exmple.com', 26, 'RUS', 90000.00),
    -> ('Sergey', 'sergey@example.com', 28, 'RUS', 90000.00),
    -> ('Andrew', 'andrew@example.com', 24, 'RUS', 95000.00),
    -> ('Bob', 'bob@example.com', 25, 'USA', 100000.00),
    -> ('Tom', 'tom@example.com', 29, 'USA', 110000.00);
Query OK, 5 rows affected (0.00 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM users;
+----+--------+--------------------+-----+---------+---------+
| id | name   | email              | age | country | balance |
+----+--------+--------------------+-----+---------+---------+
|  1 | Ivan   | ivan@example.com   |  25 | RUS     |  100000 |
|  2 | Gleb   | gleb@exmple.com    |  26 | RUS     |   90000 |
|  3 | Sergey | sergey@example.com |  28 | RUS     |   90000 |
|  4 | Andrew | andrew@example.com |  24 | RUS     |   95000 |
|  5 | Bob    | bob@example.com    |  25 | USA     |  100000 |
|  6 | Tom    | tom@example.com    |  29 | USA     |  110000 |
+----+--------+--------------------+-----+---------+---------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM users WHERE age > 26;
+----+--------+--------------------+-----+---------+---------+
| id | name   | email              | age | country | balance |
+----+--------+--------------------+-----+---------+---------+
|  3 | Sergey | sergey@example.com |  28 | RUS     |   90000 |
|  6 | Tom    | tom@example.com    |  29 | USA     |  110000 |
+----+--------+--------------------+-----+---------+---------+
2 rows in set (0.00 sec)

mysql> SELECT * FROM users WHERE age > 26 AND country = 'RUS';
+----+--------+--------------------+-----+---------+---------+
| id | name   | email              | age | country | balance |
+----+--------+--------------------+-----+---------+---------+
|  3 | Sergey | sergey@example.com |  28 | RUS     |   90000 |
+----+--------+--------------------+-----+---------+---------+
1 row in set (0.00 sec)

mysql> SELECT * FROM users;
+----+--------+--------------------+-----+---------+---------+
| id | name   | email              | age | country | balance |
+----+--------+--------------------+-----+---------+---------+
|  1 | Ivan   | ivan@example.com   |  25 | RUS     |  100000 |
|  2 | Gleb   | gleb@exmple.com    |  26 | RUS     |   90000 |
|  3 | Sergey | sergey@example.com |  28 | RUS     |   90000 |
|  4 | Andrew | andrew@example.com |  24 | RUS     |   95000 |
|  5 | Bob    | bob@example.com    |  25 | USA     |  100000 |
|  6 | Tom    | tom@example.com    |  29 | USA     |  110000 |
+----+--------+--------------------+-----+---------+---------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM users ORDER BY balance;
+----+--------+--------------------+-----+---------+---------+
| id | name   | email              | age | country | balance |
+----+--------+--------------------+-----+---------+---------+
|  2 | Gleb   | gleb@exmple.com    |  26 | RUS     |   90000 |
|  3 | Sergey | sergey@example.com |  28 | RUS     |   90000 |
|  4 | Andrew | andrew@example.com |  24 | RUS     |   95000 |
|  1 | Ivan   | ivan@example.com   |  25 | RUS     |  100000 |
|  5 | Bob    | bob@example.com    |  25 | USA     |  100000 |
|  6 | Tom    | tom@example.com    |  29 | USA     |  110000 |
+----+--------+--------------------+-----+---------+---------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM users ORDER BY balance DESC;
+----+--------+--------------------+-----+---------+---------+
| id | name   | email              | age | country | balance |
+----+--------+--------------------+-----+---------+---------+
|  6 | Tom    | tom@example.com    |  29 | USA     |  110000 |
|  1 | Ivan   | ivan@example.com   |  25 | RUS     |  100000 |
|  5 | Bob    | bob@example.com    |  25 | USA     |  100000 |
|  4 | Andrew | andrew@example.com |  24 | RUS     |   95000 |
|  2 | Gleb   | gleb@exmple.com    |  26 | RUS     |   90000 |
|  3 | Sergey | sergey@example.com |  28 | RUS     |   90000 |
+----+--------+--------------------+-----+---------+---------+
6 rows in set (0.00 sec)

mysql> SELECT * FROM users WHERE balance BETWEEN 95000 AND 110000;
+----+--------+--------------------+-----+---------+---------+
| id | name   | email              | age | country | balance |
+----+--------+--------------------+-----+---------+---------+
|  1 | Ivan   | ivan@example.com   |  25 | RUS     |  100000 |
|  4 | Andrew | andrew@example.com |  24 | RUS     |   95000 |
|  5 | Bob    | bob@example.com    |  25 | USA     |  100000 |
|  6 | Tom    | tom@example.com    |  29 | USA     |  110000 |
+----+--------+--------------------+-----+---------+---------+
4 rows in set (0.00 sec)

mysql> SELECT * FROM users;

+----+--------+--------------------+-----+---------+---------+
| id | name   | email              | age | country | balance |
+----+--------+--------------------+-----+---------+---------+
|  1 | Ivan   | ivan@example.com   |  25 | RUS     |  100000 |
|  2 | Gleb   | gleb@exmple.com    |  26 | RUS     |   90000 |
|  3 | Sergey | sergey@example.com |  28 | RUS     |   90000 |
|  4 | Andrew | andrew@example.com |  24 | RUS     |   95000 |
|  5 | Bob    | bob@example.com    |  25 | USA     |  100000 |
|  6 | Tom    | tom@example.com    |  29 | USA     |  110000 |
+----+--------+--------------------+-----+---------+---------+
6 rows in set (0.00 sec)

mysql> SELECT COUNT(*) FROM users WHERE country = 'RUS';
+----------+
| COUNT(*) |
+----------+
|        4 |
+----------+
1 row in set (0.00 sec)

mysql> SELECT COUNT(*) FROM users WHERE country = 'RUS' AND balance = 90000;
+----------+
| COUNT(*) |
+----------+
|        2 |
+----------+
1 row in set (0.00 sec)

mysql> SELECT AVG(balance) FROM users;
+--------------+
| AVG(balance) |
+--------------+
|        97500 |
+--------------+
1 row in set (0.00 sec)

mysql> SELECT SUM(balance) FROM users;
+--------------+
| SUM(balance) |
+--------------+
|       585000 |
+--------------+
1 row in set (0.00 sec)

mysql> SELECT MAX(balance) FROM users;
+--------------+
| MAX(balance) |
+--------------+
|       110000 |
+--------------+
1 row in set (0.00 sec)

mysql> SELECT MIN(balance) FROM users;
+--------------+
| MIN(balance) |
+--------------+
|        90000 |
+--------------+
1 row in set (0.00 sec)
mysql> SELECT * FROM users;

+----+--------+--------------------+-----+---------+---------+
| id | name   | email              | age | country | balance |
+----+--------+--------------------+-----+---------+---------+
|  1 | Ivan   | ivan@example.com   |  25 | RUS     |  100000 |
|  2 | Gleb   | gleb@exmple.com    |  26 | RUS     |   90000 |
|  3 | Sergey | sergey@example.com |  28 | RUS     |   90000 |
|  4 | Andrew | andrew@example.com |  24 | RUS     |   95000 |
|  5 | Bob    | bob@example.com    |  25 | USA     |  100000 |
|  6 | Tom    | tom@example.com    |  29 | USA     |  110000 |
+----+--------+--------------------+-----+---------+---------+
6 rows in set (0.00 sec)

mysql> UPDATE users SET balance = 110000 WHERE id = 2;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM users;

+----+--------+--------------------+-----+---------+---------+
| id | name   | email              | age | country | balance |
+----+--------+--------------------+-----+---------+---------+
|  1 | Ivan   | ivan@example.com   |  25 | RUS     |  100000 |
|  2 | Gleb   | gleb@exmple.com    |  26 | RUS     |  110000 |
|  3 | Sergey | sergey@example.com |  28 | RUS     |   90000 |
|  4 | Andrew | andrew@example.com |  24 | RUS     |   95000 |
|  5 | Bob    | bob@example.com    |  25 | USA     |  100000 |
|  6 | Tom    | tom@example.com    |  29 | USA     |  110000 |
+----+--------+--------------------+-----+---------+---------+
6 rows in set (0.00 sec)

mysql> UPDATE users SET name = 'Ivan';
Query OK, 5 rows affected (0.00 sec)
Rows matched: 6  Changed: 5  Warnings: 0

mysql> SELECT * FROM users;

+----+------+--------------------+-----+---------+---------+
| id | name | email              | age | country | balance |
+----+------+--------------------+-----+---------+---------+
|  1 | Ivan | ivan@example.com   |  25 | RUS     |  100000 |
|  2 | Ivan | gleb@exmple.com    |  26 | RUS     |  110000 |
|  3 | Ivan | sergey@example.com |  28 | RUS     |   90000 |
|  4 | Ivan | andrew@example.com |  24 | RUS     |   95000 |
|  5 | Ivan | bob@example.com    |  25 | USA     |  100000 |
|  6 | Ivan | tom@example.com    |  29 | USA     |  110000 |
+----+------+--------------------+-----+---------+---------+
6 rows in set (0.00 sec)

mysql> UPDATE users set name = 'Gleb' WHERE id = 2;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0

mysql> SELECT * FROM users;

+----+------+--------------------+-----+---------+---------+
| id | name | email              | age | country | balance |
+----+------+--------------------+-----+---------+---------+
|  1 | Ivan | ivan@example.com   |  25 | RUS     |  100000 |
|  2 | Gleb | gleb@exmple.com    |  26 | RUS     |  110000 |
|  3 | Ivan | sergey@example.com |  28 | RUS     |   90000 |
|  4 | Ivan | andrew@example.com |  24 | RUS     |   95000 |
|  5 | Ivan | bob@example.com    |  25 | USA     |  100000 |
|  6 | Ivan | tom@example.com    |  29 | USA     |  110000 |
+----+------+--------------------+-----+---------+---------+
6 rows in set (0.00 sec)
mysql> UPDATE users SET name = 'Sergey' WHERE id = 3;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
mysql> UPDATE users SET name = 'Andrew' WHERE id = 4;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
mysql> UPDATE users SET name = 'Bob' WHERE id = 5;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
mysql> UPDATE users SET name = 'Tom' WHERE id = 6;
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
mysql> SELECT * FROM users;

+----+--------+--------------------+-----+---------+---------+
| id | name   | email              | age | country | balance |
+----+--------+--------------------+-----+---------+---------+
|  1 | Ivan   | ivan@example.com   |  25 | RUS     |  100000 |
|  2 | Gleb   | gleb@exmple.com    |  26 | RUS     |  110000 |
|  3 | Sergey | sergey@example.com |  28 | RUS     |   90000 |
|  4 | Andrew | andrew@example.com |  24 | RUS     |   95000 |
|  5 | Bob    | bob@example.com    |  25 | USA     |  100000 |
|  6 | Tom    | tom@example.com    |  29 | USA     |  110000 |
+----+--------+--------------------+-----+---------+---------+
6 rows in set (0.00 sec)
mysql> DELETE FROM users WHERE id = 5;

Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM users;

+----+--------+--------------------+-----+---------+---------+
| id | name   | email              | age | country | balance |
+----+--------+--------------------+-----+---------+---------+
|  1 | Ivan   | ivan@example.com   |  25 | RUS     |  100000 |
|  2 | Gleb   | gleb@exmple.com    |  26 | RUS     |  110000 |
|  3 | Sergey | sergey@example.com |  28 | RUS     |   90000 |
|  4 | Andrew | andrew@example.com |  24 | RUS     |   95000 |
|  6 | Tom    | tom@example.com    |  29 | USA     |  110000 |
+----+--------+--------------------+-----+---------+---------+
5 rows in set (0.00 sec)




mysql> CREATE TABLE orders (
    -> id INT(11) NOT NULL AUTO_INCREMENT,
    ->  user_id INT(11) NOT NULL,
    -> product_name VARCHAR(50) NOT NULL,
    ->  price FLOAT NOT NULL,
    -> quantity INT(11) NOT NULL,
    -> order_date DATE NOT NULL,
    -> PRIMARY KEY (id),
    -> FOREIGN KEY (user_id) REFERENCES users(id)
    -> );
Query OK, 0 rows affected, 3 warnings (0.02 sec)

mysql> DESCRIBE orders;

+--------------+-------------+------+-----+---------+----------------+
| Field        | Type        | Null | Key | Default | Extra          |
+--------------+-------------+------+-----+---------+----------------+
| id           | int         | NO   | PRI | NULL    | auto_increment |
| user_id      | int         | NO   | MUL | NULL    |                |
| product_name | varchar(50) | NO   |     | NULL    |                |
| price        | float       | NO   |     | NULL    |                |
| quantity     | int         | NO   |     | NULL    |                |
| order_date   | date        | NO   |     | NULL    |                |
+--------------+-------------+------+-----+---------+----------------+

mysql> INSERT INTO orders (user_id, product_name, price, quantity, order_date) VALUES
    -> (1, 'Product A', 10.00, 2, '2023-02-22');
    
Query OK, 1 row affected (0.01 sec)
mysql> SELECT * FROM orders;

+----+---------+--------------+-------+----------+------------+
| id | user_id | product_name | price | quantity | order_date |
+----+---------+--------------+-------+----------+------------+
|  1 |       1 | Product A    |    10 |        2 | 2023-02-22 |
+----+---------+--------------+-------+----------+------------+
1 row in set (0.00 sec)

mysql> INSERT INTO orders (user_id, product_name, price, quantity, order_date) VALUES
    -> (2, 'Product B', 20.00, 1, '2023-02-20'),
    -> (2, 'Product C', 15.00, 3, '2023-02-23'),
    -> (1, 'Product D', 12.00, 2, '2023-02-25'),
    -> (2, 'Product E', 25.00, 1, '2023-02-26');
    
Query OK, 4 rows affected (0.00 sec)
Records: 4  Duplicates: 0  Warnings: 0
mysql> SELECT * FROM orders;

+----+---------+--------------+-------+----------+------------+
| id | user_id | product_name | price | quantity | order_date |
+----+---------+--------------+-------+----------+------------+
|  1 |       1 | Product A    |    10 |        2 | 2023-02-22 |
|  2 |       2 | Product B    |    20 |        1 | 2023-02-20 |
|  3 |       2 | Product C    |    15 |        3 | 2023-02-23 |
|  4 |       1 | Product D    |    12 |        2 | 2023-02-25 |
|  5 |       2 | Product E    |    25 |        1 | 2023-02-26 |
+----+---------+--------------+-------+----------+------------+
5 rows in set (0.00 sec)


Вложенные запросы

Вложенные запросы позволяют использовать результат одного запроса в качестве входных данных 
для другого запроса


mysql> SELECT * FROM orders WHERE user_id = (SELECT id FROM users WHERE name = 'Gleb');
+----+---------+--------------+-------+----------+------------+
| id | user_id | product_name | price | quantity | order_date |
+----+---------+--------------+-------+----------+------------+
|  2 |       2 | Product B    |    20 |        1 | 2023-02-20 |
|  3 |       2 | Product C    |    15 |        3 | 2023-02-23 |
|  5 |       2 | Product E    |    25 |        1 | 2023-02-26 |
+----+---------+--------------+-------+----------+------------+
3 rows in set (0.00 sec)


UNION объединение

UNION используется для объединения двух и более SELECT запросов в один набор результатов


mysql> SELECT id, name, 'user' AS source FROM users
    -> UNION
    -> SELECT id, product_name, 'order' AS source FROM orders;
+----+-----------+--------+
| id | name      | source |
+----+-----------+--------+
|  1 | Ivan      | user   |
|  2 | Gleb      | user   |
|  3 | Sergey    | user   |
|  4 | Andrew    | user   |
|  6 | Tom       | user   |
|  1 | Product A | order  |
|  2 | Product B | order  |
|  3 | Product C | order  |
|  4 | Product D | order  |
|  5 | Product E | order  |
+----+-----------+--------+
10 rows in set (0.00 sec)


INNER JOIN - это тип объединения, который выбирает только те строки, 
которые имеют соответствующие значения в обеих таблицах.

INNER JOIN соединяет строки из левой таблицы с теми, 
которые имеют соответствующие значения в таблице справа.


Синтаксис запроса INNER JOIN:

SELECT *
FROM table1
INNER JOIN table2
ON table1.column = table2.column;

Здесь table1 и table2 - имена таблиц, а column - название столбцов, 
которые используются для объединения 2-х таблиц.

mysql> SELECT users.name, users.email, orders.product_name, orders.order_date
    -> FROM users
    -> INNER JOIN orders
    -> ON users.id = orders.user_id;
    
+------+------------------+--------------+------------+
| name | email            | product_name | order_date |
+------+------------------+--------------+------------+
| Ivan | ivan@example.com | Product A    | 2023-02-22 |
| Gleb | gleb@exmple.com  | Product B    | 2023-02-20 |
| Gleb | gleb@exmple.com  | Product C    | 2023-02-23 |
| Ivan | ivan@example.com | Product D    | 2023-02-25 |
| Gleb | gleb@exmple.com  | Product E    | 2023-02-26 |
+------+------------------+--------------+------------+
5 rows in set (0.00 sec)

LEFT JOIN - это тип объединения, который выбирает все строки из левой таблицы,
а также вернет строки из правой таблицы.

Если в правой таблице нет соответствующих строк, 
то в результате будут возвращены значения NULL


Синтаксис запроса LEFT JOIN:

SELECT *
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;

Здесь table1 и table2 - имена таблиц, а column - название столбцов, 
которые используются для объединения 2-х таблиц.
 
SELECT users.name, users.email, orders.product_name, orders.order_date
    -> FROM users
    -> LEFT JOIN orders
    -> ON users.id = orders.user_id;
    
+--------+--------------------+--------------+------------+
| name   | email              | product_name | order_date |
+--------+--------------------+--------------+------------+
| Ivan   | ivan@example.com   | Product A    | 2023-02-22 |
| Ivan   | ivan@example.com   | Product D    | 2023-02-25 |
| Gleb   | gleb@exmple.com    | Product B    | 2023-02-20 |
| Gleb   | gleb@exmple.com    | Product C    | 2023-02-23 |
| Gleb   | gleb@exmple.com    | Product E    | 2023-02-26 |
| Sergey | sergey@example.com | NULL         | NULL       |
| Andrew | andrew@example.com | NULL         | NULL       |
| Tom    | tom@example.com    | NULL         | NULL       |
+--------+--------------------+--------------+------------+

8 rows in set (0.00 sec)
```
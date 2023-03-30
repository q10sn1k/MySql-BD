```
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
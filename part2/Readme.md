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
```

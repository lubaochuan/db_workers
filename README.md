# Workers Database
source https://www.techbeamers.com/sql-query-questions-answers-for-practice/

The following set of SQL practice questions is based on a Worker's database. The schema is as follows and you can find the [sample data](sample_data.md) in the "CIS3323" database.
 
## Schema
* Worker(WORKER_ID, FIRST_NAME, LAST_NAME, SALARY, JOINING_DATE, DEPARTMENT)
* Title(WORKER_REF_ID, WORKER_TITLE, AFFECTED_FROM)
* Bonus(WORKER_REF_ID, BONUS_AMOUNT, BONUS_DATE)
```
MariaDB [CIS3323]> desc Worker;
+--------------+----------+------+-----+---------+----------------+
| Field        | Type     | Null | Key | Default | Extra          |
+--------------+----------+------+-----+---------+----------------+
| WORKER_ID    | int(11)  | NO   | PRI | NULL    | auto_increment |
| FIRST_NAME   | char(25) | YES  |     | NULL    |                |
| LAST_NAME    | char(25) | YES  |     | NULL    |                |
| SALARY       | int(15)  | YES  |     | NULL    |                |
| JOINING_DATE | datetime | YES  |     | NULL    |                |
| DEPARTMENT   | char(25) | YES  |     | NULL    |                |
+--------------+----------+------+-----+---------+----------------+
6 rows in set (0.01 sec)

MariaDB [CIS3323]> desc Title;
+---------------+----------+------+-----+---------+-------+
| Field         | Type     | Null | Key | Default | Extra |
+---------------+----------+------+-----+---------+-------+
| WORKER_REF_ID | int(11)  | YES  | MUL | NULL    |       |
| WORKER_TITLE  | char(25) | YES  |     | NULL    |       |
| AFFECTED_FROM | datetime | YES  |     | NULL    |       |
+---------------+----------+------+-----+---------+-------+
3 rows in set (0.00 sec)

MariaDB [CIS3323]> desc Bonus;
+---------------+----------+------+-----+---------+-------+
| Field         | Type     | Null | Key | Default | Extra |
+---------------+----------+------+-----+---------+-------+
| WORKER_REF_ID | int(11)  | YES  | MUL | NULL    |       |
| BONUS_AMOUNT  | int(10)  | YES  |     | NULL    |       |
| BONUS_DATE    | datetime | YES  |     | NULL    |       |
+---------------+----------+------+-----+---------+-------+
3 rows in set (0.01 sec)
```

## Queries
1. Write An SQL query to fetch "FIRST_NAME" from Worker table using the alias name as "WORKER_NAME".
```
+-------------+
| WORKER_NAME |
+-------------+
| Monika      |
| Niharika    |
| Vishal      |
| Amitabh     |
| Vivek       |
| Vipul       |
| Satish      |
| Geetika     |
+-------------+
8 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT FIRST_NAME AS WORKER_NAME
FROM Worker;
```
</details>

2. Write an SQL query to fetch unique values of DEPARTMENT from Worker table.
```
+------------+
| DEPARTMENT |
+------------+
| HR         |
| Admin      |
| Account    |
+------------+
3 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT DISTINCT DEPARTMENT
FROME Worker;
```
</details>

3. Write an SQL query to print the FIRST_NAME and LAST_NAME from Worker table into a single column COMPLETE_NAME. A space char should separate them.
```

+-----------------+
| COMPLETE_NAME   |
+-----------------+
| Monika Arora    |
| Niharika Verma  |
| Vishal Singhal  |
| Amitabh Singh   |
| Vivek Bhati     |
| Vipul Diwan     |
| Satish Kumar    |
| Geetika Chauhan |
+-----------------+
8 rows in set (0.01 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT CONCAT(FIRST_NAME, ' ', LAST_NAME) AS 'COMPLETE_NAME'
FROM Worker;
```
</details>

4. Write an SQL query to print all worker details from the Worker table order by FIRST_NAME ascending.
```
+-----------+------------+-----------+--------+---------------------+------------+
| WORKER_ID | FIRST_NAME | LAST_NAME | SALARY | JOINING_DATE        | DEPARTMENT |
+-----------+------------+-----------+--------+---------------------+------------+
|         4 | Amitabh    | Singh     | 500000 | 2014-02-20 09:00:00 | Admin      |
|         8 | Geetika    | Chauhan   |  90000 | 2014-04-11 09:00:00 | Admin      |
|         1 | Monika     | Arora     | 100000 | 2014-02-20 09:00:00 | HR         |
|         2 | Niharika   | Verma     |  80000 | 2014-06-11 09:00:00 | Admin      |
|         7 | Satish     | Kumar     |  75000 | 2014-01-20 09:00:00 | Account    |
|         6 | Vipul      | Diwan     | 200000 | 2014-06-11 09:00:00 | Account    |
|         3 | Vishal     | Singhal   | 300000 | 2014-02-20 09:00:00 | HR         |
|         5 | Vivek      | Bhati     | 500000 | 2014-06-11 09:00:00 | Admin      |
+-----------+------------+-----------+--------+---------------------+------------+
8 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT *
FROM Worker
ORDER BY FIRST_NAME ASC;
```
</details>

5. Write an SQL query to print all worker details from the Worker table order by DEPARTMENT descending and FIRST_NAME ascending.
```
+-----------+------------+-----------+--------+---------------------+------------+
| WORKER_ID | FIRST_NAME | LAST_NAME | SALARY | JOINING_DATE        | DEPARTMENT |
+-----------+------------+-----------+--------+---------------------+------------+
|         1 | Monika     | Arora     | 100000 | 2014-02-20 09:00:00 | HR         |
|         3 | Vishal     | Singhal   | 300000 | 2014-02-20 09:00:00 | HR         |
|         4 | Amitabh    | Singh     | 500000 | 2014-02-20 09:00:00 | Admin      |
|         8 | Geetika    | Chauhan   |  90000 | 2014-04-11 09:00:00 | Admin      |
|         2 | Niharika   | Verma     |  80000 | 2014-06-11 09:00:00 | Admin      |
|         5 | Vivek      | Bhati     | 500000 | 2014-06-11 09:00:00 | Admin      |
|         7 | Satish     | Kumar     |  75000 | 2014-01-20 09:00:00 | Account    |
|         6 | Vipul      | Diwan     | 200000 | 2014-06-11 09:00:00 | Account    |
+-----------+------------+-----------+--------+---------------------+------------+
8 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT *
FROM Worker
ORDER BY DEPARTMENT DESC, FIRST_NAME ASC;
```
</details>

6. Write an SQL query to print details for Workers with the first name as "Vipul" And "Satish" from Worker table.
```
+-----------+------------+-----------+--------+---------------------+------------+
| WORKER_ID | FIRST_NAME | LAST_NAME | SALARY | JOINING_DATE        | DEPARTMENT |
+-----------+------------+-----------+--------+---------------------+------------+
|         6 | Vipul      | Diwan     | 200000 | 2014-06-11 09:00:00 | Account    |
|         7 | Satish     | Kumar     |  75000 | 2014-01-20 09:00:00 | Account    |
+-----------+------------+-----------+--------+---------------------+------------+
2 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT *
FROM Worker
WHERE FIRST_NAME in ('Vipul','Satish');
```
</details>

7. Write an SQL query to print details of Workers with DEPARTMENT name that  starts with "Admin".
```
+-----------+------------+-----------+--------+---------------------+------------+
| WORKER_ID | FIRST_NAME | LAST_NAME | SALARY | JOINING_DATE        | DEPARTMENT |
+-----------+------------+-----------+--------+---------------------+------------+
|         2 | Niharika   | Verma     |  80000 | 2014-06-11 09:00:00 | Admin      |
|         4 | Amitabh    | Singh     | 500000 | 2014-02-20 09:00:00 | Admin      |
|         5 | Vivek      | Bhati     | 500000 | 2014-06-11 09:00:00 | Admin      |
|         8 | Geetika    | Chauhan   |  90000 | 2014-04-11 09:00:00 | Admin      |
+-----------+------------+-----------+--------+---------------------+------------+
4 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT *
FROM Worker
WHERE DEPARTMENT LIKE 'Admin%';
```
</details>

8. Write an SQL query to print details of the workers whose FIRST_NAME ends with 'h' and contains six letters.
```
+-----------+------------+-----------+--------+---------------------+------------+
| WORKER_ID | FIRST_NAME | LAST_NAME | SALARY | JOINING_DATE        | DEPARTMENT |
+-----------+------------+-----------+--------+---------------------+------------+
|         7 | Satish     | Kumar     |  75000 | 2014-01-20 09:00:00 | Account    |
+-----------+------------+-----------+--------+---------------------+------------+
1 row in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT *
FROM Worker
WHERE FIRST_NAME LIKE '_____h';
```
</details>

9. Write an SQL query to print details of the workers whose SALARY lies between 100000 And 500000.
```
+-----------+------------+-----------+--------+---------------------+------------+
| WORKER_ID | FIRST_NAME | LAST_NAME | SALARY | JOINING_DATE        | DEPARTMENT |
+-----------+------------+-----------+--------+---------------------+------------+
|         1 | Monika     | Arora     | 100000 | 2014-02-20 09:00:00 | HR         |
|         3 | Vishal     | Singhal   | 300000 | 2014-02-20 09:00:00 | HR         |
|         4 | Amitabh    | Singh     | 500000 | 2014-02-20 09:00:00 | Admin      |
|         5 | Vivek      | Bhati     | 500000 | 2014-06-11 09:00:00 | Admin      |
|         6 | Vipul      | Diwan     | 200000 | 2014-06-11 09:00:00 | Account    |
+-----------+------------+-----------+--------+---------------------+------------+
5 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT *
FROM Worker
WHERE SALARY BETWEEN 100000 AND 500000;
```
</details>

10. Write an SQL query to print details of the workers who have joined in Feb  2014.
```
| WORKER_ID | FIRST_NAME | LAST_NAME | SALARY | JOINING_DATE        | DEPARTMENT |
+-----------+------------+-----------+--------+---------------------+------------+
|         1 | Monika     | Arora     | 100000 | 2014-02-20 09:00:00 | HR         |
|         3 | Vishal     | Singhal   | 300000 | 2014-02-20 09:00:00 | HR         |
|         4 | Amitabh    | Singh     | 500000 | 2014-02-20 09:00:00 | Admin      |
+-----------+------------+-----------+--------+---------------------+------------+
3 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT *
FROM Worker
WHERE year(JOINING_DATE) = 2014
  AND month(JOINING_DATE) = 2;
```
</details>

11. Write an SQL query to fetch the count of workers working in the department 'Admin'.
```
+----------+
| COUNT(*) |
+----------+
|        4 |
+----------+
1 row in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT COUNT(*)
FROM Worker
WHERE DEPARTMENT = 'Admin';
```
</details>

12. Write an SQL query to fetch the count of workers for each department in the descending order.
```
+------------+---------------+
| DEPARTMENT | No_Of_Workers |
+------------+---------------+
| Admin      |             4 |
| HR         |             2 |
| Account    |             2 |
+------------+---------------+
3 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT DEPARTMENT, count(WORKER_ID) No_Of_Workers
FROM Worker
GROUP BY DEPARTMENT
ORDER BY No_Of_Workers DESC;
```
</details>

13. Write an SQL query to print details of the workers who are also managers.
```
+------------+--------------+
| FIRST_NAME | WORKER_TITLE |
+------------+--------------+
| Monika     | Manager      |
| Vivek      | Manager      |
+------------+--------------+
2 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT DISTINCT W.FIRST_NAME, T.WORKER_TITLE
FROM Worker W INNER JOIN Title T
  ON W.WORKER_ID = T.WORKER_REF_ID
AND T.WORKER_TITLE = 'Manager';
```
</details>

14. Write an SQL query to fetch duplicate worker records having matching "WORKER_TITLE" and "AFFECTED_FROM" fields.
```
+--------------+---------------------+----------+
| WORKER_TITLE | AFFECTED_FROM       | COUNT(*) |
+--------------+---------------------+----------+
| Executive    | 2016-06-11 00:00:00 |        3 |
| Lead         | 2016-06-11 00:00:00 |        2 |
+--------------+---------------------+----------+
2 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT WORKER_TITLE, AFFECTED_FROM, COUNT(*)
FROM Title
GROUP BY WORKER_TITLE, AFFECTED_FROM
HAVING COUNT(*) > 1;
```
</details>

15. Write an SQL query to fetch the list of workers with the same salary.
```
+-----------+------------+--------+
| WORKER_ID | FIRST_NAME | Salary |
+-----------+------------+--------+
|         5 | Vivek      | 500000 |
|         4 | Amitabh    | 500000 |
+-----------+------------+--------+
2 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT distinct W.WORKER_ID, W.FIRST_NAME, W.Salary
FROM Worker W, Worker W1
WHERE W.Salary = W1.Salary
AND W.WORKER_ID != W1.WORKER_ID;
```
</details>

16. Write an SQL query to show the second highest salary.
```
+-------------+
| max(Salary) |
+-------------+
|      300000 |
+-------------+
1 row in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT max(Salary)
FROM Worker
WHERE Salary not in
  (SELECT max(Salary) FROM Worker);
```
</details>

17. Write an SQL query to fetch the departments that have less than five people in it.
```
+------------+-------------------+
| DEPARTMENT | Number of Workers |
+------------+-------------------+
| Account    |                 2 |
| Admin      |                 4 |
| HR         |                 2 |
+------------+-------------------+
3 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT DEPARTMENT, COUNT(WORKER_ID) as 'Number of Workers'
FROM Worker
GROUP BY DEPARTMENT
HAVING COUNT(WORKER_ID) < 5;
```
</details>

18. Write an SQL query to print the name of workers having the highest salary in each department.
```+------------+------------+--------+
| DEPARTMENT | FIRST_NAME | Salary |
+------------+------------+--------+
| HR         | Vishal     | 300000 |
| Admin      | Amitabh    | 500000 |
| Admin      | Vivek      | 500000 |
| Account    | Vipul      | 200000 |
+------------+------------+--------+
4 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT t.DEPARTMENT, t.FIRST_NAME, t.Salary
FROM
  (SELECT max(Salary) AS HighestSalary, DEPARTMENT
   FROM Worker
   GROUP BY DEPARTMENT) AS Highest
  INNER JOIN
  Worker t
  ON Highest.DEPARTMENT=t.DEPARTMENT and Highest.HighestSalary=t.Salary;
```
</details>

19. Write an SQL query to fetch departments along with the total salaries paid for each of them.
```
+------------+-------------+
| DEPARTMENT | sum(Salary) |
+------------+-------------+
| Account    |      275000 |
| Admin      |     1170000 |
| HR         |      400000 |
+------------+-------------+
3 rows in set (0.00 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT DEPARTMENT, sum(Salary)
FROM Worker
GROUP BY DEPARTMENT;
```
</details>

20. Write an SQL query to fetch Nth (e.g. 4th) max salary.
```
+--------+
| Salary |
+--------+
| 500000 |
| 300000 |
| 200000 |
| 100000 |
+--------+
4 rows in set (0.01 sec)
```
<details>
<summary>answer</summary>

```sql
SELECT distinct Salary
FROM Worker a 
WHERE 4 >=
  (SELECT count(distinct Salary)
  FROM Worker b
  WHERE a.Salary <= b.Salary)
ORDER BY a.Salary desc;
```
</details>

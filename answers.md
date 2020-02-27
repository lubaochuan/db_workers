1.
```
SELECT FIRST_NAME AS WORKER_NAME
FROM Worker;
```

2.
```
SELECT DISTINCT DEPARTMENT
FROME Worker;
```

3.
```
SELECT CONCAT(FIRST_NAME, ' ', LAST_NAME) AS 'COMPLETE_NAME'
FROM Worker;
```

4.
```
SELECT *
FROM Worker
ORDER BY FIRST_NAME ASC;
```

5.
```
SELECT *
FROM Worker
ORDER BY DEPARTMENT DESC, FIRST_NAME ASC;
```

6.
```
SELECT *
FROM Worker
WHERE FIRST_NAME in ('Vipul','Satish');
```

7.
```
SELECT *
FROM Worker
WHERE DEPARTMENT LIKE 'Admin%';
```

8.
```
SELECT *
FROM Worker
WHERE FIRST_NAME LIKE '_____h';
```

9.
```
SELECT *
FROM Worker
WHERE SALARY BETWEEN 100000 AND 500000;
```

10.
```
MariaDB [CIS3323]> select now();
+---------------------+
| now()               |
+---------------------+
| 2020-02-27 09:25:03 |
+---------------------+
1 row in set (0.00 sec)

MariaDB [CIS3323]> select year(now());
+-------------+
| year(now()) |
+-------------+
|        2020 |
+-------------+
1 row in set (0.00 sec)

MariaDB [CIS3323]> select hour(now());
+-------------+
| hour(now()) |
+-------------+
|          10 |
+-------------+
1 row in set (0.00 sec)

MariaDB [CIS3323]> select minute(now());
+---------------+
| minute(now()) |
+---------------+
|            41 |
+---------------+
1 row in set (0.00 sec)

MariaDB [CIS3323]> select second(now());
+---------------+
| second(now()) |
+---------------+
|            15 |
+---------------+
1 row in set (0.00 sec)

SELECT *
FROM Worker
WHERE year(JOINING_DATE) = 2014
  AND month(JOINING_DATE) = 2;
```

11.
```
SELECT COUNT(*)
FROM Worker
WHERE DEPARTMENT = 'Admin';
```

12.
```
SELECT DEPARTMENT, count(WORKER_ID) No_Of_Workers
FROM Worker
GROUP BY DEPARTMENT
ORDER BY No_Of_Workers DESC;
```

13.
```
SELECT DISTINCT W.FIRST_NAME, T.WORKER_TITLE
FROM Worker W INNER JOIN Title T
  ON W.WORKER_ID = T.WORKER_REF_ID
AND T.WORKER_TITLE = 'Manager';
```

14.
```
SELECT WORKER_TITLE, AFFECTED_FROM, COUNT(*)
FROM Title
GROUP BY WORKER_TITLE, AFFECTED_FROM
HAVING COUNT(*) > 1;
```

15.
```
SELECT distinct W.WORKER_ID, W.FIRST_NAME, W.Salary
FROM Worker W, Worker W1
WHERE W.Salary = W1.Salary
AND W.WORKER_ID != W1.WORKER_ID;
```

16.
```
SELECT max(Salary)
FROM Worker
WHERE Salary not in
  (SELECT max(Salary) FROM Worker);
```

17.
```
SELECT DEPARTMENT, COUNT(WORKER_ID) as 'Number of Workers'
FROM Worker
GROUP BY DEPARTMENT
HAVING COUNT(WORKER_ID) < 5;
```

18.
```
SELECT t.DEPARTMENT, t.FIRST_NAME, t.Salary
FROM
  (SELECT max(Salary) AS HighestSalary, DEPARTMENT
   FROM Worker
   GROUP BY DEPARTMENT) AS Highest
  INNER JOIN
  Worker t
  ON Highest.DEPARTMENT=t.DEPARTMENT and Highest.HighestSalary=t.Salary;
```

19.
```
SELECT DEPARTMENT, sum(Salary)
FROM Worker
GROUP BY DEPARTMENT;
```

20.
```
SELECT distinct Salary
FROM Worker a 
WHERE 4 >=
  (SELECT count(distinct Salary)
  FROM Worker b
  WHERE a.Salary <= b.Salary)
ORDER BY a.Salary desc;
```

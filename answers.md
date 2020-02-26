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


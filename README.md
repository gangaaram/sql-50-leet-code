# SQL 50 — LeetCode Solutions

Solutions to the [SQL 50 Study Plan](https://leetcode.com/studyplan/top-sql-50/) on LeetCode.

A collection of SQL queries covering filtering, aggregation, joins, subqueries, CTEs, window functions, and other common SQL concepts.

---

### 01. Recyclable and Low Fat Products

[LeetCode #1757](https://leetcode.com/problems/recyclable-and-low-fat-products/)

```sql
SELECT product_id FROM Products
WHERE low_fats ="Y" AND recyclable="Y";
```

### 02. Find Customer Referee

[LeetCode #584](https://leetcode.com/problems/find-customer-referee/)

```sql
SELECT name FROM Customer
WHERE referee_id!=2 OR referee_id IS NULL;
```

### 03. Big Countries

[LeetCode #595](https://leetcode.com/problems/big-countries/)

```sql
SELECT name, population, area FROM World
WHERE area>=3000000 OR population >=25000000;
```

### 04. Article Views I

[LeetCode #1148](https://leetcode.com/problems/articles-views-i/)

```sql
SELECT DISTINCT author_id as id FROM Views
WHERE author_id=viewer_id
ORDER BY id ASC;
```

### 05. Invalid Tweets

[LeetCode #1683](https://leetcode.com/problems/invalid-tweets/)

```sql
SELECT tweet_id FROM Tweets
WHERE length(content) > 15;
```

### 06. Replace Employee ID With The Unique Identifier

[LeetCode #1378](https://leetcode.com/problems/replace-employee-id-with-the-unique-identifier/)

```sql
SELECT unique_id, name FROM Employees E
LEFT JOIN EmployeeUNI EU ON E.id=EU.id;
```

### 07. Product Sales Analysis I

[LeetCode #1068](https://leetcode.com/problems/product-sales-analysis-i/)

```sql
SELECT product_name, year, price FROM Sales s
LEFT JOIN Product p on S.product_id=P.product_id;
```

### 08. Customer Who Visited but Did Not Make Any Transactions

[LeetCode #1581](https://leetcode.com/problems/customer-who-visited-but-did-not-make-any-transactions/)

```sql
SELECT customer_id, COUNT(customer_id) as count_no_trans FROM Visits v
LEFT JOIN Transactions t on v.visit_id=t.visit_id
WHERE transaction_id IS NULL
GROUP BY customer_id;
```

### 09. Rising Temperature

[LeetCode #197](https://leetcode.com/problems/rising-temperature/)

```sql
SELECT w2.id FROM Weather w1
LEFT JOIN Weather w2
ON w1.recordDate= DATE_SUB(w2.recordDate, INTERVAL 1 DAY)
WHERE w2.temperature>w1.temperature;
```

### 10. Average Time of Process per Machine

[LeetCode #1661](https://leetcode.com/average-time-of-process-per-machine/)

```sql
SELECT a1.machine_id, ROUND(AVG(a2.timestamp-a1.timestamp),3) AS processing_time FROM Activity a1
LEFT JOIN Activity a2
ON a1.machine_id=a2.machine_id AND a1.process_id=a2.process_id AND a1.activity_type='start' AND a2.activity_type='end'
GROUP BY a1.machine_id;
```

### 11. Employee Bonus

[LeetCode #577](https://leetcode.com/employee-bonus/)

```sql
SELECT name, bonus FROM Employee e
LEFT JOIN Bonus b on e.empId=b.empId
WHERE bonus<1000 OR bonus IS NULL;
```

### 12. Students and Examinations

[LeetCode #1280](https://leetcode.com/students-and-examinations/)

```sql
SELECT name, bonus FROM Employee e
LEFT JOIN Bonus b on e.empId=b.empId
WHERE bonus<1000 OR bonus IS NULL;
```

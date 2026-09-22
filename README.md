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
SELECT st.student_id,st.student_name,s.subject_name, COUNT(e.subject_name) AS attended_exams FROM Students st
CROSS JOIN Subjects s
LEFT JOIN Examinations e
ON st.student_id=e.student_id AND s.subject_name=e.subject_name
GROUP BY st.student_id,st.student_name,s.subject_name
ORDER BY st.student_id, s.subject_name;
```

### 13. Managers with at Least 5 Direct Reports

[LeetCode #570](https://leetcode.com/managers-with-at-least-5-direct-reports/)

```sql
SELECT e.name FROM Employee e
CROSS JOIN Employee e2
WHERE e.id=e2.managerId 
GROUP BY e.name,e.id
HAVING COUNT(e.id)>=5;
```

### 14. Confirmation Rate

[LeetCode #1934](https://leetcode.com/confirmation-rate/)

```sql
SELECT s.user_id, ROUND(AVG(IF(c.action='confirmed',1,0)),2) AS confirmation_rate FROM Signups s
LEFT JOIN Confirmations c
ON s.user_id=c.user_id
GROUP BY s.user_id;
```
### 15. Not Boring Movies

[LeetCode #620](https://leetcode.com/not-boring-movies/)

```sql
SELECT * FROM Cinema
WHERE id%2!=0 AND description !='boring'
ORDER BY rating DESC;
```

### 16. Average Selling Price

[LeetCode #1251](https://leetcode.com/average-selling-price/)

```sql
SELECT p.product_id, IFNULL(ROUND(SUM(units*price)/SUM(units),2),0) AS average_price FROM Prices p
LEFT JOIN UnitsSold u
ON (p.product_id=u.product_id) AND (u.purchase_date BETWEEN start_date AND end_date)
GROUP BY p.product_id;
```

### 17. Project Employees I

[LeetCode #1075](https://leetcode.com/project-employees-i/)

```sql
SELECT p.project_id, ROUND(AVG(experience_years),2) AS average_years FROM Project p
LEFT JOIN Employee e
ON p.employee_id = e.employee_id
GROUP BY p.project_id;
```

### 18. Percentage of users Attended a Contest

[LeetCode #1633](https://leetcode.com/percentage-of-users-attended-a-contest)

```sql
SELECT contest_id, ROUND(COUNT(user_id)/(SELECT COUNT(user_id)FROM Users)*100,2) AS percentage FROM Register
GROUP BY contest_id
ORDER BY percentage DESC, contest_id ASC;
```

### 19. Queries Quality and Percentage

[LeetCode #1211](https://leetcode.com/queries-quality-and-percentage)

```sql
SELECT query_name, ROUND(AVG(rating/position),2) AS quality,
ROUND(SUM(IF(rating<3,1,0))/COUNT(result)*100,2) AS poor_query_percentage
FROM Queries
GROUP BY query_name;
```

### 20. Monthly Transactions I

[LeetCode #1193](https://leetcode.com/monthly-transactions-i)

```sql
SELECT LEFT(trans_date,7) AS month, country, COUNT(id) AS trans_count,
SUM(IF(state='approved',1,0)) AS approved_count,
SUM(amount) AS trans_total_amount,
SUM(IF(state='approved',amount,0)) AS approved_total_amount
FROM Transactions
GROUP BY month, Country;
```

### 21. Immediate Food Delivery II

[LeetCode #1174](https://leetcode.com/immediate-food-delivery-ii)

```sql
SELECT ROUND(COUNT(IF(order_date=customer_pref_delivery_date,1,NULL))/COUNT(customer_id)*100,2) AS immediate_percentage FROM Delivery
WHERE (customer_id,order_date) IN (
SELECT customer_id, MIN(order_date) AS order_date 
FROM Delivery
GROUP BY customer_id
);
```

### 22. Game Play Analysis IV

[LeetCode #550](https://leetcode.com/game-play-analysis-iv/)

```sql
SELECT ROUND(COUNT(a.player_id)/(SELECT COUNT(DISTINCT player_id) FROM Activity),2) AS fraction FROM Activity a LEFT JOIN
(
SELECT player_id, MIN(event_date) AS event_date FROM Activity 
GROUP BY player_id
) aa ON a.player_id=aa.player_id
WHERE a.event_date=DATE_ADD(aa.event_date, INTERVAL 1 day);
```

### 23. Number of Unique Subjects Taught by Each Teacher

[LeetCode #2356](https://leetcode.com/number-of-unique-subjects-taught-by-each-teacher/)

```sql
SELECT teacher_id, COUNT(DISTINCT subject_id) AS cnt FROM Teacher
GROUP BY teacher_id;
```

### 24. User Activity for the Past 30 Days I

[LeetCode #1141](https://leetcode.com/user-activity-for-the-past-30-days-i/)

```sql
SELECT activity_date as day, COUNT(DISTINCT user_id) AS active_users FROM Activity
WHERE activity_date BETWEEN DATE_SUB('2019-07-27', INTERVAL 29 DAY) AND '2019-07-27'
GROUP BY activity_date;
```

### 25. Product Sales Analysis III

[LeetCode #1070](https://leetcode.com/product-sales-analysis-iii)

```sql
SELECT product_id, year AS first_year, quantity, price FROM Sales 
WHERE (product_id, year) IN (
SELECT product_id, MIN(year) AS year FROM Sales
GROUP BY product_id
);
```

### 26. Classes With at Least 5 students

[LeetCode #596](https://leetcode.com/classes-with-at-least-5-students/)

```sql
SELECT class FROM Courses
GROUP BY class
HAVING COUNT(student) >=5;
```

### 27. Find Followers Count

[LeetCode #1729](https://leetcode.com/find-followers-count/)

```sql
SELECT user_id,COUNT(follower_id) AS followers_count FROM Followers
GROUP BY user_id
ORDER BY user_id ASC;
```

### 28. Biggest Single Number

[LeetCode #619](https://leetcode.com/biggest-single-number/)

```sql
SELECT MAX(num) AS num FROM(
SELECT num FROM MyNumbers
GROUP BY num
HAVING COUNT(num) =1
) a;
```

### 29. Customers Who Bought All Products

[LeetCode #1045](https://leetcode.com/customers-who-bought-all-products/)

```sql
SELECT customer_id FROM Customer c
GROUP BY c.customer_id
HAVING COUNT(DISTINCT c.product_key)=(SELECT COUNT(*) FROM Product);
```

### 30. The Number of Employees Which Report to Each Employee

[LeetCode #1731](https://leetcode.com/the-number-of-employees-which-report-to-each-employee/)

```sql
SELECT e.employee_id, e.name, COUNT(*) AS reports_count, ROUND(AVG(ee.age),0) AS average_age FROM Employees e
LEFT JOIN Employees ee
ON ee.reports_to=e.employee_id
WHERE ee.reports_to IS NOT NULL
GROUP BY e.employee_id
ORDER BY e.employee_id;
```

### 31. Primary Department for Each Employee

[LeetCode #1789](https://leetcode.com/primary-department-for-each-employee/)

```sql
SELECT employee_id, department_id
FROM Employee
WHERE primary_flag='Y' OR employee_id IN (
    SELECT employee_id FROM Employee
    GROUP BY employee_id
    HAVING COUNT(*)=1
);
```

### 32. Triangle Judgement

[LeetCode #610](https://leetcode.com/triangle-judgement/)

```sql
SELECT *, IF(x+y>z AND x+z>y AND y+z>x, 'Yes', 'No') AS triangle FROM Triangle;
```

### 33. Consecutive Numbers

[LeetCode #180](https://leetcode.com/consecutive-numbers/)

```sql
SELECT DISTINCT(IF(l.num=ll.num AND l.num=lll.num AND ll.num=lll.num,l.num,NULL)) AS ConsecutiveNums FROM Logs l
LEFT JOIN Logs ll
ON l.id=ll.id-1
LEFT JOIN Logs lll
ON l.id=lll.id-2
HAVING ConsecutiveNums IS NOT NULL;
```

### 34. Product Price at a Given Date

[LeetCode #1164](https://leetcode.com/product-price-at-a-given-date/)
```sql
SELECT product_id, 10 AS price FROM Products
GROUP BY product_id
HAVING MIN(change_date) > '2019-08-16'
UNION
SELECT product_id, new_price FROM products
WHERE (product_id,change_date) IN (
    SELECT product_id, MAX(change_date) AS change_date FROM products
WHERE change_date<='2019-08-16'
GROUP BY product_id
)
```

### 35. Last Person to Fit in the Bus

[LeetCode #1204](https://leetcode.com/last-person-to-fit-in-the-bus/)
```sql
SELECT q.person_name FROM Queue q 
LEFT JOIN Queue qq ON q.turn >= qq.turn
GROUP BY q.turn
HAVING SUM(qq.weight) <= 1000
ORDER BY sum(qq.weight) DESC
LIMIT 1;

OR

SELECT person_name FROM (
SELECT person_name, SUM(weight) OVER(ORDER BY turn) AS total_weight
FROM Queue
) a WHERE total_weight<=1000
ORDER BY total_weight DESC
LIMIT 1;
```
### 35. Last Person to Fit in the Bus

[LeetCode #1204](https://leetcode.com/last-person-to-fit-in-the-bus/)
```sql
SELECT q.person_name FROM Queue q 
LEFT JOIN Queue qq ON q.turn >= qq.turn
GROUP BY q.turn
HAVING SUM(qq.weight) <= 1000
ORDER BY sum(qq.weight) DESC
LIMIT 1;

OR

SELECT person_name FROM (
SELECT person_name, SUM(weight) OVER(ORDER BY turn) AS total_weight
FROM Queue
) a WHERE total_weight<=1000
ORDER BY total_weight DESC
LIMIT 1;
```
### 35. Last Person to Fit in the Bus

[LeetCode #1204](https://leetcode.com/last-person-to-fit-in-the-bus/)
```sql
SELECT q.person_name FROM Queue q 
LEFT JOIN Queue qq ON q.turn >= qq.turn
GROUP BY q.turn
HAVING SUM(qq.weight) <= 1000
ORDER BY sum(qq.weight) DESC
LIMIT 1;

OR

SELECT person_name FROM (
SELECT person_name, SUM(weight) OVER(ORDER BY turn) AS total_weight
FROM Queue
) a WHERE total_weight<=1000
ORDER BY total_weight DESC
LIMIT 1;
```

### 36. Count Salary Categories

[LeetCode #1907](https://leetcode.com/count-salary-categories/)
```sql
SELECT "Low Salary" AS category, SUM(income<20000) AS accounts_count FROM Accounts
UNION ALL
SELECT "Average Salary" AS category, SUM(income BETWEEN 20000 AND 50000) AS accounts_count FROM Accounts
UNION ALL
SELECT "High Salary" AS category, SUM(income> 50000) AS accounts_count FROM Accounts
```

### 37. Employees Whose Manager Left the Company

[LeetCode #1978](https://leetcode.com/employees-whose-manager-left-the-company/)
```sql
SELECT employee_id FROM Employees
WHERE manager_id IS NOT NULL AND manager_id NOT IN (SELECT employee_id from Employees) AND salary<30000
ORDER BY employee_id
```

### 38. Exchange Seats

[LeetCode #626](https://leetcode.com/exchange-seats/)
```sql
SELECT 
CASE
    WHEN id%2=1 AND id+1 IN (SELECT id FROM Seat) THEN id+1
    WHEN id%2=0 THEN id-1
    ELSE id
END AS id, student
FROM Seat
ORDER BY id
```

### 39. Movie Rating

[LeetCode #626](https://leetcode.com/movie-rating/)
```sql
(SELECT name AS results FROM MovieRating mr
LEFT JOIN Users u
ON u.user_id = mr.user_id
GROUP BY u.user_id
ORDER BY COUNT(*) DESC, name ASC
LIMIT 1)
UNION ALL
(SELECT title as results FROM MovieRating mr
LEFT JOIN Movies m
ON mr.movie_id = m.movie_id
WHERE LEFT(created_at, 7) = '2020-02'
GROUP BY mr.movie_id
ORDER BY AVG(rating) DESC, title ASC
LIMIT 1);
```

### 40. Restaurant Growth

[LeetCode #1321](https://leetcode.com/restaurant-growth/)
```sql

```


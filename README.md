# Solution of 50 SQL Leetcode Problems MSSQL
# Link to all 50 Questions: 
https://leetcode.com/studyplan/top-sql-50/

# Solution

**1757. Recyclable and Low Fat Products**

SELECT product_id FROM Products where low_fats='Y' and recyclable='Y';

**584. Find Customer Referee**

SELECT name FROM Customer WHERE referee_id IS NULL OR referee_id<>2;

  **OR**

SELECT name FROM Customer WHERE referee_id IS NULL OR referee_id!=2;

**595. Big Countries**

SELECT name,population,area FROM World WHERE area>=3000000 or population>=25000000;

**1148. Article Views I**

SELECT DISTINCT author_id AS id FROM Views WHERE author_id=viewer_id ORDER BY id ASC;

**1683. Invalid Tweets**

SELECT tweet_id FROM Tweets where len(content)>15;

**1378. Replace Employee ID With The Unique Identifier**

SELECT unique_id,name FROM Employees emp LEFT JOIN EmployeeUNI uni ON emp.id=uni.id;

**1068. Product Sales Analysis I**

SELECT product_name,year,price FROM Product p INNER JOIN Sales s ON p.product_id=s.product_id;

**1581. Customer Who Visited but Did Not Make Any Transactions**

SELECT customer_id,COUNT(customer_id) as count_no_trans FROM Transactions t RIGHT JOIN Visits v on v.visit_id=t.visit_id WHERE t.transaction_id IS null GROUP BY customer_id;

**197. Rising Temperature**

SELECT w2.id as Id FROM Weather w1 INNER JOIN Weather w2 ON DATEDIFF(day,w1.recordDate,w2.recordDate)=1 AND w2.temperature>w1.temperature;

**1661. Average Time of Process per Machine**

SELECT a1.machine_id,ROUND(AVG(a2.timestamp-a1.timestamp),3) as processing_time FROM Activity a1 INNER JOIN Activity a2 ON a1.machine_id=a2.machine_id AND a1.process_id=a2.process_id AND a1.activity_type='start' AND a2.activity_type='end' GROUP BY a1.machine_id;

**577. Employee Bonus**

SELECT name,bonus FROM Employee emp left join Bonus b on emp.empId=b.empId where bonus<1000 or bonus is null;

**1280. Students and Examinations**

SELECT std.student_id,std.student_name,sub.subject_name,COUNT(ex.subject_name) AS attended_exams FROM Students std CROSS JOIN Subjects sub LEFT JOIN Examinations ex ON std.student_id=ex.student_id AND sub.subject_name=ex.subject_name GROUP BY std.student_id,std.student_name,sub.subject_name ORDER BY std.student_id,sub.subject_name;

**570. Managers with at Least 5 Direct Reports**

SELECT e1.name FROM Employee e1 INNER JOIN Employee e2 ON e1.id<>e2.id WHERE e1.id=e2.managerId GROUP BY e1.id,e1.name HAVING COUNT(e2.id)>=5;

**1934. Confirmation Rate**

SELECT s.user_id,ROUND(AVG(CASE WHEN action='confirmed' THEN 1.0 ELSE 0.0 END),2) as confirmation_rate FROM Signups s left join Confirmations c on s.user_id=c.user_id GROUP BY s.user_id;

**OR**

SELECT s.user_id,ROUND(CAST(COUNT(CASE WHEN action='confirmed' THEN 1 ELSE NULL END) AS FLOAT)/COUNT(*),2) AS confirmation_rate FROM Signups s LEFT JOIN Confirmations c ON s.user_id=c.user_id GROUP BY s.user_id;

**620. Not Boring Movies**

SELECT id,movie,description,rating FROM Cinema WHERE id%2<>0 and description != 'boring' order by rating desc;

**OR**

SELECT id,movie,description,rating FROM Cinema where not description='boring' and id%2=1 order by rating desc;

**OR**

SELECT id,movie,description,rating FROM Cinema WHERE description<>'boring' AND id%2=1 ORDER BY rating DESC;

**1251. Average Selling Price**

SELECT p.product_id,ISNULL(ROUND((SUM(price*units*1.0)/SUM(units)),2),0) AS average_price FROM Prices p LEFT JOIN UnitsSold s ON p.product_id=s.product_id AND purchase_date BETWEEN start_date AND end_date GROUP BY p.product_id;


**1075. Project Employees I**

SELECT p.project_id,ROUND(AVG(experience_years*1.0),2) AS [average_years] FROM Project p INNER JOIN Employee e ON p.employee_id=e.employee_id GROUP BY project_id;

**1633. Percentage of Users Attended a Contest**

SELECT contest_id, ROUND((COUNT(r.user_id)*100.0/(SELECT COUNT(*) FROM Users)),2) AS percentage FROM Register r INNER JOIN Users u ON r.user_id=u.user_id GROUP BY contest_id ORDER BY percentage DESC,contest_id;

**1211. Queries Quality and Percentage**

SELECT query_name,ROUND(AVG(rating*1.0/position),2) AS quality, ROUND(AVG(CASE WHEN rating<3 THEN 1.0 ELSE 0.0 END)*100.0,2) AS poor_query_percentage FROM Queries WHERE query_name IS NOT NULL GROUP BY query_name;

**1193. Monthly Transactions I**

SELECT FORMAT(trans_date,'yyyy-MM') AS month,
country,
COUNT(id) AS trans_count,
SUM(CASE WHEN state='approved' THEN 1 ELSE 0 END) AS approved_count,
SUM(amount) AS trans_total_amount,
SUM(CASE WHEN state='approved' THEN amount ELSE 0 END) AS approved_total_amount
FROM Transactions
GROUP BY country,FORMAT(trans_date,'yyyy-MM');

**2356. Number of Unique Subjects Taught by Each Teacher**

SELECT teacher_id,COUNT(DISTINCT subject_id) AS cnt FROM Teacher GROUP BY teacher_id;

**1141. User Activity for the Past 30 Days I**

SELECT activity_date AS day,COUNT(DISTINCT user_id) AS active_users FROM Activity WHERE activity_date BETWEEN '2019-06-28' AND '2019-07-27' GROUP BY activity_date;

**596. Classes More Than 5 Students**

SELECT class FROM Courses GROUP BY class HAVING COUNT(*)>=5;

**1729. Find Followers Count**

SELECT user_id,COUNT(follower_id) AS followers_count FROM Followers GROUP BY user_id ORDER BY user_id;

**619. Biggest Single Number**

SELECT MAX(num) as num FROM MyNumbers WHERE num IN (SELECT num FROM MyNumbers GROUP BY num HAVING COUNT(num)=1);

**OR**

SELECT MAX(A.num) AS num FROM (SELECT num AS num FROM MyNumbers GROUP BY num HAVING COUNT(*)=1) A;

**1731. The Number of Employees Which Report to Each Employee**

SELECT e1.employee_id,e1.name,COUNT(e2.reports_to) AS reports_count,ROUND(AVG(e2.age*1.0),0) AS average_age FROM Employees e1 INNER JOIN Employees e2 ON e1.employee_id=e2.reports_to GROUP BY e1.employee_id,e1.name ORDER BY employee_id;

# Advanced String Functions /Regex /Clause

**1667. Fix Names in a Table**

SELECT user_id,CONCAT(UPPER(SUBSTRING(name,1,1)),LOWER(SUBSTRING(name,2,LEN(name)))) AS name FROM Users ORDER BY user_id;

**1527. Patients With a Condition**

SELECT patient_id,patient_name,conditions FROM Patients WHERE conditions LIKE 'DIAB1%' OR conditions LIKE '% DIAB1%';

**196. Delete Duplicate Emails**

DELETE p2 FROM Person p1,Person p2 WHERE p1.email=p2.email AND p2.id>p1.id;

**176. Second Highest Salary**

SELECT CASE WHEN EXISTS (SELECT DISTINCT salary FROM Employee ORDER BY salary DESC OFFSET 1 rows FETCH NEXT 1 ROWS ONLY) THEN (SELECT Distinct salary FROM Employee ORDER BY salary DESC OFFSET 1 ROWS FETCH NEXT 1 ROWS ONLY) ELSE NULL END AS SecondHighestSalary;

**OR**

SELECT MAX(salary) AS SecondHighestSalary FROM Employee WHERE salary <(SELECT MAX(salary) FROM EMPLOYEE);

**1484. Group Sold Products By The Date**

WITH t AS (SELECT DISTINCT sell_date,product FROM Activities)
SELECT t.sell_date,COUNT(t.product) AS num_sold,STRING_AGG(t.product,',') WITHIN GROUP (ORDER BY t.product) AS products FROM t GROUP BY t.sell_date ORDER BY sell_date;

**1327. List the Products Ordered in a Period**

SELECT p.product_name, SUM(unit) AS unit FROM Products p INNER JOIN Orders o ON p.product_id=o.product_id WHERE MONTH(order_date)=2 AND YEAR(order_date)=2020 GROUP BY p.product_name HAVING SUM(unit)>=100; 

**OR**

SELECT product_name,SUM(unit) AS unit FROM Products p INNER JOIN Orders o ON p.product_id=o.product_id WHERE FORMAT(order_date,'yyyy-MM')='2020-02' GROUP BY product_name HAVING SUM(unit)>=100;

**1517. Find Users With Valid E-Mails**

SELECT user_id,name,mail FROM Users WHERE mail LIKE '[Aa-Zz]%@leetcode.com' AND mail NOT LIKE '%[^Aa-Zz0-9-_.]%@leetcode.com';





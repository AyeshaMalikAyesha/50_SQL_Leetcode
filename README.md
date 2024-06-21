# Solution of 50 SQL Leetcode Problems MSSQL
# Link to all 50 Questions: 
https://leetcode.com/studyplan/top-sql-50/

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



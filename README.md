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



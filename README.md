# Assignment16.1

CREATE TABLE users
(id INT,name STRING,salary INT,unit STRING) ROW FORMAT DELIMITED 
FIELDS TERMINATED BY '\t';
LOAD DATA LOCAL INPATH '/home/acadgild/users.txt'INTO TABLE users;
select name, rank() over (order by V.salary desc) as rank from (select name, unit,salary,(Salary - 100) as rank from users group by unit) V ;
SELECT name FROM    (        SELECT  name        ,       salary        ,       unit        ,       (                SELECT  ROUND(AVG(salary),2)                FROM    users u_inner                WHERE   u_inner.unit = e.unit                ) AS avg_sal        FROM    users e        ) as SubqueryAliasWHERE   salary > avg_sal

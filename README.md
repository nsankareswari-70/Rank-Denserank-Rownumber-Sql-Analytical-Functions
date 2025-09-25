### Rank-Denserank-Rownumber-Sql-Analytical-Functions
### Sql Server
```
How to view the list of databases available
select name from sys.databases;
- To pick a database to work
  use testdb;
- To view the tables available in the testdb database
  select table_name from INFORMATION_SCHEMA.TABLES;
```
```
create table employee(emp_id int,emp_name varchar(50),department_id int,salary int);

insert into employee(emp_id,emp_name,department_id,salary)values
(1,'Ankit',100,10000),
(2,'Mohit',100,15000),
(3,'Vikas',100,10000),
(4,'Rohit',100,5000),
(5,'Mudit',200,12000),
(6,'Agam',200,12000),
(7,'Sanjay',200,9000),
(8,'Ashish',200,5000);

```
```
1. Rank the employees by salary
select emp_id,emp_name,department_id,salary,
rank() over(order by salary desc) as rnk
from employee;
```
![img alt](
https://github.com/nsankareswari-70/Rank-Denserank-Rownumber-Sql-Analytical-Functions/blob/9a382f122ff32497ea7083d83c85a93ef2e45a1a/sql1.png)
```
2.Dense rank employees by salary
  select emp_id,emp_name,department_id,salary,
dense_rank() over(order by salary desc)as rnk from employee;
```
![img alt](
https://github.com/nsankareswari-70/Rank-Denserank-Rownumber-Sql-Analytical-Functions/blob/795b52f56b6ce48ff3dd1182122a21192336d1b6/sql2.png)
```
3.Give row number for employees by salary desc
select emp_id,emp_name,department_id,salary,
dense_rank() over(order by salary desc)as rnk,
row_number() over(order by salary desc)as rn from employee;
```
![img alt](https://github.com/nsankareswari-70/Rank-Denserank-Rownumber-Sql-Analytical-Functions/blob/177616dec7b64b3fd97b5db8e2bff26fd4214920/sql3.png)

```
4.Partition by department
select emp_id,emp_name,department_id,salary,
rank() over(partition by department_id order by salary desc)as rnk,
dense_rank() over(partition by department_id order by salary desc)as densrnk,
row_number() over(partition by department_id order by salary desc)as rn from employee;
```
![img alt](https://github.com/nsankareswari-70/Rank-Denserank-Rownumber-Sql-Analytical-Functions/blob/1e42da2377ee16dfca83a20b4dc5fa59ea2720d9/sql4.png)

```
5. Sort the employees within each department in descending order of salary.
select emp_id,emp_name,department_id,salary,
dense_rank() over(partition by department_id order by salary desc)as densrnk
 from employee;
```
![img alt](
https://github.com/nsankareswari-70/Rank-Denserank-Rownumber-Sql-Analytical-Functions/blob/fb518669224c01128207072468a750cfc81aa54a/sql5.png)

```
6. Find which employee is getting the highest salary in each department
select * from(
select emp_id,emp_name,department_id,salary,
dense_rank() over(partition by department_id order by salary desc)as densrnk
 from employee) t
 where densrnk=1;
```


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

  

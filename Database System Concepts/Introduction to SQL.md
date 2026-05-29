```sql
-- Find the department names of all instructors
select dept_name from instructor;
```
```sql
-- Find the department names
select distinct dept_name from instructor;
```
```sql
-- mathematical Operators
select ID, name, dept_name, salary*1.1
from instructor;
```
```sql
-- Find the names of all instructors in the Computer Science department who have salary greater than $70,000
select * from instructor
where dept_name = 'Comp. Sci.' and salary > 70000;
```
```sql
-- Retrieve the names of all instructors, along with their department names and department building name
select name, i.dept_name, building 
	from instructor i, department d
	where i.dept_name = d.dept_name;
```
-- 

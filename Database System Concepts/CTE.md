### The WITH Clause
```sql
-- Find department with maximum budget
with max_budget(value) as
    (select max(budget) 
    from department)
select dept_name, budget
from department d, max_budget m
where d.budget = m.value;
```
```sql
-- Find all departments where the total salary is greater than the average of the total salary at all departments.
with dept_total(dept_name, value) as
		(select dept_name, sum(salary)
		from instructor
		group by dept_name),
	dept_total_avg(value) as
		(select avg(value) 
		from dept_total)
select dept_name
from dept_total t, dept_total_avg a
where t.value > a.value;
```

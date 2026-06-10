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


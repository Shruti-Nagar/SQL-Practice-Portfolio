### Scalar Subquery
```sql
-- lists all departments along with the number of instructors in each department.
select dept_name, (
	select count(*) -- it returns only one value
		from instructor i
		where d.dept_name = i.dept_name) 
	as num_instructor
from department d
```

```sql
-- Scalar without FROM Clause
select (
	select count(*) from teaches)
	/
	(select count(*) from instructor)
	as num_of_instrutors
```

### Modification of DB
### DELETION

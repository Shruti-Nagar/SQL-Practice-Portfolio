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
```sql
-- Delete all tuples in the instructor relation pertaining to instructors in the Finance department.
delete from instructor
where department = 'Finance';
```
```sql
-- Delete all instructors with a salary between $13,000 and $15,000.
delete from instructors
where salary between 13000 and 15000;
```
```sql
-- Delete all tuples in the instructor relation for those instructors associated with a
-- department located in the Watson building.
delete from instructor
	where dept_name in (select dept_name
from department
where building = 'Watson')
```
```sql
-- delete the records of all instructors with salary below the average at the university.
delete from instructor
where salary < (select avg(salary)
				from instructor);
```

### INSERTION
```sql
-- insert the course CS-437 in the Computer Science department with title “Database Systems” and four credit hours.
select * from course
insert into course values (
	'CS-437', 'Database Systems', 'Comp. Sci.', 4
);
```
```sql
/* Make each student in the Music department who has earned more than 144 credit 
	hours an instructor in the Music department with a salary of $18,000. */
insert into instructor (
		select ID, name, dept_name, 18000
			from student
			where dept_name = 'Music'
			and tot_cred > 144
			);
```

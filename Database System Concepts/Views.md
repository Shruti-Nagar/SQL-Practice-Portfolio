### VIEWS
```sql
-- create view: for who needs to access instructor data except salary.
create view faculty as 
	select id, name, dept_name
	from instructor
```
```sql
/* create a view that lists all course sections offered by the Physics department in
the Fall 2017 semester with the building and room number of each section.*/

create view physics_fall_2017 as
	select c.course_id, sec_id, building, room_number
	from course c, section s
	where c.course_id = s.course_id
	and dept_name = 'Physics'
	and s.semester = 'Fall'
	and s.year = 2017;
```
```sql
-- specifing attribute names in the view
create view departments_total_salary(dept_name, total_salary) as
	select dept_name, sum(salary)
		from instructor
		group by dept_name
```
```sql
-- inserting into view 'faculty'.
insert into faculty
values ('30765', 'Green', 'Music');
```

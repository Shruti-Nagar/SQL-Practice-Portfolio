```sql
-- Find all instructors in the Physics department
select * 
from instructor 
where dept_name='Physics';
```
```sql
-- Find instructors and the courses they teach (inner join)
select *
from instructor i, teaches t
where i.id = t.id;
```
```sql
-- Find courses taught in both Fall 2017 and Spring 2018 (set intersection)
select course_id
from section
where semester='Fall' and Year=2017
intersect
select course_id
from section
where semester='Spring' and Year=2018;
```
```sql
-- Find courses taught in Fall 2017 but not in Spring 2018 (set difference)
select course_id
from section
where semester='Fall' and Year=2017
except
select course_id
from section
where semester='Spring' and Year=2018;
```
```sql
-- Find the ID and names of all Physics department instructors
select id, name from instructor
where dept_name='Physics';
```
```sql
-- Find instructors whose department is in the Watson building
select i.id, i.name
from instructor i, department d
where i.dept_name = d.dept_name
and building = 'Watson';
```
```sql
-- Find the department names of all instructors
select dept_name from instructor;
```
```sql
-- Find unique department names (remove duplicates)
select distinct dept_name from instructor;
```
```sql
-- Calculate 10% salary increase for all instructors (mathematical operators)
select ID, name, dept_name, salary*1.1
from instructor;
```
```sql
-- Find names of all instructors in the Computer Science department who have salary greater than $70,000
select * from instructor
where dept_name = 'Comp. Sci.' and salary > 70000;
```
```sql
-- Retrieve the names of all instructors, along with their department names and department building name
select name, i.dept_name, building 
	from instructor i, department d
	where i.dept_name = d.dept_name;
```
```sql
-- Cartesian Product - combines every instructor with every course taught
select * from instructor, teaches;
```
```sql
-- Find which courses each instructor teaches (join without cartesian product)
select * from instructor i, teaches t
	where i.id = t.id;
```
```sql
-- Find instructor names and courses they teach using aliases
select name as instructor_name, course_id
from instructor, teaches
where instructor.id = teaches.id;
```
```sql
-- Find instructor names and courses they teach using table aliases (alternative syntax)
select i.name, t.course_id
from instructor as i, teaches as t
where i.id = t.id;
```
```sql
-- Find the names of all instructors whose salary is greater than at least one instructor in the Biology department
select a.name
from instructor a, instructor b
where a.salary>b.salary and b.dept_name = 'Biology';
```
```sql
-- Find the names of all departments whose building name includes the substring 'Watson'
select dept_name from department
where building like '%Watson';
```
```sql
-- List in alphabetic order all instructors in the Physics department
select name from instructor where dept_name='Physics' order by name;
```
```sql
-- Use tuple comparison to find instructors in Biology department using tuple equality
select name, course_id
from instructor i, teaches t
where (i.id, i.dept_name) = (t.id, 'Biology');
```

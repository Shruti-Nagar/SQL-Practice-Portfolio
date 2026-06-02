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
```sql
-- Cartesian Product
select * from instructor, teaches;
```
```sql
select * from instructor i, teaches t
	where i.id = t.id;
```
```sql
-- Alias or renaming attributes
select name as instructor_name, course_id
from instructor, teaches
where instructor.id = teaches.id;
```
```sql
select i.name, t.course_id
from instructor as i, teaches as t
where i.id = t.id;
```
```sql
-- Find the names of all instructors whose salary is greater than at least one instructor in the Biology department.
select a.name
from instructor a, instructor b
where a.salary>b.salary and b.dept_name = 'Biology';
```
```sql
-- Find the names of all departments whose building name includes the substring 'Watson'.
select dept_name from department
where building like '%Watson';
```
```sql
--  list in alphabetic order all instructors in the Physics department.
select name from instructor where dept_name='Physics' order by name;
```
```sql
--The comparison operators can be used on tuples, and the ordering is defined lexicographically.
select name, course_id
from instructor i, teaches t
where (i.id, i.dept_name) = (t.id, 'Biology');
```
### SET OPERATIONS
```sql
-- Find the set of all courses taught either in Fall 2017 or in Spring 2018, or both.
(select course_id from section
where semester = 'Fall' and year = 2017)
union
(select course_id from section
where semester = 'Spring' and year = 2018);
```
```sql
-- Union All - retains duplicates
(select course_id from section
where semester = 'Fall' and year = 2017)
union all
(select course_id from section
where semester = 'Spring' and year = 2018);
```
```sql
-- Find the set of all courses taught in both the Fall 2017 and Spring 2018.
(select course_id from section
where semester = 'Fall' and year = 2017)
intersect
(select course_id from section
	where semester = 'Spring' and year = 2018);
```
```sql
-- to retain all duplicates
(select course_id from section
where semester = 'Fall' and year = 2017)
intersect all
(select course_id from section
	where semester = 'Spring' and year = 2018);
```
```sql
-- Find all courses taught in the Fall 2017 semester but not in the Spring 2018 semester.
(select course_id from section
where semester = 'Fall' and year = 2017)
except
(select course_id from section
where semester = 'Spring' and year = 2018);
```
### AGGREGATIONS
```sql
-- Find the average name of instructors in the Computer Science department.
select avg(salary) as avg_salary
from instructor
where dept_name = 'Comp. Sci.';
```
```sql
-- Find the total number of instructors who teach a course in the Spring 2018 semester.
select count(distinct ID) as total_instructors
from teaches
where semester = 'Spring' and year = 2018;
```
```sql
-- Find the average salary in each department.
select dept_name, round(avg(salary)) as avg_salary
from instructor
group by dept_name
order by dept_name;
```
```sql
-- Find the number of instructors in each department who teach a course in the Spring 2018 semester.
select i.dept_name, count(distinct i.id) as instructor_count
	from teaches t, instructor i
	where t.id = i.id
		and t.semester = 'Spring' and t.year = 2018
	group by dept_name;
```
```sql
-- Departments where the average salary of the instructors is more than $42,000.
select dept_name, avg(salary) as avg_salary
from instructor
group by dept_name
having avg(salary)>42000
order by dept_name;
```

```sql
-- Find the courses taught in spring 2018 as well as in fall 2017, using subquery.
select distinct course_id
	from section 
	where semester = 'Fall' and year = 2017 
	and course_id in (
		select course_id 
		from section 
		where semester = 'Spring' and year = 2018);
```
```sql
-- Find all the courses taught in the Fall 2017 semester but not in the Spring 2018 semester.
select distinct course_id 
	from section
	where semester = 'Fall' and year = 2017
	and course_id not in (
		select course_id
		from section
		where semester = 'Spring' and year = 2018
	);
```
```sql
-- Select the names of instructors whose names are neither “Mozart” nor “Einstein”.
select name 
	from instructor
	where name not in ('Mozart', 'Einstein');
```
```sql
/* Find the total number of (distinct) students who have taken course sections taught by the instructor with ID 10101. */
select count (distinct id)
from takes
where (course_id, sec_id, semester, year) in (
	select course_id, sec_id, semester, year
	from teaches
	where id = 10101);

-- Alternate way
select count (distinct id)
	from takes s
	where exists (
		select course_id, sec_id, semester, year
		from teaches t 
		where t.id = 10101 
		and t.course_id = s.course_id
		and t.sec_id = s.sec_id
		and t.semester = s.semester
		and t.year = s.year);
```
```sql
-- Find the names of all instructors whose salary is greater than at least one instructor in the Biology department.
select name
from instructor
where salary > some (
		select salary 
		from instructor 
		where dept_name = 'Biology')

--alternate query (self join)
select a.name 
	from instructor a, instructor b
	where a.salary> b.salary;
	and b.dept_name = 'Biology';
```
```sql
-- find the names of all instructors that have a salary value greater than that of each instructor in the Biology department.
select name 
	from instructor
	where salary > all (
			select salary 
			from instructor 
			where dept_name = 'Biology');
```
```sql
-- Find the departments that have the highest average salary
select dept_name
	from instructor
	group by dept_name
	having avg(salary) >= all (
			select avg(salary)
			from instructor
			group by dept_name);
```

###  Test for Empty Relations
```sql
-- Find all courses taught in both the Fall 2017 semester and in the Spring 2018 semester using Correlated Subquery.
select course_id 
	from section a
	where semester = 'Spring'
	and year = 2018 and exists (select course_id 
		from section b
		where semester = 'Fall'
		and year = 2017
		and a.course_id = b.course_id);
```
```sql
-- Find all students who have taken all courses offered in the Biology department.
select s.ID, s.name 
	from student s
	where not exists ((
					-- if an empty set then included in output else not.
			select course_id 
			from course
			where dept_name = 'Biology')
			except (
				select t.course_id from teaches t
				where t.id = s.id	
			));
```
### Test for the Absence of Duplicate Tuples
```sql
-- Find all courses that were offered at most once in 2017.
select c.course_id
from course c
where unique (select s.course_id 
				from section s
				where c.course_id = s.course_id
				and s.year = 2017);
```
```sql
-- Alternate **Some SQL softwares do not implement UNIQUE predicate
select c.course_id
from course c
where 1 >= (select count(s.course_id) 
				from section s
				where c.course_id = s.course_id
				and s.year = 2017);
```
### Find Duplicates
```sql
-- Find all courses that were offered at least twice in 2017.
select course_id
	from course c
	where not unique (select course_id
	from section s 
	where c.course_id = s.course_id
	and year = 2017);
```
```sql
-- Alternate
select course_id
	from course c
	where 1 < (select count(s.course_id)
	from section s 
	where c.course_id = s.course_id
	and year = 2017);
```
### From Clause SubQueries
```sql
-- Find the average instructors salaries of those departments where the average salary is greater than $42,000.
select dept_name, avg_salary
from (select dept_name, avg(salary)
		from instructor
		group by dept_name) as dept_avg_salary(dept_name, avg_salary) -- can give alias to attributes too while declaring a suquery name
where avg_salary>42000;
```
```sql
-- Find the maximum salary across all departments of the total of all instructors’ salaries in each department.
select max(total_salary)
	from (select dept_name, sum(salary)
			from instructor
			group by dept_name) as dept_salary(dept_name, total_salary);
```
```sql
select name, salary, avg_salary
	from instructor i, 
	lateral (select avg(salary) as avg_salary
	from instructor n
	where i.dept_name = n.dept_name);
```
```sql
select name, salary, avg_salary
	from instructor i,
	lateral (
		select round(avg(salary)) as avg_salary
		from instructor n
		where i.dept_name = n.dept_name
	) avgSalary
```


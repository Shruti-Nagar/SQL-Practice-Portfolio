```sql
-- Find the average salary of instructors in the Computer Science department
select avg(salary) as avg_salary
from instructor
where dept_name = 'Comp. Sci.';
```
```sql
-- Find the total number of instructors who teach a course in the Spring 2018 semester
select count(distinct ID) as total_instructors
from teaches
where semester = 'Spring' and year = 2018;
```
```sql
-- Find the average salary in each department
select dept_name, round(avg(salary)) as avg_salary
from instructor
group by dept_name
order by dept_name;
```
```sql
-- Find the number of instructors in each department who teach a course in the Spring 2018 semester
select i.dept_name, count(distinct i.id) as instructor_count
	from teaches t, instructor i
	where t.id = i.id
		and t.semester = 'Spring' and t.year = 2018
	group by dept_name;
```
```sql
-- Find departments where the average salary of the instructors is more than $42,000
select dept_name, avg(salary) as avg_salary
from instructor
group by dept_name
having avg(salary)>42000
order by dept_name;
```
```sql
/* For each course section offered in 2017, find the average total credits (tot cred) of all students 
enrolled in the section, if the section has at least 2 students */
select course_id, semester, year, sec_id, round(avg(tot_cred))
from student s, takes t
where s.id = t.id
and t.year = 2017
group by course_id, semester, year, sec_id
having count(s.id)>=2
```

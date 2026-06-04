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
```

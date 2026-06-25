
### Natural Join
```sql
-- For all students in the university who have taken some course, find their names and the course ID of all courses they took 
select *
  from student
  natural join takes;

-- Natural join automatically identifies the common attribute to joined relations.
```
```sql
-- List the names of students along with the titles of courses that they have taken.
select name, title
from student natural join takes, course
where takes.course_id = course.course_id;
```
### Join USING condition
```sql
-- List the names of students along with the titles of courses that they have taken.
select name, title
from (student natural join takes)
join course
using (course_id) -- multiple attributes can be mentioned in the Using condition
```

### Join ON condiiton
```sql
select name, title
	from student 
	join takes on student.id = takes.id
	join course on takes.course_id = course.course_id;
```
```sql
-- Find all students and the courses they have taken (include students who haven't taken any course
select *
from student s 
	left outer join takes t
	on s.id = t.id
order by s.id
```
```sql
-- List the names of students along with the titles of courses they have taken
select * name, title
from (student natural join takes)
join course
using (course_id) from student inner join takes using (ID);
```
```sql
-- Find all Physics department course sections offered in Fall 2017 with building and room details
select c.course_id, sec_id, building, room_number
from course c, section s
where c.course_id = s.course_id
and dept_name = 'Physics'
and s.semester = 'Fall'
and s.year = 2017;
```

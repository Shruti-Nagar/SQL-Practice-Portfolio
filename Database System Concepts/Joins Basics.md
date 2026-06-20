
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

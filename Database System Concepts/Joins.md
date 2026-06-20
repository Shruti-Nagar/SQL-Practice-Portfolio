
### Natural Join
```sql
-- For all students in the university who have taken some course, find their names and the course ID of all courses they took 
select *
  from student
  natural join takes;

-- Natural join automatically identifies the common attribute to join the relations
```
```sql
-- List the names of students along with the titles of courses that they have taken.
select name, title
from student natural join takes, course
where takes.course_id = course.course_id;
```

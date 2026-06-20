
### Natural Join
```sql
-- For all students in the university who have taken some course, find their names and the course ID of all courses they took 
select * from student natural join takes;

-- Natural join automatically identifies the common attribute to join the relations
```

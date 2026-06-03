```sql
-- Find the set of all courses taught either in Fall 2017 or in Spring 2018, or both
(select course_id from section
where semester = 'Fall' and year = 2017)
union
(select course_id from section
where semester = 'Spring' and year = 2018);
```
```sql
-- Union All - retains duplicates when combining two result sets
(select course_id from section
where semester = 'Fall' and year = 2017)
union all
(select course_id from section
where semester = 'Spring' and year = 2018);
```
```sql
-- Find the set of all courses taught in both the Fall 2017 and Spring 2018
(select course_id from section
where semester = 'Fall' and year = 2017)
intersect
(select course_id from section
	where semester = 'Spring' and year = 2018);
```
```sql
-- Intersect All - retain all duplicates when finding common rows
(select course_id from section
where semester = 'Fall' and year = 2017)
intersect all
(select course_id from section
	where semester = 'Spring' and year = 2018);
```
```sql
-- Find all courses taught in the Fall 2017 semester but not in the Spring 2018 semester
(select course_id from section
where semester = 'Fall' and year = 2017)
except
(select course_id from section
where semester = 'Spring' and year = 2018);
```

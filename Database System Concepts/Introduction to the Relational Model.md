```sql
create table department (
	dept_name varchar(20) primary key,
	building varchar(20),
	budget int);
```

```sql
insert into department values
	('Biology', 'Watson', 90000),
	('Comp. Sci.', 'Taylor', 100000),
	('Elec. Eng', 'Taylor', 85000),
	('Finance', 'Painter', 120000),
	('History', 'Painter', 50000),
	('Music', 'Packerd', 80000),
	('Physics', 'Watson', 70000)
;
```

```sql
update department
set dept_name='Elec. Eng.'
where dept_name='Elec. Eng'
```

```sql
select * from department;
```

```sql
create table instructor (
	ID int primary key,
	name varchar(50),
	dept_name varchar(20) references department(dept_name),
	salary int);
```

```sql
insert into instructor values
	(10101, 'Srinivasan', 'Comp. Sci.', 65000),
	(12121, 'Wu', 'Finance', 90000),
	(15151, 'Mozart', 'Music', 40000),
	(22222, 'Einstein', 'Physics', 95000),
	(32343, 'El Said', 'History', 60000),
	(33456, 'Gold', 'Physics', 87000),
	(45565, 'Katz', 'Comp. Sci.', 75000),
	(58583, 'Califieri', 'History', 62000),
	(76543, 'Singh', 'Finance', 80000),
	(76766, 'Crick', 'Biology', 72000),
	(83821, 'Brandt', 'Comp. Sci.', 92000),
	(98345, 'Kim', 'Elec. Eng.', 80000);
```

```sql
select * from instructor;
```

```sql
update instructor
	set name = 'Kim'
	where name = 'Kim"';
```

```sql
create table course(
	course_id varchar(10) primary key,
	title varchar(50),
	dept_name varchar(20) references department(dept_name),
	credits int
);
```

```sql
create table prereq(
	course_id varchar(10) references course(course_id),
	prereq_id varchar(10)
);
```

```sql
insert into course values
	('BIO-101', 'Into to Biology', 'Biology', 4),
	('BIO-301', 'Genetics', 'Biology', 4),
	('BIO-399', 'Computational Biology', 'Biology', 3),
	('CS-101', 'Intro to Computer Science', 'Comp. Sci.', 4),
	('CS-190', 'Game Design', 'Comp. Sci.', 4),
	('CS-315', 'Robotics', 'Comp. Sci.', 3),
	('CS-319', 'Image Processing', 'Comp. Sci.', 3),
	('CS-347', 'Database System Concepts', 'Comp. Sci.', 3),
	('EE-181', 'Intro. to Digtal Systems', 'Elec. Eng.', 3),
	('FIN-201', 'Investment Banking', 'Finance', 3),
	('HIS-351', 'World History', 'History', 3),
	('MU-199', 'Music Video Production', 'Music', 3),
	('PHY-101', 'Physical Principles', 'Physics', 4);
```
	
```sql
select * from course;
```

```sql
alter table prereq
	add foreign key (prereq_id) references course(course_id); 
```

```sql
insert into prereq values 
	('BIO-301', 'BIO-101'),
	('BIO-399', 'BIO-101'),
	('CS-190', 'CS-101'),
	('CS-315', 'CS-101'),
	('CS-319', 'CS-101'),
	('CS-347', 'CS-101'),
	('EE-181', 'PHY-101');
```

```sql
select * from prereq;
```

```sql
create table classroom(
	building varchar(15),
	room_number varchar(7),
	capacity int,
	primary key (building, room_number));
```

```sql
insert into classroom values 
	('Packard', '101', 500),
	('Painter', '514', 10),
	('Taylor', '3128', 70),
	('Watson', '100', 30),
	('Watson', '120', 50);
```

```sql
select * from classroom;
```

```sql
create table section (
	course_id varchar(10) references course(course_id),
	sec_id int,
	semester varchar(10),
	year numeric(4,0),
	building varchar(15),
	room_number varchar(7),
	time_slot_id varchar(4),
	primary key (course_id, sec_id, semester, year)
);
```

```sql
insert into section values
	('BIO-101', 1, 'Summer', 2017, 'Painter', 514, 'B'),
	('BIO-301', 1, 'Summer', 2018, 'Painter', 514, 'A'),
	('CS-101', 1, 'Fall', 2017, 'Packard', 101, 'H'),
	('CS-101', 1, 'Spring', 2018, 'Packard', 101, 'F'),
	('CS-190', 1, 'Spring', 2017, 'Taylor', 3128, 'E'),
	('CS-190', 2, 'Spring', 2017, 'Taylor', 3128, 'A'),
	('CS-315', 1, 'Spring', 2018, 'Watson', 120, 'D'),
	('CS-319', 1, 'Spring', 2018, 'Watson', 100, 'B'),
	('CS-319', 2, 'Spring', 2018, 'Taylor', 3128, 'C'),
	('CS-347', 1, 'Fall', 2017, 'Taylor', 3128, 'A'),
	('EE-181', 1, 'Spring', 2017, 'Taylor', 3128, 'C'),
	('FIN-201', 1, 'Spring', 2018, 'Packard', 101, 'B'),
	('HIS-351', 1, 'Spring', 2018, 'Painter', 514, 'C'),
	('MU-199', 1, 'Spring', 2018, 'Packard', 101, 'D'),
	('PHY-101', 1, 'Fall', 2017, 'Watson', 100, 'A');
```

```sql
select * from section;
```

```sql
create table teaches(
	ID int references instructor(ID),
	course_id varchar(10),
	sec_id int,
	semester varchar(10),
	year numeric(4,0),
	primary key (ID, course_id, sec_id, semester, year),
	foreign key (course_id, sec_id, semester, year) references section
);
```

```sql
insert into teaches values 
	(10101, 'CS-101', 1, 'Fall', 2017),
	(10101, 'CS-315', 1, 'Spring', 2018),
	(10101, 'CS-347', 1, 'Fall', 2017),
	(12121, 'FIN-201', 1, 'Spring', 2018),
	(15151, 'MU-199', 1, 'Spring', 2018),
	(22222, 'PHY-101', 1, 'Fall', 2017),
	(32343, 'HIS-351', 1, 'Spring', 2018),
	(45565, 'CS-101', 1, 'Spring', 2018),
	(45565, 'CS-319', 1, 'Spring', 2018),
	(76766, 'BIO-101', 1, 'Summer', 2017),
	(76766, 'BIO-301', 1, 'Summer', 2018),
	(83821, 'CS-190', 1, 'Spring', 2017),
	(83821, 'CS-190', 2, 'Spring', 2017),
	(83821, 'CS-319', 2, 'Spring', 2018),
	(98345, 'EE-181', 1, 'Spring', 2017);
```

```sql
select * from teaches;
```

```sql
select * 
from instructor 
where dept_name='Physics';
```

```sql
select *
from instructor i, teaches t
where i.id = t.id;
```

```sql
select course_id
from section
where semester='Fall' and Year=2017
intersect
select course_id
from section
where semester='Spring' and Year=2018;
```

```sql
select course_id
from section
where semester='Fall' and Year=2017
except
select course_id
from section
where semester='Spring' and Year=2018;
```

```sql
select id, name from instructor
where dept_name='Physics';
```

```sql
select i.id, i.name
from instructor i, department d
where i.dept_name = d.dept_name
and building = 'Watson';
```

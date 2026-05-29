### Inner Joins

Table: movies
| id | title            | director        | year | length_minutes |
|----|------------------|----------------|------|----------------|
| 1  | Toy Story        | John Lasseter  | 1995 | 81             |
| 2  | A Bug's Life     | John Lasseter  | 1998 | 95             |
| 3  | Toy Story 2      | John Lasseter  | 1999 | 93             |
| 4  | Monsters, Inc.   | Pete Docter    | 2001 | 92             |
| 5  | Finding Nemo     | Andrew Stanton | 2003 | 107            |
| 6  | The Incredibles  | Brad Bird      | 2004 | 116            |
...

Table: boxoffice
| movie_id | rating | domestic_sales | international_sales |
|----------|--------|----------------|---------------------|
| 5        | 8.2    | 380843261      | 555900000           |
| 14       | 7.4    | 268492764      | 475066843           |
| 8        | 8.0    | 206445654      | 417277164           |
| 12       | 6.4    | 191452396      | 368400000           |
| 3        | 7.9    | 245852179      | 239163000           |
| 6        | 8.0    | 261441092      | 370001000           |
....


Find the domestic and international sales for each movie.
```sql
select m.title, b.domestic_sales, b.international_sales
from movies m
inner join boxoffice b on m.id = b.movie_id;
```

Show the sales numbers for each movie that did better internationally rather than domestically.
```sql
select m.title, b.domestic_sales, b.international_sales
from movies m
inner join boxoffice b on m.id = b.movie_id
where b.domestic_sales < b.international_sales;
```

List all the movies by their ratings in descending order.
```sql
select title, rating
from movies m
join boxoffice b on m.id = b.movie_id
order by rating desc;
```

### Outer Joins

Table: buildings (Read-only)
| building_name | capacity |
|---------------|----------|
| 1e            | 24       |
| 1w            | 32       |
| 2e            | 16       |
| 2w            | 20       |
...

Table: employees (Read-only)
| role     | name       | building | years_employed |
|----------|------------|----------|----------------|
| Engineer | Becky A.   | 1e       | 4              |
| Engineer | Dan B.     | 1e       | 2              |
| Engineer | Sharon F.  | 1e       | 6              |
| Engineer | Dan M.     | 1e       | 4              |
| Engineer | Malcom S.  | 1e       | 1              |
| Artist   | Tylar S.   | 2w       | 2              |
...

Find the list of all buildings that have employees
```sql
select distinct building
from employees;
```

Find the list of all buildings and their capacity
```sql
select * from buildings;
```

List all buildings and the distinct employee roles in each building (including empty buildings)
```sql
select distinct(building_name), role
from buildings b
left join employees e
on b.building_name = e.building;
```

Find the name and role of all employees who have not been assigned to a building 
```sql
select name, role
from employees where building is null;
```

Find the names of the buildings that hold no employees.
```sql
select building_name
from buildings
left join employees
on employees.building = buildings.building_name
where building is null;
```

### Aggregate Operations

List all movies and their combined sales in millions of dollars.
```sql
select title, (domestic_sales+international_sales)/1000000 as combined_sales
from movies left join boxoffice
on movies.id=boxoffice.movie_id
group by combined_sales;
```

List all movies and their ratings in percent
```sql
select title, concatenate(rating*10, "%" as ratings
from movies left join boxoffice
on movies.id = boxoffice.movie_id;
```

List all movies that were released on even number years
```sql
select * from movies
where year%2 == 0;
```

Find the longest time that an employee has been at the studio
```sql
select max(years_employed)
from Employees
```

For each role, find the average number of years employed by employees in that role
```sql
select role, avg(years_employed)
from Employees
group by role;
```

Find the total number of employee years worked in each building
```sql
select building, sum(years_employed)
from Employees
group by building;
```

Find the number of Artists in the studio (without a HAVING clause).
```sql
select role, count(*) total_artists
from employees
where role = 'Artist';
```

Find the number of Employees of each role in the studio
```sql
select role, count(*) total_emp
from employees
group by role;
```

Find the total number of years employed by all Engineers
```sql
select role, sum(years_employed) total_years
from employees
group by role
having role = 'Engineer';
```

Find the number of movies each director has directed
```sql
select director, count(*) as total_movies
from movies
group by director;
```

Find the total domestic and international sales that can be attributed to each director
```sql
select director, sum(domestic_sales, international_sales) as gross_sales
from movies m
left join boxoffice b
on m.id = b.movie_id
group by director
```

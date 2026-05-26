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

### Find the domestic and international sales for each movie
```sql
select m.title, b.domestic_sales, b.international_sales
from movies m
inner join boxoffice b on m.id = b.movie_id;
```

### Show the sales numbers for each movie that did better internationally rather than domestically
select m.title, b.domestic_sales, b.international_sales
from movies m
inner join boxoffice b on m.id = b.movie_id
where b.domestic_sales < b.international_sales;

### List all the movies by their ratings in descending order
select title, rating
from movies m
join boxoffice b on m.id = b.movie_id
order by rating desc;

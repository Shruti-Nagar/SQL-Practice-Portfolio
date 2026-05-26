```sql
SELECT * FROM north_american_cities;
```

Table: north_american_cities
| city         | country        | population | latitude  | longitude   |
|--------------|----------------|------------|-----------|-------------|
| Guadalajara  | Mexico         | 1500800    | 20.659699 | -103.349609 |
| Toronto      | Canada         | 2795060    | 43.653226 | -79.383184  |
| Houston      | United States  | 2195914    | 29.760427 | -95.369803  |
| New York     | United States  | 8405837    | 40.712784 | -74.005941  |
| Philadelphia | United States  | 1553165    | 39.952584 | -75.165222  |
| Havana       | Cuba           | 2106146    | 23.054070 | -82.345189  |
...

### List all the Canadian cities and their populations
```sql
SELECT City, Population 
FROM north_american_cities
WHERE Country = 'Canada';
```

### Order all the cities in the United States by their latitude from north to south
```sql
Select City from north_american_cities
Where Country = "United States"
Order by latitude desc;
```

### List all the cities west of Chicago, ordered from west to east
```sql
select city, longitude from north_american_cities
where longitude < (select longitude from north_american_cities where city = "Chicago")
order by longitude asc;
```
### List the two largest cities in Mexico (by population)
```sql
select City 
from north_american_cities
where Country = "Mexico"
order by population desc
limit 2;
```

### List the third and fourth largest cities (by population) in the United States and their population
```sql
select * from north_american_cities
where country = "United States"
order by population desc
limit 2 offset 2;
```

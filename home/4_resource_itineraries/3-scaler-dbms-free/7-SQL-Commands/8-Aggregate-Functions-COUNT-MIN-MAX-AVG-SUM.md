# 8. Aggregate Functions COUNT MIN MAX AVG SUM
Created Wed Apr 10, 2024 at 1:21 AM

## Task
What is the highest rankscore ever assigned to any movie.

## Context
All SQL statements we learnt until now (SELECT, WHERE etc) returned a table.
But sometimes we want to calculate a single (scalar) value, like getting total, count, avg, min, max etc.

In SQL, these operations are done using 'Aggregate functions'. Essentially they are an array.reduce operation (think JS `Array.reduce`)

The count 50,000 below is calculated using an aggregate function
![](../../../../assets/8-Aggregate-Functions-COUNT-MIN-MAX-AVG-SUM-image-1-90a59cee.png)
## Syntax
```sql
SELECT aggregate_function(columnA) FROM table_name;

-- specifically, the syntax is
SELECT aggregate_function(columnA)

-- note: there should be no space between function and opening parentheses
COUNT (year) ❌ -- syntax error
COUNT(year)  ✅
```

Examples:
```sql
SELECT MIN(year) FROM movies;
SELECT MAX(year) FROM movies;
SELECT COUNT(*) FROM movies;
SELECT COUNT(*) FROM movies WHERE year > 2000; -- conditional counting is possible!
SELECT COUNT(year) FROM movies;
-- COUNT(year) gives the same result as COUNT(*) since
-- COUNT doesn't care about column values, but just the existence of rows
```

Outputs
```sql
mysql> SELECT MIN(year) FROM movies;
+-----------+
| MIN(year) |
+-----------+
|      1888 |
+-----------+
1 row in set (0.15 sec)


mysql> SELECT MAX(year) FROM movies;
+-----------+
| MAX(year) |
+-----------+
|      2008 |
+-----------+
1 row in set (0.09 sec)


mysql> SELECT COUNT(*) FROM movies;
+----------+
| COUNT(*) |
+----------+
|   388269 |
+----------+
1 row in set (0.03 sec)


mysql> SELECT COUNT(*) FROM movies WHERE year > 2000;
+----------+
| COUNT(*) |
+----------+
|    46006 |
+----------+
1 row in set (0.08 sec)


mysql> SELECT COUNT(year) FROM movies;
-- COUNT(year) gives the same result as COUNT(*) since
-- COUNT doesn't care about column values, but just the existence of rows
+-------------+
| COUNT(year) |
+-------------+
|      388269 |
+-------------+
1 row in set (0.09 sec)
```

Note: 
- aggregate functions ignore NULL values

## Aggregate functions
The aggregate functions are:
1. COUNT
2. SUM
3. AVG
4. MAX
5. MIN
## Output of aggregate queries is also a table
Even though the value is a scalar, we still get output as a table.
It's a single-column-single-row table with column name being the aggregate part of the query, and value is the computed value.

```sql
mysql> SELECT COUNT(year) FROM movies;
+-------------+
| COUNT(year) |
+-------------+
|      388269 |
+-------------+
```

## Conclusion
Aggregate functions are used in finding a reduced value (avg, sum, count) or min/max values.

Note: in case of MIN, MAX, the result is the optimal value, not the row having the optimal value, this is important.
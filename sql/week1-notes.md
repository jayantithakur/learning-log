Day 1: SELECT + SELECT DISTINCT + COUNT + SELECT WHERE
Notes: COUNT(COLUMN) counts the non-null values in that column, not rows. COUNT(*) counts all rows. 

Day 2: ORDER BY + LIMIT
Notes: Syntax order - SELECT > FROM > WHERE > ORDER BY > LIMIT

Day 3: GROUP BY + AGGREGATIONS + HAVING 

    Aggregate functions:
    1. AVG(): returns average values, floating point - ROUND(AVG(COST),2)
    2. COUNT(): returns the number of VALUES
    3. MAX(): returns the maximum value
    4. MIN(): returns the minimum value
    5. SUM(): returns the sum of all VALUES

    Group By: 
    SELECT category_col, AGG(data_col) FROM TABLE
    WHERE
    GROUP BY category_col
    ORDER BY AGG(data_col)
    LIMIT 5;

Notes: For a group by on a date with timestamp:
SELECT DATE(Date_col) FROM table GROUP BY DATE(Date_col);

    Having: This allows us to filter AFTER an aggregation has already taken place.
    SELECT company, AGG(data_col) FROM TABLE
    WHERE company != 'GOOGLE'
    GROUP BY company
    HAVING AGG(data_col) > 1000;

Notes: ROUND - for display but filter HAVING on aggregates
example: SELECT c1, round(avg(c2),2) FROM TABLE
        GROUP BY c1
        HAVING avg(c2) > 2.90;

Day 4: BETWEEN + IN + LIKE, ILIKE

    Between: match values against a range of VALUES
    - SELECT * FROM table WHERE amount BETWEEN 8 AND 9;

    In: Use in cases where you want to check for multiple possible value options.
    - SELECT * FROM t1 WHERE colour IN ('Red','Blue','Green')

    Like/ilike: pattern matching.
    - Like: operators such as % or _ (case sensitive)
    - Ilike: case insensitive, only available in oracle sql

Day 5: JOINS + UNION
Joins allows us to combine information from multiple tables.

    Alias (as)
    - SELECT column_name AS updated_column_name (gets executed at the end of the query)

    INNER JOIN: Result with the set of records that match in both tables. 
    - SELECT * FROM t1 INNER JOIN t2 ON t1.column = t2.column;

    FULL OUTER JOIN: allows us to specify how to deal with values only present in one of the tables being joined.
    - SELECT * FROM t1 FULL OUTER JOIN t2 ON t1.column = t2.column;

    LEFT OUTER JOIN/LEFT JOIN: results in the set of records that are in the left table, if there is no match with the right table, the results are null.
    - SELECT * FROM t1 LEFT JOIN t2 ON t1.column = t2.column; 

    RIGHT OUTER JOIN/ RIGHT JOIN: essentially the same as a left join, except the tables are switched. ADD

    UNION: used to combine the result set of two or more SELECT statements (concatenate)
    - SELECT column_name(s) FROM t1
        UNION
    SELECT column_name(s) FROM t2;

Notes: UNION removes duplicates (thus, slower). UNION ALL keeps duplicates. ADD

MULTIPLE JOINS:
SELECT title, first_name, last_name FROM t1
INNER JOIN t2 on t1.actor_id = t2.actor_id
INNER JOIN t3 on t1.film_id = t2.film_id
WHERE first_name = 'Jayanti' AND last_name = 'Thakur'; 

Notes: How do you understand which join is required? 
Ask yourself: Do I want to see the rows that have no match?
    - if no, then INNER JOIN
    - if yes, from one table, then LEFT JOIN
    - if yes, from both table, then FULL JOIN.

Scenarios: 
1. How much did each customer pay? INNER JOIN
2. List all customers and how much they paid. LEFT JOIN
3. Customers that never paid. LEFT JOIN WITH IS NULL
4. Reconciliation : FULL OUTER JOIN, rare case (think of ODS activity)
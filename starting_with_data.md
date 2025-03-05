Question 1: 
Which cities and countries have the highest level of transaction revenues on the site
SQL Queries:
``` SELECT city, country, CAST(SUM(COALESCE(CAST(totaltransactionrevenue AS BIGINT),0))AS BIGINT) AS total_revenue
FROM all_sessions
GROUP BY city, country
HAVING CAST(SUM(COALESCE(CAST(totaltransactionrevenue AS BIGINT),0))AS BIGINT) > 0
ORDER BY total_revenue DESC
```

Answer: 



Question 2: 
Testing
SQL Queries:

Answer:



Question 3: 

SQL Queries:

Answer:



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:

Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
```
SELECT 
    city, 
    country, 
    CAST(SUM(COALESCE(CAST(totaltransactionrevenue AS BIGINT),0))AS BIGINT) AStotal_revenue
FROM 
    all_sessions
GROUP BY 
    city, 
    country
HAVING 
    CAST(SUM(COALESCE(CAST(totaltransactionrevenue AS BIGINT),0))AS BIGINT) > 0
ORDER BY 
    total_revenue DESC;
```

Answer:
![ans_Q1](/Users/erum/Documents/SQL_PICTURES/Ans_1.png)






**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:



Answer:





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:








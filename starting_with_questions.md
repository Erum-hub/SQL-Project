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
![ans_Q1](/Users/erum/project_pictures/Ans_1.png)






**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
```
SELECT 
    s.city, 
    s.country, ROUND(AVG(orderedquantity), 2) as avg_quantity
FROM 
    products p
JOIN 
    all_sessions s
ON 
    s.productsku = p.sku
GROUP BY 
    s.city, 
    s.country
```



Answer:
![ans_Q1](/Users/erum/project_pictures/Ans_1.png)





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
```
WITH Visitor_counts AS (
    SELECT 
        country, 
        CASE 
            WHEN city = '' THEN 'Unknown'
            ELSE city 
        END AS city, 
        v2productcategory, 
        COUNT(DISTINCT fullvisitorid) AS visitor_count
    FROM 
        all_sessions 
    GROUP BY 
        country, 
        CASE 
            WHEN city = '' THEN 'Unknown'
            ELSE city 
        END, 
        v2productcategory
)

SELECT 
    country, 
    city, 
    SUM(visitor_count) AS total_visitor_count
FROM 
    Visitor_counts
GROUP BY 
    country, 
    city
ORDER BY 
    SUM(visitor_count) DESC
    
```


Answer:
![ans_Q1](/Users/erum/project_pictures/Ans_1.png)




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**

```
SQL Queries:
WITH product_sales AS (
    SELECT 
        country, 
        city, 
        v2ProductName, 
        CAST(SUM(COALESCE(CAST(productrevenue AS BIGINT),0))AS BIGINT) AS total_revenue
    FROM 
        all_sessions
    WHERE 
        productRevenue IS NOT NULL
    GROUP BY 
        country, 
        city, 
        v2ProductName
), ranked_sales AS (
    SELECT 
        country, 
        city, 
        v2ProductName, 
        total_revenue,
        ROW_NUMBER() OVER (PARTITION BY country, city ORDER BY total_revenue DESC) AS rank
    FROM 
        product_sales
)
SELECT 
    country, 
    city, 
    v2ProductName AS top_selling_product, 
    total_revenue
FROM 
    ranked_sales
WHERE 
    rank = 1
ORDER BY 
    country, 
    city;
 ```



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**


SQL Queries:
```
WITH revenue_summary AS (
    SELECT 
        country, 
        city, 
        CAST(SUM(COALESCE(CAST(productrevenue AS BIGINT),0))AS BIGINT) AS total_revenue
    FROM 
        all_sessions
    GROUP BY 
        country, 
        city
)
SELECT 
    country, 
    city, 
    total_revenue,
    RANK() OVER (PARTITION BY country ORDER BY total_revenue DESC) AS city_rank
FROM 
    revenue_summary
ORDER BY 
    total_revenue DESC;
```

Answer:
![ans_Q1](/Users/erum/project_pictures/Ans_1.png)









What issues will you address by cleaning the data?





Queries:
Below, provide the SQL queries you used to clean your data.
During the data cleaning process, the following issues were identified and addressed.

1. Fixed Incorrect data type
2. Duplicate Rows
3. Null values
4. Inconsistent Date formats 

 ## Queries Executed
 ## 1. Fixed Incorrect data type and handled Null value
 - This Query Converts totaltransactionrevenue column to a BIGINT and converts Null value to 0
 ```
 SELECT 
    city, 
    country, 
    CAST(SUM(COALESCE(CAST(totaltransactionrevenue AS BIGINT),0))AS BIGINT) AS total_revenue
FROM 
    all_sessions
GROUP BY 
    city, 
    country
HAVING 
    CAST(SUM(COALESCE(CAST(totaltransactionrevenue AS BIGINT),0))AS BIGINT) > 0
ORDER BY 
    total_revenue DESC
    
 ```
 - The Query converts the unit_price column to INTEGER and divided by 1000000 to normalize the values

 ```
 SELECT Cast (unit_price AS INTEGER) / 1000000 AS unit_cost
FROM analytics
```

 ### 1. Removed Duplicate Rows
 Identified duplicates in fullvisitorid column
```
 SELECT 
    fullVisitorId, 
    COUNT(*) AS row_count
FROM 
    analytics
GROUP BY 
    fullVisitorId
HAVING 
    COUNT(*) > 1
```
### 3. Updated Date format
```
UPDATE 
    all_sessions
SET date = TO_DATE(date, 'YYYYMMDD')
WHERE 
    date IS NOT NULL;
```
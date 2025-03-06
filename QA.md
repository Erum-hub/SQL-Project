What are your risk areas? Identify and describe them.
DUPLICATE full visitor id - Various duplicates identified.
Duplicates SKU can lead to inaccuracies - No duplicates found


QA Process:
Describe your QA process and include the SQL queries used to execute it.
### This query Identifies duplicates in fullvisitorid
```
SELECT 
    fullVisitorid, 
    COUNT(*) AS row_count
FROM 
    analytics
GROUP BY 
    fullVisitorid
HAVING 
    COUNT(*) > 1
```
## This Query validates if SKU are unique
```
SELECT 
	sku,
	COUNT (*) AS Count_row
FROM
	products
GROUP BY
	sku
HAVING
	COUNT(*) >1
```
Successful creation of primary key validated that there are no duplicates
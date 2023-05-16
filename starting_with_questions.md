Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries: 
```SQL
--  Country

SELECT 	country, 
    	SUM(totaltransactionrevenue) AS total_revenue
FROM all_sessions
WHERE totaltransactionrevenue IS NOT Null
GROUP BY country
ORDER BY total_revenue DESC
LIMIT 5;
```
```SQL
--  City

SELECT 	city, 
    	SUM(totaltransactionrevenue) AS total_revenue
FROM all_sessions
WHERE city <> 'not available in demo dataset'
GROUP BY city
HAVING SUM(totaltransactionrevenue) IS NOT NULL
ORDER BY total_revenue DESC
LIMIT 5;
```



Answer:

![Country](https://github.com/rlmrezende/SQL-Project/assets/128871261/839a384f-6538-431e-b66d-c95e8c4e971d)


![City](https://github.com/rlmrezende/SQL-Project/assets/128871261/4deb225a-0ee5-4b07-bd5b-2fa2b344c413)


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
````SQL
-- City

SELECT 	city,
	CAST(AVG(p.orderedquantity) AS DECIMAL(10,0)) AS avg_products_ordered
FROM all_sessions as alls
JOIN products as p ON alls.productsku = p.sku
WHERE city IS NOT NULL
GROUP BY city
ORDER BY avg_products_ordered DESC
LIMIT 5;
````
````SQL
-- Country

SELECT 	country,
	CAST(AVG(p.orderedquantity) AS DECIMAL(10,0)) AS avg_products_ordered
FROM all_sessions as alls
JOIN products as p ON alls.productsku = p.sku
GROUP BY country
ORDER BY avg_products_ordered DESC
LIMIT 5;
````

Answer:

![City](https://github.com/rlmrezende/SQL-Project/assets/128871261/f67fa9bc-6658-46af-baf5-9a3a78d24584)

![Country](https://github.com/rlmrezende/SQL-Project/assets/128871261/0b8c76a9-12e3-4965-974f-d1f79f6368fe)



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
````SQL
-- Country

SELECT 	country,
	v2productcategory AS product_category,
    	SUM(orderedquantity) AS total_ordered_quantity
FROM all_sessions AS alls
JOIN products AS p ON alls.productsku = p.sku
GROUP BY country, v2productcategory
HAVING SUM(orderedquantity) = 
	(
    SELECT MAX(sum_ordered_quantity)
    FROM (
        SELECT	country,
            	v2productcategory,
            	SUM(orderedquantity) AS sum_ordered_quantity
        FROM all_sessions AS alls2
        JOIN products AS p2 ON alls2.productsku = p2.sku
        GROUP BY country, v2productcategory
    	) AS total_ordered_quantity_by_category
    WHERE total_ordered_quantity_by_category.country = alls.country
)
ORDER BY total_ordered_quantity DESC
LIMIT 5;
````
````SQL
-- City

SELECT 	city,
	v2productcategory AS product_category,
    	SUM(orderedquantity) AS total_ordered_quantity
FROM all_sessions AS alls
JOIN products AS p ON alls.productsku = p.sku
WHERE city <> '(not set)'
GROUP BY city, v2productcategory
HAVING SUM(orderedquantity) = 
	(
    SELECT MAX(sum_ordered_quantity)
    FROM (
        SELECT	city,
            	v2productcategory,
            	SUM(orderedquantity) AS sum_ordered_quantity
        FROM all_sessions AS alls2
        JOIN products AS p2 ON alls2.productsku = p2.sku
        GROUP BY city, v2productcategory
    	) AS total_ordered_quantity_by_category
    WHERE city <> 'not available in demo dataset' AND total_ordered_quantity_by_category.city = alls.city
)
ORDER BY total_ordered_quantity DESC
LIMIT 5;
````

Answer:

![Country](https://github.com/rlmrezende/SQL-Project/assets/128871261/f7b86032-bbb3-40a6-82c9-40568a959bcf)

![City](https://github.com/rlmrezende/SQL-Project/assets/128871261/82d5ed29-05a3-4a6c-92b7-3ae6c8539612)




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:








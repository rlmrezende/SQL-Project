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

SELECT 	country AS Name,
   	v2productcategory AS product_category,
    	CAST(AVG(p.orderedquantity) AS DECIMAL(10,0)) AS avg_products_ordered
FROM all_sessions AS alls
JOIN 
    products AS p 
		ON alls.productsku = p.sku
GROUP BY country, v2productcategory
ORDER BY avg_products_ordered DESC
LIMIT 8;
````
````SQL
-- City

SELECT 	city AS Name,
   	v2productcategory AS product_category,
    	CAST(AVG(p.orderedquantity) AS DECIMAL(10,0)) AS avg_products_ordered
FROM all_sessions AS alls
JOIN 
    products AS p 
		ON alls.productsku = p.sku
GROUP BY city, v2productcategory
ORDER BY avg_products_ordered DESC
LIMIT 8;
````

Answer:

![Country](https://github.com/rlmrezende/SQL-Project/assets/128871261/5c61105b-fc42-433c-8060-fae371dfeed7)

![City](https://github.com/rlmrezende/SQL-Project/assets/128871261/9260625d-897a-43de-8222-0651c45abece)




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:








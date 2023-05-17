### Question 1: What are the top 10 most popular products based on unique visitor IDs?

SQL Queries:
````SQL
SELECT 	COUNT(DISTINCT visitid) AS visitors,
	  	v2productname AS product_name
FROM all_sessions
GROUP BY v2productname
ORDER BY visitors DESC
LIMIT 10;
````
Answer:

![image](https://github.com/rlmrezende/SQL-Project/assets/128871261/bf7e0cb1-ccc9-4204-a1ec-31a65c4f1acb)


### Question 2: List the products that have only been visited by one unique user

SQL Queries:
````SQL
SELECT 	DISTINCT v2productname AS product_name,
	  	COUNT(visitid) AS visitors
FROM all_sessions
GROUP BY v2productname
HAVING COUNT(DISTINCT visitid) = 1
ORDER BY visitors DESC;
````
Answer: Returns a list of 30 products that have only been visited by one unique user, which can be analyzed to determine why there is such low visitation for these products.

![image](https://github.com/rlmrezende/SQL-Project/assets/128871261/342ec773-071f-4268-a6bd-61485e89c961)



### Question 3: What is the total revenue broken down by year?

SQL Queries:
````SQL
SELECT 	EXTRACT(YEAR from date) AS year, 
		SUM(totaltransactionrevenue) AS total_revenue
FROM all_sessions
WHERE totaltransactionrevenue IS NOT NULL
GROUP BY year
ORDER BY year;
````
Answer: 

![image](https://github.com/rlmrezende/SQL-Project/assets/128871261/c6e1e85a-d1c5-4a46-a7b1-626509b2e46c)




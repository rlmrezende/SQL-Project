Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries: 
```SQL
--  Country

SELECT country, SUM(totaltransactionrevenue) AS total_revenue
FROM all_sessions
WHERE totaltransactionrevenue IS NOT Null
GROUP BY country
ORDER BY total_revenue DESC
LIMIT 5;
```
```SQL
--  City

SELECT city, SUM(totaltransactionrevenue) AS total_revenue
FROM all_sessions
WHERE city <> 'not available in demo dataset'
GROUP BY city
HAVING SUM(totaltransactionrevenue) IS NOT NULL
ORDER BY total_revenue DESC
LIMIT 5;
```



Answer:

![image](https://github.com/rlmrezende/SQL-Project/assets/128871261/839a384f-6538-431e-b66d-c95e8c4e971d)


![image](https://github.com/rlmrezende/SQL-Project/assets/128871261/4deb225a-0ee5-4b07-bd5b-2fa2b344c413)


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








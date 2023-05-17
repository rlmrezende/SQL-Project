What are your risk areas? Identify and describe them.
1. Checking the values between sales_report and sales_by_sku to gain a better understanding of their relationship.
2. Examining the all_sessions table more closely
#
QA Process:
Describe your QA process and include the SQL queries used to execute it.

1. Checking the values between sales_report and sales_by_sku to gain a better understanding of their relationship.
 
Question: Can we drop the sales_by_sku table? 

````SQL
SELECT 
    SUM(ss.total_ordered) AS total_ordered_sales_by_sku,
    SUM(sr.total_ordered) AS total_ordered_sales_report
FROM sales_by_sku ss
FULL OUTER JOIN sales_report sr ON ss.total_ordered = sr.total_ordered;
````
![image](https://github.com/rlmrezende/SQL-Project/assets/128871261/5aff0ba2-60b7-410b-ab0b-ab5bb7eaf9ff)

````SQL
SELECT 
    COUNT(ss.productsku) AS total_by_sku,
    COUNT(sr.productsku) AS total_by_sku_report
FROM sales_by_sku ss
FULL OUTER JOIN sales_report sr ON ss.productsku = sr.productsku;
````
![image](https://github.com/rlmrezende/SQL-Project/assets/128871261/e2819612-f185-4044-9531-b1acff5ef0f3)

Answer: It seems that there are 8 productsku values that exist in the sales_by_sku table but are missing in the sales_report table. Further investigation is needed before deciding to drop the table.

2. Examining the all_sessions table more closely

````SQL
SELECT visitid,
       transactions,
       transactionid, 
       productquantity, 
       productrevenue, 
       transactionrevenue, 
       totaltransactionrevenue 
FROM all_sessions
WHERE transactionid IS NOT NULL
````
![image](https://github.com/rlmrezende/SQL-Project/assets/128871261/61773270-dcab-432e-a31d-0f2c289b180e)

Upon analyzing the all_sessions table, we found that filtering by the transactionid column yields only 9 records. However, out of these records, we have identified 5 rows with null values in the productquantity column and 5 rows with null values in the productrevenue column. These findings suggest a potential data inconsistency, which requires further investigation.

 - Checking the total of orders:
````SQL
SELECT visitid,
	      transactions,
       transactionid, 
       productquantity, 
       productrevenue, 
       transactionrevenue, 
       totaltransactionrevenue 
FROM all_sessions
WHERE transactions IS NOT NULL
ORDER BY transactionid;
````
![image](https://github.com/rlmrezende/SQL-Project/assets/128871261/7ca81ac5-4bad-4a9f-896c-94dec12900eb)

After filtering the all_sessions table by transactions, we found that there are 81 rows. with those 9 transactionid include. However, when we add the condition that productquantity is not null, the output returns only 18 rows, of which only 4 rows have a transactionid. This discrepancy raises concerns about the accuracy of the 81 rows as the total number of orders. How can we be certain about the accuracy of these results?

````SQL
SELECT visitid,
       transactions,
       transactionid, 
       productquantity, 
       productrevenue, 
       transactionrevenue, 
       totaltransactionrevenue 
FROM all_sessions
WHERE totaltransactionrevenue IS NOT NULL
ORDER BY transactionid;
````
Although, if we filter by the column totaltransactionrevenue, we get the same result of 81 rows. Could this be the actual total number of orders?

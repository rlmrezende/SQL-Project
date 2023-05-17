What are your risk areas? Identify and describe them.
1. Checking the values between sales_report and sales_by_sku to gain a better understanding of their relationship.

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

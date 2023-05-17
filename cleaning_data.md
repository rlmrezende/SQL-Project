What issues will you address by cleaning the data?

1. Removing empty columns using the DROP function.
2. Removing duplicate columns using the DROP function.
3. Changing the data type for better understanding.
4. The unit cost in the data needs to be divided by 1,000,000.

Queries:
Below, provide the SQL queries you used to clean your data.




1. Removing empty columns using the DROP function:
````SQL
ALTER TABLE all_sessions 
  DROP COLUMN itemquantity,
  DROP COLUMN itemrevenue,
  DROP COLUMN searchkeyword;
````
````SQL
ALTER TABLE analytics 
  DROP COLUMN userid;
````

2. Removing duplicate columns using the DROP function:
````SQL
ALTER TABLE sales_report 
  DROP COLUMN name, 
  DROP COLUMN stocklevel, 
  DROP COLUMN restockingleadtime,
  DROP COLUMN sentimentscore,
  DROP COLUMN sentimentmagnitude;
````

3. Changing the data type for better understanding:
````SQL
-- analytics

ALTER TABLE analytics 
  ALTER COLUMN revenue TYPE decimal(15,2) 
  USING (revenue::decimal);

ALTER TABLE analytics 
  ALTER column unit_price TYPE decimal(10,2) 
  USING (unit_price::decimal);

-- all_sessions

ALTER TABLE all_sessions 
  ALTER column productprice TYPE decimal(10,2) 
  USING (productprice::decimal);
  
ALTER TABLE all_sessions 
  ALTER column totaltransactionrevenue TYPE decimal(15,2) 
  USING (totaltransactionrevenue::decimal);
  
ALTER TABLE all_sessions 
  ALTER column productrevenue TYPE decimal(15,2) 
  USING (productrevenue::decimal);
````

4. The unit cost in the data needs to be divided by 1,000,000:
````SQL
  -- analytics 
  
UPDATE analytics 
  SET unit_price = (unit_price/1000000);

UPDATE analytics 
  SET revenue = (revenue/1000000);

-- all_sessions 

UPDATE all_sessions 
  SET productprice = (productprice/1000000);

UPDATE all_sessions 
  SET totaltransactionrevenue = (totaltransactionrevenue/1000000);
````

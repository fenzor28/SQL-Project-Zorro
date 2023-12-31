# What issues will you address by cleaning the data?

## Duplicate Records:
   Removing the same piece of data being entered more than once, which can lead to biased analyses.

## Inconsistent formatting:
   Ensuring that each column has the appropriate data type, converting them if needed.

## Handle Missing Values: 
   Identifying and handling missing values

## Text Cleaning:
   Removing unnecessary whitespace, special characters, or punctuation in text data. By addressing these issues, we can ensure that the data is complete, correct, and relevant to the problem we're trying to solve, leading to more accurate and reliable insights.





# Queries:


## ALL_SESSIONS TABLE

In a dataset that captures visitor sessions, it's common to have multiple rows for the same visitor, representing different sessions or interactions. Therefore, a single column might not be unique across the entire dataset. I decided to add an Auto-Incremented ID.

By performing the same query below for each column I found that some columns have duplicates.
```
SELECT fullvisitorid, COUNT(*)
FROM all_sessions
GROUP BY fullvisitorid
HAVING count(*) > 1
```

This query will show the data types of all columns in the table. This is to verify that all columns have been converted to the correct data types
```
SELECT column_name, data_type 
FROM information_schema.columns 
WHERE table_name = 'all_sessions'
```

This query will update only the rows where the value is '(other)' in the column channelgrouping, removing the parentheses from that specific value 
```
UPDATE all_sessions
SET channelgrouping = SUBSTRING(channelgrouping, 2, LENGTH(channelgrouping) - 2)
WHERE channelgrouping = '(Other)'
```

Since the data was gathered before 2018, Retaining the historical name Macedonia (FYROM) might be beneficial but it's not necessary for my analysis. It's also to maintain consistent formatting across the countries.
```
UPDATE all_sessions 
SET country = 'Macedonia'
WHERE country = 'Macedonia (FYROM)'
```

The name change from "Burma" to "Myanmar" is tied to historical, ethnic, and political factors. Myanmar is the official name recognized by the United Nations and many countries so I decided to use it instead of Burma for consistent formatting across the countries.
```
UPDATE all_sessions 
SET country = 'Myanmar'
WHERE country = 'Myanmar (Burma)'
```

Placeholder values like "(not set)" or "not available in demo dataset" are not standardized and can be confusing.
Replacing them with a consistent value like "Unknown" makes it clear that the information is not available.
```
UPDATE all_sessions
SET city = 'Unknown'
WHERE city = '(not set)' OR city = 'not available in demo dataset'
```
```
UPDATE all_sessions
SET country = 'Unknown'
WHERE country = '(not set)'
```
```
UPDATE all_sessions
SET v2productcategory = 'Unknown'
WHERE v2productcategory = '(not set)'
```


Dividing the values in column "productprice" by 1,000,000 would convert the values to a more standard unit like dollars. This would make the data more interpretable and consistent. To maintain consistency in the dataset, I applied the same scaling to other monetary-related columns.
The same query was used in the analytics table for consistency.

Here's a list of columns:
1) totaltransactionrevenue
2) productrevenue
3) transactionrevenue

The columns 'productrefundamount' and 'itemrevenue' were not included because they contain no values
```
UPDATE all_sessions
SET productprice = productprice / 1000000,
    totaltransactionrevenue = totaltransactionrevenue / 1000000,
    productrevenue = productRevenue / 1000000,
    transactionRevenue = transactionRevenue / 1000000
```

## ANALYTICS TABLE

By performing the same query below for each column I found that every column have duplicates, therefore none of the columns can be the primary key
```
SELECT fullvisitorid, COUNT(*)
FROM all_sessions
GROUP BY fullvisitorid
HAVING count(*) > 1
```
This query was used to identify duplicated records using the GROUP BY clause

```
SELECT
	visitnumber,
	visitid,
	visitstarttime,
	date,
	fullvisitorid,
	channelgrouping,
	pageviews,
	bounces,
	unitprice,
	COUNT(*)
FROM analytics
GROUP BY visitnumber, visitid, visitstarttime, fullvisitorid, date, channelgrouping, pageviews, bounces, unitprice
HAVING COUNT(*) > 1
```

This query was used to delete duplicate records based on a combination of multiple columns
```
WITH DuplicateRows AS (
    SELECT ctid, ROW_NUMBER() OVER(PARTITION BY visitnumber, visitid, visitstarttime, date, fullvisitorid, channelgrouping, pageviews,           bounces, unitprice ORDER BY ctid) AS rn
    FROM analytics
)
DELETE FROM analytics
WHERE ctid IN ( SELECT ctid
		FROM DuplicateRows
		WHERE rn > 1
	      )
```

This query will update only the rows where the value is '(other)' in the column channelgrouping, removing the parentheses from that specific value 
```
UPDATE analytics
SET channelgrouping = SUBSTRING(channelgrouping, 2, LENGTH(channelgrouping) - 2)
WHERE channelgrouping = '(Other)'
```


Update the columns 'revenue' and 'unitprice' to it's appropriate data type
```
ALTER TABLE analytics
ALTER COLUMN unitprice TYPE FLOAT
```

To change the column 'visitstarttime' from int data type to a time format without the date, I had to perform the conversion in two steps: first to a timestamp and then to a time.
```
ALTER TABLE analytics
ALTER COLUMN visitstarttime TYPE TIMESTAMP USING to_timestamp(visitstarttime)
```
```
ALTER TABLE analytics
ALTER COLUMN visitstarttime TYPE TIME USING CAST(visitstarttime AS TIME)
```

Deleting a column with a redundant value to reduce data redundancy and improve data integrity
```
ALTER TABLE my_table
DROP COLUMN old_column;
```


## PRODUCTS TABLE

Checking for duplicates. The 'sku' (Stock Keeping Unit) column appears to be a unique identifier for each product
```
SELECT sku, COUNT(*)
FROM products
GROUP BY sku
HAVING COUNT(*) > 1
```

For consistent formatting, this query will remove any extra spaces at the beginning and end of the 'name' values
```
UPDATE products
SET name = TRIM(name)
```

To maintain consistency across all the related columns in different tables that share the same name
```
ALTER TABLE products
RENAME COLUMN sku to productsku
```


## SALES_BY_SKU TABLE

Checking for duplicates. The 'productsku' column appears to be a unique identifier for each product
```
SELECT productsku, COUNT(*) 
FROM sales_by_sku
GROUP BY productsku
HAVING COUNT(*) > 1
```

## SALES_REPORT TABLE

Checking for duplicates. The 'productsku' column appears to be a unique identifier for each product
```
SELECT productsku, COUNT(*) 
FROM sales_report
GROUP BY productsku
HAVING COUNT(*) > 1
```
For consistent formatting, this query will remove any extra spaces at the beginning and end of the 'name' values
```
UPDATE sales_report
SET name = TRIM(name)
```























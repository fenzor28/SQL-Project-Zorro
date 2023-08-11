# What are your risk areas? Identify and describe them.
## Missing values:
    It can distort the true representation of data, leading to inaccurate results and conclusions. Not handling this properly can lead to making wrong business or research decisions.

## Loss of Information:
     Accidental deletion or modification of data during cleaning or transformation can lead to data loss.

## Determining the Reason for Missingness:
     Before deciding how to handle missing data, it's essential to understand why it's missing. Is it missing completely at random? Is it missing based on some observed data, or is it missing based on some unobserved data? I'm not sure how to properly approach this scenario.

## Normalization of Text:
     Some columns have inconsistencies in text data, such as different cases (upper/lower) and extra spaces and alternate words

## Data redundancy:
    Handling redundant rows or columns that contain similar information improperly can result to biases in the analysis 
    productSKU: All 454 rows have unique SKUs
    name: There are 113 product names with duplicates, which suggests that some SKUs might be associated with the same product name.


# QA Process:
Describe your QA process and include the SQL queries used to execute it.

## Uniqueness Check 
```
SELECT sku, COUNT(*)
FROM products
GROUP BY sku
HAVING COUNT(*) > 1
```

## Missing values
```
SELECT COUNT(*) as total_rows
FROM all_sessions
```
```
SELECT COUNT(*) - COUNT(totalTransactionRevenue) as missing_values
FROM all_sessions
```
## Data Integrity and Consistency

Check for negative values in 'totaltransactionrevenue'
```
SELECT COUNT(*) AS invalid_revenue_rows
FROM all_sessions
WHERE totaltransactionrevenue < 0
```
Check for future dates
```
SELECT COUNT(*) AS future_date_rows
FROM all_sessions
WHERE date > CURRENT_DATE
```
Check for unexpected values in 'channelGrouping'
```
SELECT channelgrouping, COUNT(*) 
FROM all_sessions
WHERE channelGrouping NOT IN ('Organic Search', 'Other', 'Display', 'Referral','Paid Search', 'Affiliates', 'Direct' ) -- list expected values here
GROUP BY channelgrouping
```
Ensure non-negative values for 'orderedquantity' column
```
SELECT COUNT(*) AS negative_ordered_quantity_rows
FROM products
WHERE orderedquantity < 0
```



# What are your risk areas? Identify and describe them.
1) Missing values:
   It can distort the true representation of data, leading to inaccurate results and conclusions. Not hadling this properly can lead to making wrong business or research decisions.

2) Loss of Information:
   Accidental deletion or modification of data during cleaning or transformation can lead to data loss.

3) Determining the Reason for Missingness:
    Before deciding how to handle missing data, it's essential to understand why it's missing. Is it missing completely at random? Is it missing based on some observed data, or is it      missing based on some unobserved data? I'm not sure how to properly approach this scenario.

4) Normalization of Text:
   Some columns have inconsistencies in text data, such as different cases (upper/lower) and extra spaces and alternate words

5) Data redundancy:
   Handling redundant rows or columns that contain similar information improperly can result to biases in the analysis



# QA Process:
Describe your QA process and include the SQL queries used to execute it.

Uniqueness Check 
```
SELECT sku, COUNT(*)
FROM products
GROUP BY sku
HAVING COUNT(*) > 1
```


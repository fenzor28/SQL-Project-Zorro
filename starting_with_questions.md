Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?


SQL Queries:
```
SELECT 
	city,
	country,
	SUM(totaltransactionrevenue) as total_revenue
FROM all_sessions 
WHERE totaltransactionrevenue IS NOT NULL 
	AND city != 'Unknown'
GROUP BY country, city
ORDER BY total_revenue DESC
```

Answer: 1) San Francisco, United States
        2) Sunnyvale, United States
        3) Atlanta, United States
        4) Palo Alto, United States
        5) Tel Aviv-Yafo, Israel
        



**Question 2: What is the average number of products ordered from visitors in each city and country?


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








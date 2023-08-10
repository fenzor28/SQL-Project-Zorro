#Answer the following questions and provide the SQL queries used to find the answer.

    
## Question 1: Which cities and countries have the highest level of transaction revenues on the site?


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

Answer: 
1) San Francisco, United States
2) Sunnyvale, United States
3) Atlanta, United States
4) Palo Alto, United States
5) Tel Aviv-Yafo, Israel
        


## Question 2: What is the average number of products ordered from visitors in each city and country?


SQL Queries:
```
SELECT 
	a.country,
	a.city,
	ROUND(AVG(p.orderedquantity)) AS avg_products_ordered
FROM all_sessions a
JOIN products p 
	ON a.productsku = p.productsku
WHERE country != 'Unknown' AND city != 'Unknown' 
GROUP BY a.country, a.city
ORDER BY a.country, avg_products_ordered DESC
```
Answer: Results for the country Argentina

| country | city | avg_products_ordered |
| ----------- | ----------- |------------|
| Argentina | Santa Fe | 1933 |
| Argentina | Buenos Aires | 435 |
| Argentina | Rosario | 433 |




## Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
```
WITH RankedCategories AS (
SELECT 
	country,
	city,
	v2productcategory,
	COUNT(*) AS no_of_orders,
	RANK() OVER (PARTITION BY country, city ORDER BY COUNT(*) DESC) AS rank
FROM all_sessions
WHERE v2productcategory IS NOT NULL AND v2productcategory != 'Unknown'
	AND city != 'Unknown' AND country != 'Unknown'
GROUP BY country, city, v2productcategory
)
SELECT 
	country,
	city,
	v2productcategory,
	no_of_orders,
	rank
FROM RankedCategories
WHERE rank <= 3
```


Answer: 
1) The category " Home/Shop by Brand/YouTube/ " appears to be consistenly popular in various cities like Bribane, Melbourne and 	        Sydney in Australia
2) The category " Home/Shop by Brand/YouTube/ " appears globally popular among the major countries like Australia,
   Canada, United States, Germany, India and United Kingdom.
3) It's evident that Youtube is a popular product category across the top countries and cities.




## Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:



Answer:





## Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
```
WITH CountryRevenue AS (
	SELECT 
		country,
	  	SUM(totaltransactionrevenue) as country_total_revenue
	FROM all_sessions
	WHERE totaltransactionrevenue IS NOT NULL
	GROUP BY country
	ORDER BY country_total_revenue DESC
)

SELECT 
	a.country,
	a.city,
	b.country_total_revenue,
	SUM(a.totaltransactionrevenue) as city_total_revenue
FROM all_sessions a
JOIN CountryRevenue b ON a.country = b.country
WHERE a.totaltransactionrevenue IS NOT NULL 
	AND a.country != 'Unknown' AND a.city != 'Unknown'
GROUP BY a.country, a.city, b.country_total_revenue
ORDER BY city_total_revenue DESC
```


Answer: It's evident that the United States, particularly cities like San Francisco, Sunnyvale and Atlanta, have contributed significantly to the revenue







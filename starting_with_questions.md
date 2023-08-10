Answer the following questions and provide the SQL queries used to find the answer.

    
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
1) The category " Home/Shop by Brand/YouTube/ " appears to be consistently popular in various cities like Bribane, Melbourne and 	        Sydney in Australia
2) The category " Home/Shop by Brand/YouTube/ " appears to be popular globally among the major countries like Australia,
   Canada, United States, Germany, India and United Kingdom.
3) It's evident that Youtube is a popular product category across the major countries and cities.




## Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
```

WITH TopSales AS (
 SELECT
	a.country,
	a.city,
	s.name AS product_name,
	s.total_ordered,
	ROW_NUMBER() OVER (PARTITION BY a.country, a.city ORDER BY s.total_ordered DESC) AS rank
FROM all_sessions a
JOIN sales_report s
	ON a.productsku = s.productsku
WHERE country != 'Unknown' AND city != 'Unknown' 
	AND s.total_ordered > 0
) 

SELECT
	country,
	city,
	product_name,
	total_ordered
FROM TopSales
WHERE rank = 1
ORDER BY country, city
```


Answer: Results for the country Japan


| country | city | product_name | total_ordered |
| ----------- | ----------- |------------| ------ |
| Japan | Minato | Sunglasses | 146 |
| Japan | Mountain View | 5-Panel Snapback Cap | 7 | 
| Japan | Osaka | Protect Smoke + CO White Wired Alarm-USA | 42 |
| Japan | Shinjuku | 17oz Stainless Steel Sport Bottle | 334 |
| Japan | Yokohama | Slim Utility Travel Bag | 13 |


### Patterns worthy of noting:

There are 79 unique products in the list of top-selling products across various cities/countries. This suggests a diverse range of products gaining popularity.
```
WITH TopSales AS (
 SELECT
	a.country,
	a.city,
	s.name as product_name,
	s.total_ordered,
	ROW_NUMBER() OVER (PARTITION BY a.country, a.city ORDER BY s.total_ordered DESC) AS rank
FROM all_sessions a
JOIN sales_report s
	ON a.productsku = s.productsku
WHERE country != 'Unknown' AND city != 'Unknown' 
	AND s.total_ordered > 0
) 

SELECT COUNT(DISTINCT product_name) AS "Number of Unique Top-Selling Product"
FROM TopSales
WHERE rank = 1
```
While there's diversity, some products such as "Ballpoint LED Light Pen", "Hard Cover Journal", and "Blackout Cap" appear to be universally popular, leading sales in multiple areas.

```
WITH TopSales AS (
 SELECT
	a.country,
	a.city,
	s.name AS product_name,
	s.total_ordered,
	ROW_NUMBER() OVER (PARTITION BY a.country, a.city ORDER BY s.total_ordered DESC) AS rank
FROM all_sessions a
JOIN sales_report s
	ON a.productsku = s.productsku
WHERE country != 'Unknown' AND city != 'Unknown' 
	AND s.total_ordered > 0
) 

SELECT 
	product_name,
	COUNT(*) AS "Number of Cities/Countries"
FROM TopSales
WHERE rank = 1
GROUP BY product_name
	ORDER BY "Number of Cities/Countries" DESC
LIMIT 3
```






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

Answer: 
It's evident that the United States, particularly cities like San Francisco, Sunnyvale and Atlanta, have contributed significantly to the revenue







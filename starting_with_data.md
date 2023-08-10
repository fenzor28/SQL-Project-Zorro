# Questions I Made Up

## Question 1: Are there products with high stock levels but low sales, indicating overstocking? What strategies can be applied to clear this inventory?

SQL Queries: 
```
SELECT 
	name as product_name,
	stocklevel,
	orderedquantity
FROM products
WHERE stocklevel > 100 AND orderedquantity < 60
ORDER BY stocklevel DESC
```

Answer: 1) Men's Watershed Full Zip Hoodie Grey
	2) Men's Short Sleeve Hero Tee Charcoal
 	3) Men's Long and Lean Tee Charcoal
  	4) Tri-blend Hoodie Grey



## Question 2: 
What are the top 3 infant products with low stock levels that might risk going out of stock soon?​

SQL Queries:
```
SELECT 
	name as product_name,
	stocklevel,
	orderedquantity
FROM products
WHERE stocklevel < 10 AND orderedquantity > 2
 AND name LIKE 'Infant%'
ORDER BY stocklevel 
LIMIT 3
```

Answer: 1) Infant Short Sleeve Tee Red
	2) Infant Short Sleeve Tee White
 	3) Infant Short Sleeve Tee Royal Blue



## Question 3:
Which products are the most commonly bought together?

SQL Queries: 
```
WITH ProductPairs AS (
	SELECT a.v2productname as product_a,
	  	   b.v2productname as product_b
	FROM all_sessions a
	JOIN all_sessions b
		ON a.fullvisitorid = b.fullvisitorid
	AND a.v2productname != b.v2productname
)
SELECT 
	product_a,
	product_b,
	COUNT(*) AS pair_count
FROM ProductPairs
GROUP BY product_a, product_b
ORDER BY pair_count DESC
LIMIT 10
```
Answer: Nest® Protect Smoke + CO Black Battery Alarm-USA and Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel
	
 	

## Question 4: 

Which channel is resposible for attracting the highest number of user sessions on the platform?

SQL Queries: 
```
SELECT channelgrouping, COUNT(*) AS no_of_sessions
FROM all_sessions
GROUP BY channelgrouping
ORDER BY no_of_sessions DESC
```
Answer:
Organic Search: indicating that users are finding the platform through seach engine results.


Question 5: 

SQL Queries:

Answer:

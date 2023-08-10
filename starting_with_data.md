Question 1: 
Are there products with high stock levels but low sales, indicating overstocking? What strategies can be applied to clear this inventory?

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



Question 2: 
What are the top 3 infant products with low stock levels that might risk going out of stock soon?​

SQL Queries:
What are the top 3 infant products with low stock levels that might risk going out of stock soon?​
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



Question 3:
Which channel is resposible for attracting the highest number of user sessions on the platform?

SQL Queries: 
```
SELECT channelgrouping, COUNT(*) AS no_of_sessions
FROM all_sessions
GROUP BY channelgrouping
ORDER BY no_of_sessions DESC

Answer:



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:

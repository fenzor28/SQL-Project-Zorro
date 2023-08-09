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

Answer: Men's Watershed Full Zip Hoodie Grey
	Men's Short Sleeve Hero Tee Charcoal
 	Men's Long and Lean Tee Charcoal
  	Tri-blend Hoodie Grey



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

Answer:



Question 3: 

SQL Queries:

Answer:



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:

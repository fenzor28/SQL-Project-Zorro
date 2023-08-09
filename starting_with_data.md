Question 1: Are there products with high stock levels but low sales, indicating overstocking? What strategies can be applied to clear this inventory?

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

Answer: 



Question 2: 

SQL Queries:

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

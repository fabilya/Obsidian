
```SQL
SELECT *
FROM customers
WHERE country='Mexico' OR country='Germany' or country='USA' or country='Canada'

-- с использованием IN
SELECT *
FROM customers
WHERE country IN ('Mexico', 'Germany', 'USA', 'Canada')

SELECT *
FROM products
WHERE category_id NOT IN (1, 3, 5, 7)
```
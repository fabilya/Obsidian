
`ANY` - возвращает истину, если условие истинно для всех значений в подзапросе.

Выбрать все уникальные компании заказчиков, которые делали заказы боле чем на 40 единиц товаров
```SQL
SELECT DISTINCT company_name, quantity
FROM customers
JOIN orders USING(customer_id)
JOIN order_details USING(order_id)
WHERE quantity > 40;

-- с подзапросом
SELECT customer_id
FROM orders
JOIN order_details USING(order_id)
WHERE quantity > 40;

-- основной запрос
SELECT DISTINCT company_name
FROM customers
WHERE customer_id = ANY(
	SELECT customer_id
	FROM orders
	JOIN order_details USING(order_id)
	WHERE quantity > 40
)
```

Выбрать продукты, количество которых больше среднего по заказам
```SQL
-- подзапрос
SELECT AVG(quantity)
FROM order_details
-- 23.8

-- основной запрос
SELECT DISTINCT product_name, quantity
FROM products
JOIN order_details USING(product_id)
WHERE quantity > (SELECT AVG(quantity)
			  	  FROM order_details
)
ORDER BY quantity
```

`ALL` - для сравнения значения с каждым значением в подзапросе. Запрос возвращает истину, если сравнение истинно для всех значений, возвращаемых подзапросом.


Найти все продукты, количество которых больше среднего значения количества заказанных товаров из групп, полученных группированием по `product_id`
```SQL
-- подзапрос
SELECT AVG(quantity)
FROM order_details
GROUP BY product_id;


-- основной запрос
SELECT DISTINCT product_name, quantity
FROM products
JOIN order_details USING(product_id)
WHERE quantity > ALL (SELECT AVG(quantity)
					   FROM order_details
					   GROUP BY product_id
)
ORDER BY quantity 
```



Работа `HAVING` во многом аналогична применению `WHERE`; но `WHERE` применяется для фильтрации строк, а `HAVING` — для фильтрации групп

Исключим из выборки все группы, в которых сумма кассовых сборов равна `NULL`:
```SQL
SELECT product_type,
       SUM(gross)
FROM video_products
GROUP BY product_type
-- Это условие относится к группам:
HAVING SUM(gross) IS NOT NULL;
-- ('Фильм', 318868922) 
```
___
```SQL
-- сгруппировать по категории, посчитать сумму товаров в категории, которые в продаже и вывести те категории, в которых сумма превышает 5000 по убыванию
SELECT category_id, SUM(unit_price * units_in_stock)
FROM products
WHERE discontinued <> 1
GROUP BY category_id
HAVING SUM(unit_price * units_in_stock) > 5000
ORDER BY SUM(unit_price * units_in_stock) DESC
	8	13010.349914550781
	2	11926.04999923706
	1	11365.25
	4	11271.199989318848
	3	10392.200072288513
	5	5230.5
```
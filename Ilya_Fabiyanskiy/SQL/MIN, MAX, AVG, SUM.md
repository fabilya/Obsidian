
```SQL
-- поиск самого старого заказа из London
SELECT ship_city, order_date
FROM orders
WHERE ship_city = 'London'
ORDER BY order_date;

-- тоже самое, с использованием MIN
SELECT MIN(order_date)
FROM orders
WHERE ship_city='London';

-- поиск самого нового заказа из London
SELECT ship_city, order_date
FROM orders
WHERE ship_city = 'London'
ORDER BY order_date DESC;

-- тоже самое, с испозованием MAX
SELECT MAX(order_date)
FROM orders
WHERE ship_city='London';

-- средняя цена по всем продуктам, которые в продаже
SELECT AVG(unit_price)
FROM products
WHERE discontinued <> 1

-- сумма всех продуктов в продаже
SELECT SUM(units_in_stock)
FROM products
WHERE discontinued <> 1
```
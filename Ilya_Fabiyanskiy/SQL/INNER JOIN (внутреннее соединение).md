```SQL
SELECT product_name, suppliers.company_name, units_in_stock
FROM products
INNER JOIN suppliers ON products.supplier_id = suppliers.supplier_id
ORDER BY units_in_stock DESC;

SELECT category_name, SUM(units_in_stock)
FROM products
INNER JOIN categories ON products.category_id = categories.category_id
GROUP BY category_name
ORDER BY SUM(units_in_stock) DESC
LIMIT 5;

SELECT category_name, SUM(unit_price * units_in_stock)
FROM products
INNER JOIN categories ON products.category_id = categories.category_id
WHERE discontinued <> 1
GROUP BY category_name
HAVING SUM(unit_price * units_in_stock) > 5000
ORDER BY SUM(unit_price * units_in_stock) DESC;

SELECT order_id, customer_id, first_name, last_name, title
FROM orders
INNER JOIN employees ON orders.employee_id = employees.employee_id
```

Задачи:
- Найти заказчиков и обслуживающих их заказы сотрудников таких, что и заказчики и сотрудники из города London, а доставка идёт компанией Speedy Express. Вывести компанию заказчика и ФИО сотрудника.
```SQL
SELECT c.company_name, CONCAT(first_name, ' ', last_name) as full_name
FROM orders AS o
JOIN customers AS c USING(customer_id)
JOIN employees AS e USING(employee_id)
JOIN shippers AS s ON o.ship_via = s.shipper_id
WHERE c.city = 'London' AND e.city = 'London' AND s.company_name = 'Speedy Express';
/*
"company_name"	"concat"
"Around the Horn"	"Michael Suyama"
"Seven Seas Imports"	"Steven Buchanan"
```

- Найти активные (см. поле discontinued) продукты из категории Beverages и Seafood, которых в продаже менее 20 единиц. Вывести наименование продуктов, кол-во единиц в продаже, имя контакта поставщика и его телефонный номер.
```SQL
SELECT product_name, category_name, units_in_stock, contact_name, phone
FROM products
JOIN categories as c USING(category_id)
JOIN suppliers as s USING(supplier_id)
WHERE category_name IN ('Beverages', 'Seafood') AND discontinued = 0 AND units_in_stock < 20
ORDER BY units_in_stock;
/*
"product_name"	"category_name"	"units_in_stock"	"contact_name"	"phone"
"Rogede sild"	"Seafood"	5	"Niels Petersen"	"43844108"
"Nord-Ost Matjeshering"	"Seafood"	10	"Sven Petersen"	"(04721) 8713"
"Gravad lax"	"Seafood"	11	"Michael Björn"	"08-123 45 67"
"Outback Lager"	"Beverages"	15	"Ian Devling"	"(03) 444-2343"
"Côte de Blaye"	"Beverages"	17	"Guylène Nodier"	"(1) 03.83.00.68"
"Ipoh Coffee"	"Beverages"	17	"Chandra Leka"	"555-8787"
```
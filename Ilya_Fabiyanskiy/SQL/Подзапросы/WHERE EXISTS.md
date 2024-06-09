
WHERE EXISTS с подзапросом внутри - возвращает `True`, если в подзапросе была возвращена 1 строка и более

Задача
Как выбрать компании и имена заказчиков, которые делали заказы весом от 50 до 100?
С помощью подзапроса:
```SQL
SELECT company_name, contact_name
FROM customers
WHERE EXISTS (SELECT customer_id FROM orders
	WHERE customer_id = customers.customer_id
	AND freight BETWEEN 50 AND 100)
/*
"company_name"	"contact_name"
"Alfreds Futterkiste"	"Maria Anders"
"Antonio Moreno Taquería"	"Antonio Moreno"
"Around the Horn"	"Thomas Hardy"
"Berglunds snabbköp"	"Christina Berglund"
"Blauer See Delikatessen"	"Hanna Moos"
"Blondesddsl père et fils"	"Frédérique Citeaux"
"Bólido Comidas preparadas"	"Martín Sommer"
"Bon app'"	"Laurence Lebihan"
```

Как выбрать продукты, которые не покупались между 1 февраля 1995 года и 15 февраля 1995 года?
```SQL
SELECT product_name
FROM products
WHERE NOT EXISTS (SELECT orders.order_id FROM orders
	JOIN order_details USING(order_id)
	WHERE order_details.product_id = product_id
	AND order_date BETWEEN '1995-02-01' AND '1995-02-15')
LIMIT 10
/*
"product_name"
"Chai"
"Chang"
"Aniseed Syrup"
"Chef Anton's Cajun Seasoning"
"Chef Anton's Gumbo Mix"
"Grandma's Boysenberry Spread"
"Uncle Bob's Organic Dried Pears"
"Northwoods Cranberry Sauce"
"Mishi Kobe Niku"
"Ikura"
```



```SQL
SELECT contact_name, company_name, phone, first_name, last_name, title, order_date, product_name, ship_country, products.unit_price, quantity, discount
FROM orders
INNER JOIN order_details ON orders.order_id = order_details.order_id
INNER JOIN products ON order_details.product_id = products.product_id
INNER JOIN customers ON orders.customer_id = customers.customer_id
INNER JOIN employees ON orders.employee_id = employees.employee_id
WHERE ship_country = 'USA'
```

Синтаксический сахар:
```SQL
SELECT contact_name, company_name, phone, first_name, last_name, title, order_date, product_name, ship_country, products.unit_price, quantity, discount
FROM orders
JOIN order_details USING(order_id) -- ON orders.order_id = order_details.order_id
JOIN products USING(product_id) -- ON order_details.product_id = products.product_id
JOIN customers USING(customer_id) -- ON orders.customer_id = customers.customer_id
JOIN employees USING(employee_id) -- ON orders.employee_id = employees.employee_id
WHERE ship_country = 'USA'
```

`NATURAL JOIN` - соединение происходит по всем столбцам, которые проименованы одинаково
Этот код не ЭКСПЛИЦИТЕН (не явен)
```SQL
SELECT order_id, customer_id, first_name, last_name, title
FROM orders
NATURAL JOIN employees
```
Задача:
Определить компании, на которых не висят никакие заказы
```SQL
SELECT company_name, order_id
FROM customers
LEFT JOIN orders ON orders.customer_id = customers.customer_id
WHERE order_id IS NULL
	"Paris spécialités"	
	"FISSA Fabrica Inter. Salchichas S.A."	
```

Есть ли работники, которые не обрабатывают никакие заказы
```SQL
SELECT COUNT(*)
FROM employees
LEFT JOIN orders ON orders.employee_id = employees.employee_id
WHERE order_id IS NULL
-- 0, таких работников нет
```

Задача
Найти заказчиков, не сделавших ни одного заказа. Вывести имя заказчика и order_id
```SQL
SELECT contact_name, order_id
FROM customers
LEFT JOIN orders USING(customer_id)
WHERE order_id is NULL;
/*
"contact_name"	"order_id"
"Marie Bertrand"	
"Diego Roel"	
```
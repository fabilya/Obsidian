Объединение, пересечение, исключение - операции над множествами
___
Задача:
Вывести все страны, из которых наши заказчики и работники

`UNION` - объединение
```SQL
SELECT country
FROM customers
UNION -- объединяет результаты двух SELECT и устраняет дубликаты (с дубликатами UNION ALL)
SELECT country
FROM employees
	"Italy"
	"Venezuela"
	"Sweden"
	"USA"
	"Ireland"
	"Germany"
	"Canada"
	"Finland"
	"Portugal"
	"Argentina"
	"France"
	"Denmark"
	"Switzerland"
	"Norway"
	"Brazil"
	"Austria"
	"UK"
	"Spain"
	"Belgium"
	"Mexico"
	"Poland"
```
___
Задача:
Выбрать страны заказчиков, из которых же происходят страны доставщиков

`INTERSECT` - пересечение
```SQL
SELECT country
FROM customers
INTERSECT
SELECT country
FROM suppliers
	"Spain"
	"Italy"
	"Norway"
	"Sweden"
	"USA"
	"France"
	"Brazil"
	"UK"
	"Germany"
	"Denmark"
	"Canada"
	"Finland"
```
___
Задача:
Найти те страны, в которых проживают customers, но в которых не проживают suppliers

`EXCEPT` - исключение, разница
```SQL
SELECT country
FROM customers
EXCEPT
SELECT country
FROM suppliers
	"Argentina"
	"Switzerland"
	"Venezuela"
	"Belgium"
	"Mexico"
	"Austria"
	"Poland"
	"Ireland"
	"Portugal"
```

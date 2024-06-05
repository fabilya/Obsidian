В SQL есть возможность сгруппировать записи, у которых совпадает значение определённого поля; после группировки можно проводить над полученными группами необходимые операции.
![[Pasted image 20240530180835.png]]

`COUNT` сколько в таблице фильмов каждого типа
```SQL
-- Показать значение поля product_type и значение счётчика...
SELECT product_type,
       COUNT(*)
FROM video_products
-- ...для групп записей с одинаковым значением в поле product_type
GROUP BY product_type; 

/*
('Мультсериал', 2)
('Мультфильм', 1)
('Сериал', 3)    
('Фильм', 4) 
*/
```

`MIN` в каждой группе
```SQL
SELECT product_type,
       MIN(release_year)
FROM video_products
GROUP BY product_type; 

/*
('Мультсериал', 1930)
('Мультфильм', 1969)
('Сериал', 1984)
('Фильм', 1967) 
*/
```
>«в таблице **video_products** объедини в группы записи с одинаковым полем `product_type`; покажи значение `product_type` и минимальное значение `release_year` для каждой из групп».

`SUM` для фильмов разного типа
```SQL
SELECT product_type,
       SUM(gross)
FROM video_products
GROUP BY product_type; 

/*
('Мультсериал', None)
('Мультфильм', None)
('Сериал', None)
('Фильм', 318868922) 
*/
```

### HAVING фильтрация групп
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

```SQL
SELECT ship_country, COUNT(*)
FROM orders
WHERE freight > 50
GROUP BY ship_country
ORDER BY COUNT(*) DESC;
	"ship_country"	"count"
	"USA"	    61
	"Germany"	58
	"Austria"	33
	"Brazil"	32
	"France"	27
	"Venezuela"	20
	"Sweden"	20
	"UK"	    17
	"Canada"	13
	"Ireland"	12
	"Mexico"	9
	"Switzerland" 9
	"Denmark"	9
	"Belgium"	8
	"Spain"	    7
	"Finland"	6
	"Italy"	    6
	"Portugal"	6
	"Norway"	3
	"Argentina"	3
	"Poland"	1



SELECT category_id, SUM(units_in_stock)
FROM products
GROUP BY category_id
ORDER BY SUM(units_in_stock) DESC
	"category_id"	"sum"
	8	701
	1	559
	2	507
	4	393
	3	386
	5	308
	6	165
	7	100
```
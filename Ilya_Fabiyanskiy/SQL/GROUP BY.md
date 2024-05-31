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

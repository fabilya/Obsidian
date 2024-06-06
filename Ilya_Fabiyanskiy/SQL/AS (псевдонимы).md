С помощью `AS` мы можем назначить имя колонки
Псевдонимами не получится пользоваться в `FROM`, `WHERE`, т.к. когда отрабатывает `WHERE` псевдоним ещё не назначен. 
`SELECT` работает после `FROM` и `WHERE`

Обычный запрос:
```SQL
SELECT COUNT(*)
FROM employee
/*
"count"
8
```

с использованием `AS`:
```SQL
SELECT COUNT(*) as employees_count
FROM employee
/* 
"employees_count"
8
```

```SQL
SELECT COUNT(DISTINCT country) AS country
FROM employees
/*
"country"
2
```

```SQL
SELECT category_id, SUM(units_in_stock) AS dsa
FROM products
GROUP BY category_id
ORDER BY dsa DESC
LIMIT 5
/*
"category_id"	"dsa"
8	701
1	559
2	507
4	393
3	386
```

в `HAVING` не можем использовать alias, иначе - ошибка
```SQL
SELECT category_id, SUM(unit_price * units_in_stock) AS total_price
FROM products
WHERE discontinued <> 1
GROUP BY category_id
HAVING SUM(unit_price * units_in_stock) > 5000
ORDER BY total_price DESC
/*
"category_id"	"total_price"
8	13010.349914550781
2	11926.04999923706
1	11365.25
4	11271.199989318848
3	10392.200072288513
5	5230.5
```
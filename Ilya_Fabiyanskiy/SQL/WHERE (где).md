```SQL
SELECT title,
       release_year
FROM video_products
# ГДЕ значение поля release_year больше 1980
WHERE release_year > 1980;
```

![[Pasted image 20240530145945.png|600]]

##### Для описания условий запроса применяют специальные операторы:

* `=`  оператор **сравнения**, а не присваивания (это аналог `==` в Python)

* `BETWEEN ... AND ...` - для проверки значения между диапазонами, начало и конец включены в условие
```SQL
  SELECT title
  FROM video_products
 # Найдём фильмы, выпущенные с 1980 по 1990 год включительно:
  WHERE release_year BETWEEN 1980 AND 1990;
```

* `IN` - вхождение в список
```SQL
  SELECT title
  FROM video_products
# Найдём в базе все фильмы, 
# у которых значение поля product_type - 'Сериал' или 'Фильм':
  WHERE product_type IN ('Сериал', 'Фильм');
```

* `LIKE`- поиск строки по шаблону
```SQL
  SELECT title
  FROM video_products
  WHERE product_type LIKE 'Мульт%';
```

Для объединения сразу нескольких условий используются операторы `AND`, `OR` или `NOT`:
```Python
results = cur.execute('''
SELECT title,
       release_year
FROM video_products
WHERE (release_year BETWEEN 1965 AND 1990) AND product_type LIKE '%ильм';
''')

for result in results:
    print(result)

# ('Кто подставил кролика Роджера', 1988)
# ('Хороший, плохой, злой', 1967)
# ('Розовая пантера: Контроль за вредителями', 1969)
```

**Приоритет логических операторов:**
1. `NOT` 
2. `AND`
3. `OR`

**Значение** `NULL`:
`NULL` означает отсутствие данных. 
Для работы с `NULL` используют отдельные операторы — `IS NULL` и `IS NOT NULL`. 
Основная особенность `NULL` в том, что это значение не равно ничему; любая попытка сравнить `NULL` с чем угодно, даже с `NULL`, вернёт `False`

Для значения `NULL` оператор `IS NULL` вернёт `True`
Оператор `IS NOT NULL` вернёт `True` - если значение не равно `NULL`.

#### Порядок элементов в запросе

В SQL-запросах важно указывать элементы запроса в правильном порядке
```SQL
SELECT <перечень столбцов через запятую>
FROM <название таблицы>
WHERE <условия>;
```

В SQLite есть служебная таблица `sqlite_master`, в колонке `tbl_name` она хранит названия всех таблиц базы.

```SQL
cur.execute('''
    SELECT tbl_name
    FROM sqlite_master
    WHERE type='table';
''')

table = cur.fetchall()[0][0]  # Получение имени таблицы через атрибут курсора.
```
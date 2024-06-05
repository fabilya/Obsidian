* `DISTINCT` - уникальные значения из заданного столбца
```SQL
# ВЫБРАТЬ УНИКАЛЬНЫЕ ЗНАЧЕНИЯ из колонки product_type:
SELECT DISTINCT product_type
FROM video_products;

# ('Мультсериал',)
# ('Фильм',)
# ('Сериал',)
# ('Мультфильм',)
```
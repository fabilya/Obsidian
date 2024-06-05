`BETWEEN` - всегда включает границы в результирующей выборке
```SQL
SELECT *
FROM orders
WHERE freight >= 20 and freight <= 40;

-- тоже самое, что выше, с использованием BETWEEN включая границы
SELECT COUNT(*)
FROM orders
WHERE freight BETWEEN 20 and 40;
```
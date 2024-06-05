`LIKE` - используется для поиска строк, похожие на заданный шаблон

Шаблоны
`%` - placeholder (заполнитель) означающий 0, 1 и более символов
`_` - ровно 1 любой символ

- `LIKE 'U%'` - строки, начинающиеся с **U**
- `LIKE '%a'` - строки, кончающиеся на **а**
- `LIKE '%John%'` - строки, содержащие **John**
- `LIKE 'J%n'` - строки, начинающиеся на **J** и кончающиеся на **n**
- `LIKE '_oh_'` - строки, где 2, 3 символы - **oh**, а первый (1) и последний (4) - **любые**
- `LIKE '_oh%'`- строки, где 2, 3 символы - **oh**, а первый - **любой** и в конце **0, 1 и более любых символов**

```SQL
SELECT last_name, first_name
FROM employees
WHERE first_name LIKE '%n';

SELECT last_name, first_name
FROM employees
WHERE last_name LIKE 'B%';

SELECT last_name, first_name
FROM employees
WHERE last_name LIKE 'Buch%';

SELECT last_name, first_name
FROM employees
WHERE last_name LIKE '__ch%';
```

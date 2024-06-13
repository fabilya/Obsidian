* `CREATE TABLE` table_name - создание таблицы
* `ALTER TABLE` *table_name* - изменить таблицу
	* `ADD COLUMN` *column_name* **data_type** - добавить столбец
	* `RENAME TO` *new_table_name* - переименовать таблицу
	* `RENAME` *old_column_name* `TO` *new_column_name* - переименовать столбец
	* `ALTER COLUMN` *column_name* `SET DATA TYPE` **data_type** - изменить тип данных
- `DROP TABLE` *table_name* - удалить таблицу
- `TRUNCATE TABLE` *table_name* - удалить все данные в таблице, не может удалить данные, на которые есть ссылки из других таблиц
- `DROP COLUMN` *column_name* - удалить столбец

 Примеры использования:
 ```SQL
 CREATE TABLE student -- создание таблицы student
(
	student_id serial,
	first_name varchar,
	last_name varchar,
	birthday date,
	phone varchar
);

CREATE TABLE cathedra
(
	cathedra_id serial,
	cathedra_name varchar,
	dekan varchar
);

ALTER TABLE student 
ADD COLUMN middle_name varchar;  -- добавление столбца в таблицу student

ALTER TABLE student
ADD COLUMN rating float; 

ALTER TABLE student
ADD COLUMN enrolled date;  

ALTER TABLE student
DROP COLUMN middle_name;  -- удаление столбца

ALTER TABLE cathedra -- изменение имени таблицы
RENAME TO chair  

ALTER TABLE chair -- изменение имени столбца
RENAME cathedra_id TO chair_id;

ALTER TABLE chair
RENAME cathedra_name TO chair_name;

ALTER TABLE student  -- изменение типов данных у столбцов
ALTER COLUMN first_name SET DATA TYPE varchar(64);
ALTER TABLE student
ALTER COLUMN last_name SET DATA TYPE varchar(64);
ALTER TABLE student
ALTER COLUMN phone SET DATA TYPE varchar(30);

CREATE TABLE faculty  -- добавление данных в таблицу
(
	faculty_id serial,
	faculty_name varchar
);
INSERT INTO faculty (faculty_name)
VALUES
('faculty 1'),
('faculty 2'),
('faculty 3');

SELECT * FROM faculty
/*
"faculty_id"	"faculty_name"
1	"faculty 1"
2	"faculty 2"
3	"faculty 3"
*/

TRUNCATE TABLE faculty -- удаление данных из таблицы, по умолчанию: без рестарта автоинкремента

INSERT INTO faculty (faculty_name)
VALUES
('faculty 1'),
('faculty 2'),
('faculty 3');

SELECT * FROM faculty  -- ID начались с 4,5,6
/*
"faculty_id"	"faculty_name"
4	"faculty 1"
5	"faculty 2"
6	"faculty 3"
*/

TRUNCATE TABLE faculty RESTART IDENTITY  -- c рестартом автоинкремента

INSERT INTO faculty (faculty_name)
VALUES
('faculty 1'),
('faculty 2'),
('faculty 3');

SELECT * FROM faculty

/*
"faculty_id"	"faculty_name"
1	"faculty 1"
2	"faculty 2"
3	"faculty 3"
*/

DROP TABLE faculty  -- удаление таблицы


```
* `CREATE TABLE` table_name - создание таблицы
* `ALTER TABLE` *table_name* - изменить таблицу
	* `ADD COLUMN` *column_name* **data_type** - добавить колонку
	* `RENAME TO` *new_table_name* - переименовать таблицу
	* `RENAME` *old_column_name* `TO` *new_column_name* - переименовать столбец
	* `ALTER COLUMN` *column_name* `SET DATA TYPE` **data_type** - изменить тип данных
- `DROP TABLE` *table_name* - удалить таблицу
- `TRUNCATE TABLE` *table_name* - удалить все данные в таблице
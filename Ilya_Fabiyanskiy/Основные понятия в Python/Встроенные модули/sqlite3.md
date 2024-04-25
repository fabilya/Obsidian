[[Встроенные модули]]

Программа с помощью которой можно смотреть содержимое БД и взаимодействовать с ней - [DB Browser for SQLite](http:/sqlitebrowser.org/)

**Создание БД**
```Python
import sqlite3  
  
# БД в виде файла  
DB_NAME = "sqlite_db.db"  
  
# Создание БД и проверка подключения  
with sqlite3.connect(DB_NAME) as sqlite_conn:  
    # создался объект <sqlite3.Connection object at 0x000001AEC952DE40>  
    print(sqlite_conn)  
    # Версия 2.6.0  
    print(sqlite3.version)
```

**Создание таблицы в БД**
```Python
import sqlite3  
  
DB_NAME = "sqlite_db.db"  
  
# Создание таблицы в БД  
with sqlite3.connect(DB_NAME) as sqlite_conn:  
    # SQL запрос  
    sql_request = """CREATE TABLE IF NOT EXISTS courses (  
        id integer PRIMARY KEY,        title text NOT NULL,        students_qty integer,        reviews_qty integer        );"""  
    sqlite_conn.execute(sql_request)
```

Запись данных в таблицу SQLite
```Python
import sqlite3  
  
DB_NAME = "sqlite_db.db"  
  
courses = [  
    (351, "JavaScript course", 415, 100),  
    (614, "C++ course", 161, 10),  
    (721, "Java full course", 100, 35)  
]  
  
with sqlite3.connect(DB_NAME) as sqlite_conn:  
    # SQL запрос (вставить в таблицу courses - значения)  
    sql_request = "INSERT INTO courses VALUES(?, ?, ?, ?)"  
    # заполняем значениями в sql запросе  
    for course in courses:  
        sqlite_conn.execute(sql_request, course)  
    # сохраняем изменения в БД  
    sqlite_conn.commit()
```

**Чтение данных из таблицы SQLite**
```Python
import sqlite3  
  
DB_NAME = "sqlite_db.db"  
  
with sqlite3.connect(DB_NAME) as sqlite_conn:  
    # чтение всех записей из таблицы courses где reviews_qty>=30  
    sql_request = "SELECT * FROM courses WHERE reviews_qty>=30"  
    sql_cursor = sqlite_conn.execute(sql_request)  
    # вывод всех записей из таблицы courses  
    # for record in sql_cursor:    
    #     print(record)    
    records = sql_cursor.fetchall()  
    print(records)
```

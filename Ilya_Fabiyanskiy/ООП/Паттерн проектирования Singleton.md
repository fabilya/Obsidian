___
Паттерн проектирования Singleton (Одиночка) гарантирует, что у класса есть только один экземпляр, и предоставляет глобальную точку доступа к этому экземпляру. Это может быть полезно в ситуациях, когда нужен только один объект для координации действий по всему приложению, например, для работы с базой данных, логирования или управления конфигурацией.

```Python
class DataBase:
	__instance = None # ссылка на экземпляр класса, проверяет существует ли объект.

	def __new__(cls, *args, **kwargs):
		if cls.__instance is None:
			cls.__instance = super().__new__(cls)

		return cls.__instance # вернет адрес ранее созданного объекта

	def __del__(self):
		Database.__instance = None

	def __init__(self, user, psw, port):
		self.user = user
		self.psw = psw
		self.port = port

	def connect(self):
		print(f"Соединение с БД: {self.user}, {self.psw}, {self.port}")

	def close(self):
		print("закрытие соединения с БД")

	def read(self):
		print("Данные из БД")

	def write(self, data):
		print(f"Запись в БД: {data}")

db = DataBase('root', '1234', 80)
db2 = DataBase('root2', '5678', 40)
print(id(db), id(db2))

# 1512591956864 1512591956864
db.connect()
db2.connect()
# Соединение с БД: root2, 5678, 40
# Соединение с БД: root2, 5678, 40
```
>метод `__init__` переопределил локальные свойства в объекте, для этого нужно переопределить магический метод `__call__`
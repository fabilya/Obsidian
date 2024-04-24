**JSON (JavaScript Object Notation)** - формат обмена и хранения данных и формат файлов
В JSON используются только двойные кавычки

Пример:
```Json
{
	"id": 235,
	"brand": "Nike",
	"qty": 94,
	"status": {   
		"isForSale": true
	}
}
```

Допустимые типы значений в JSON:
`string`, `number`, `JSON object`, `boolean`, `array`, `null`

Передача данных в формате JSON в виде строки
```Json
{"id": 235,	"brand": "Nike", "qty": 94,	"status": {"isForSale": true}}
```

Конвертация JSON в словарь с помощью встроенного модуля json и его методом `json.loads()`
```Python
import json

json_str = '{"id": 235,	"brand": "Nike", "qty": 94,	"status": {"isForSale": true}}'

sneakers = json.loads(json_str)

print(type(sneakers))  # class <'dict'>

print(sneakers['brand'])  # Nike
print(sneakers['qty'])  # 84
print(sneakers['status']['isForSale'])  # True
```

Конвертация словаря в JSON (`json.dumps()`)

>Это может понадобиться, когда необходимо отправить данные с вашей программы на удаленный сервер, сохранить данные в БД

Форматирование результирующего JSON
```Python
result = json.dumps(sneakers, indent=1)
print(result)

#{
# "id": 235,
# "brand": "Nike",
# "qty": 94,
# "status": {
#  "isForSale": true
# }
#}
```

Конвертация типов Python в типы JSON:

| Python  | JSON   |
| ------- | ------ |
| `str`   | String |
| `int`   | Number |
| `float` | Number |
| `True`  | true   |
| `False` | false  |
| `None`  | null   |
| `dict`  | Object |
| `list`  | Array  |
| `tuple` | Array  |




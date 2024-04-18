Кортеж - это упорядоченная последовательность элементов, похожи на списки, но их изменять нельзя, т.е. нельзя добавлять или удалять элементы
Объект типа tuple неизменяемый

**Структура и синтаксис**
```
my_fruits = ('apple', 'banana', 'lime')
user_inputs = (True, 'hi!', 10.5, '😁')  # В кортеже могут быть объекты разных типов
```

**Порядок в кортеже важен**
```
my_fruits = ('apple', 'banana', 'lime')
other_fruits = ('banana', 'lime', 'apple')
print(my_fruits == other_fruits)
# False
```

Длина, получение значений как в списках.

**Изменять элементы НЕЛЬЗЯ!**
```
posts_ids = (151, 256, 222, 567)
posts_ids[0] = 555
# TypeError: 'tuple' object does not support item assignment
```

**Изменяемые объекты в кортежах изменять МОЖНО** (словари, списки или др. изменяемые объекты)
```
users = (
	{
		'user_id': 123,
		'user_name': 'Alice'
	},
	{
		'user_id': 321,
		'user_name': 'Bob'
	}
)
print(users[1]['user_id'])
# 321
users[1]['user_id'] = 100
print(users[1]['user_id'])
# 100
```

Кортежи можно конвертировать в список, и обратно
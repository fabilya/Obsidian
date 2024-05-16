Кортеж - это упорядоченная неизменяемая последовательность элементов, похожи на списки, но их изменять нельзя, т.е. нельзя добавлять или удалять элементы
Объект типа tuple неизменяемый

[[Распаковка (unpucking)]]

**Структура и синтаксис**
```Python
my_fruits = ('apple', 'banana', 'lime')
user_inputs = (True, 'hi!', 10.5, '😁')  # В кортеже могут быть объекты разных типов
```

**Порядок в кортеже важен**
```Python
my_fruits = ('apple', 'banana', 'lime')
other_fruits = ('banana', 'lime', 'apple')
print(my_fruits == other_fruits)
# False
```

**Длина, получение значений как в списках**
```Python
my_fruits = ('apple', 'banana', 'lime')
print(len(my_fruits))  # 3
```

**Получение значений, как и в списках начинается с 0**
```Python
posts_ids = (151, 45, 762, 178)
print(posts_ids[0])  # 151
print(posts_ids[1])  # 45
```

**ИЗМЕНЯТЬ ЭЛЕМЕНТЫ  НЕЛЬЗЯ!**
```Python
posts_ids = (151, 256, 222, 567)
posts_ids[0] = 555
# TypeError: 'tuple' object does not support item assignment
```

**ИЗМЕНЯЕМЫЕ объекты в кортежах изменять МОЖНО** (словари, списки или др. изменяемые объекты)
```Python
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

[[Циклы#Генераторы в comrehension Tuple (кортежи) (такого понятия как touple comprehension - нет) `for in`|for in]] в кортежах (Генераторы)

Кортежи можно конвертировать в список, и обратно
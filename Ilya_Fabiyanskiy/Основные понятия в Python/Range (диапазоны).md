***Диапазон*** - это упорядоченная неизменяемая последовательность элементов.
Диапазоны обычно используются в циклах

Структура и синтаксис
```Python
my_range = range(7)
print(type(my_range))
# class <'range'>       # Каждый диапазон - это экземпляр класса range
print(my_range)
# range(0, 7)
print(list(my_range))
# [0, 1, 2, 3, 4, 5, 6]
```

Добавление шага в диапазонах
```Python
my_range = range(10, 20, 3)   # третий аргумент в вызове функции - шаг для диапазона
print(list(my_range)
# [10, 13, 16, 19]
```

Индексы элементов в диапазонах
```Python
my_range = range(10, 20, 3)
print(my_range[0])
# 10
print(my_range[1])
# 13
print(my_range[2])
# 16
print(my_range[3])
# 19
print(my_range[4])
# IndexError: range object index out of range
```

Использование диапазонов в циклах
```Python
my_range = range(10, 20, 3)
for n in my_range:             # Итерация по диапазону
	print(n)
	# 10
	# 13
	# 16
	# 19
```

Методы диапазонов
* `index` - передается элемент, мы получаем индекс этого элемента в диапазоне
```Python
my_range = range(10, 30, 3)
print(my_range.index(19))
# 3
print(my_range.index(20))
# ValueError: 20 is not in range
```
* `count` - работает как в списках, но в диапазонах есть только уникальные элементы, в диапазоне элемент либо может быть, либо нет, поэтому count возвращает либо "0", либо "1"
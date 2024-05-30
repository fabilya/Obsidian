[[Встроенные функции Python (Built-in Functions)]]
`filter(функция, последовательность)` - возвращает тип `filter object`, выполняет итерацию по определенной последовательности.
*  `функция` - которая будет выполнять действия с каждым элементом `последовательности`

**Задание:**
>Написать функцию, которая будет фильтровать список с учетом второго параметра (`int`, `bool`, `str` и т.д.) 

Классическое решение с помощью строенной функции `filter()`
```Python
def filter_list(list_to_filter, value_type):
	 def check_element_type(elem):
		 return type(elem) is value_type
	return list(filter(check_element_type, list_to_filter))

print(filter_list([1, 10, 'abc', True, 5.5], int))
# [1, 10]
```

С помощью лямбда функции (`lambda function`)
```Python
def filter_list(list_to_filter, value_type):
	return list(filter(lambda elem: type(elem) is value_type, list_to_filter))

print(filter_list([1, 10, 'abc', True, 5.5], int))
# [1, 10]
```
`
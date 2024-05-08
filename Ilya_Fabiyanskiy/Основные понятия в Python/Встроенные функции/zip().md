`zip()` - встроенная функция, с помощью которой, можно формировать новые объекты на основании других последовательностей, т.е. объединять последовательности вместе

Пример
```Python
fruits = ['apple', 'banana', 'lime']
quantities = [100, 70, 50]
# необходимо создать новую последовательность, в которой будут пары apple - 100, banana - 70, lime - 50.

fruit_qtys_zip = zip(fruits, quantities)
print(fruit_qtys_zip)
# <zip object at 0x7fbca80a74c0>   # объект zip

# объект zip можно легко конвертировать в список
fruit_qtys_list = list(fruit_qtys_zip)
print(fruit_qtys_list)
# [('apple', 100), ('banana', 70), ('lime', 50)] # список кортежей
```
> При конвертации `zip` объекта в `список` получается список кортежей

Конвертация в `dict`
```Python
fruits = ['apple', 'banana', 'lime']
quantities = [100, 70, 50]
fruit_qtys_zip = zip(fruits, quantities)
fruit_qtys_dict = dict(fruit_qtys_zip)
print(fruit_qtys_dict)
# {'apple': 100, 'banana': 70, 'lime': 50}
```
> При конвертации `zip` объекта в `словарь` допускается только 2 аргумента в вызове функции `zip`


`zip` объект формируется на основании самого короткого из списков, которые вы передаете в функцию `zip`




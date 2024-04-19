Поведение ***неизменяемых*** объектов
```
first_num = 10
second_num = first_num

print(id(first_num))   # 14037000977120
print(id(second_num))  # 14037000977120

second_num += 5    # здесь нет изменение объекта, здесь создание нового объекта
print(second_num)  # 15
print(first_num)   # 10

print(id(second_num))  # 72310033353213
print(id(first_num))   # 14037000977120
```
> Для неизменяемых объектов в случае выполнения операции сложения, создается новый объект, мы не меняем существующий.
> Так Python себя ведет касательно всех неизменяемых объектов

Поведение ***изменяемых*** объектов
```
my_list = [1, 2, 3]
print(id(my_list))
# 140294704433984

other_list = [1, 2, 3]
print(id(other_list))
# 140294705022106

print(id([1, 2, 3]))
# 140294704303168
```

> Если переменные ссылаются на один и тот же изменяемый объект, изменения отражаются на ***всех*** "копиях" 

Как избежать изменений копий?

Вариант №1
```
info = {
	'name': 'Ilya',
	'is_instructor': True
}

info_copy = info.copy()    
info_copy['reviews_qty] = 5
print(info_copy)
# {'name': 'Ilya', 'is_instructor': True, 'reviews_qty': 5}
print(info)
# {'name': 'Ilya', 'is_instructor': True}
```
> Если у словаря есть вложенные словари, либо вложенные списки, или другие изменяемые объекты, то ссылки на них сохраняются

Вариант №2
```
info = {
	'name': 'Ilya',
	'is_instructor': True,
	'reviews': []          <- # если у словаря есть вложенные словари, списки, или 
	                          # другие изменяемые объекты, то ссылки на 
							  # них сохраняются
}

info_copy = info.copy()    
info_copy['reviews'].append('Good job')
print(info)
# {'name': 'Ilya', 'is_instructor': True, 'reviews': 'Good job'}
print(info_copy)
# {'name': 'Ilya', 'is_instructor': True, 'reviews': 'Good job'}
```
> ==Метод `copy()` дает нам копию только первого уровня (поверхностную (по англ. shallow) копию), а другие уровни, вложенные уровни, например словарь, список - остаются без изменений==

В Python есть решение и этой проблемы, встроенным в Python модулем ***copy*** и из этого модуля можно импортировать функцию ***deepcopy***
```
from copy import deepcopy
info = {
	'name': 'Ilya',
	'is_instructor': True,
	'reviews': []
}

info_copy = deepcopy(info)    # Если у словаря есть вложенные словари, то ссылки на 
                              # них не сохраняются
info_copy['reviews'].append('Good job')
print(info)
# {'name': 'Ilya', 'is_instructor': True, 'reviews': []}
print(info_copy)
# {'name': 'Ilya', 'is_instructor': True, 'reviews': ['Good job']}
```

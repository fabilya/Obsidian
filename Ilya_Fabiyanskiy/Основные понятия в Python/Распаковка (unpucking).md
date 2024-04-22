Содержание:
- [[#^8957f8 |Определение]]
- [[#Распаковка списков и кортежей]]
- [[#Распаковка словаря в именованные аргументы]] ^2083b8
- [[#Распаковка списка в позиционные аргументы]]

**Распаковка** - это извлечение значений и присвоение их переменным ^8957f8
##### Распаковка списков и кортежей
```
my_fruits = ['apple', 'banana', 'lime']
my_apple, my_banana, my_line = my_fruits  
print(my_apple)  # apple
print(my_banana) # banana
print(my_lime)   # lime
```
>Нельзя использовать больше элементов чем в списке

**Использование `*` при распаковке**
```
my_fruits = ['apple', 'banana', 'lime']
my_apple, *remaining_fruits = my_fruits

print(my_apple)            # apple
print(remaining_fruits)    # ['banana', 'lime']
```

##### Распаковка словаря в именованные аргументы
```
user_profile = {
	'name': 'Ilya',
	'comments_qty': 23,
}

def user_info(name, comments_qty=0):
	if not comments_qty:
		return f"{name} has no comments"
	return f"{name} has {comments_qty} comments"

print(user_info(**user_profile))) # Распаковка значений словаря
# Ilya has 23 comments
```

^5cb962

##### Распаковка списка в позиционные аргументы
```
user_data = ['Ilya', 23]

def user_info(name, comments_qty=0):
	if not comments_qty:
		return f"{name} has no comments"
	return f"{name} has {comments_qty} comments"

print(user_info(*user_data))  # Распаковка списка в позиционные аргументы	
```
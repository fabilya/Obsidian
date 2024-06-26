[[Колбэк функции (callback functions)]]
[[Область видимости]]
[[Рекурсивные функции]]

**Функция** - это блок кода, который можно выполнять ***многократно***

***Правила работы с функциями***
1. Называть функции исходя из выполняемых задач
2. Название функции начинать с **глагола**
3. **Одна** функция должна выполнять **одну** задачу
4. Не рекомендуется изменять **внешние** относительно функции **переменные**.


Функция - это объект
```Python
def sum(a, b):
	c = a + b
	print(c)
print(type(sum))
# <class 'function'>
```
> Каждая функция это экземпляр класса `function`

***Структура и синтаксис***
![[Pasted image 20240418160911.png|400]]
***[[Параметры функции]]*** - это переменные, которые доступны внутри функции (параметры функции принадлежат зоне видимости функции, их можно воспринимать, как переменные, доступные внутри функции, но значения этим переменным можно задать при вызове функции, с помощью аргументов)

Функция возвращает `None` если нет ключевого слова `return`
Функцию нужно ***вызывать*** для выполнения кода внутри функции

![[Pasted image 20240418162524.png|400]]
**[[Аргументы функций]]** - изменяются при каждом вызове функции
Передача ***изменяемых*** объектов
```Python
def increase_person_age(person):  
    person['age'] += 1  
    return person                 # Функция изменяет внешний объект
  
  
person_one = {  
    'name': 'Bob',  
    'age': 21  
}  
  
  
increase_person_age(person_one)  
print(person_one)
# 22
```
> Внутри функции ***не рекомендуется*** изменять внешние объекты

Как избежать изменения внешних объектов в функции?
> Создание ***копии*** объекта методом `copy()`

**Напоминаю**, что метод `copy()` создает только поверхностную (по англ. shallow) копию, но в данном примере нас это вполне устраивает, т.к. в словаре `person_one` у нас значения это ***неизменяемые объекты***. (нет вложенных словарей/списков)
```Python
def increase_person_age(person):
	person_copy = person.copy()  # Копирование объекта
    person_copy['age'] += 1  
    return person_copy             


person_one = {  
    'name': 'Bob',  
    'age': 21 
}  
  
  
new_person = increase_person_age(person_one)  
print(person_one['age']) # 21
print(new_person['age']) # 22
```




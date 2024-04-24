[[Встроенные модули]]
Позволяет выполнять различные операции с регулярными выражениями

**Нахождение определенного совпадения в строке**
```Python
import re  
  
my_string = "My name is Ilya"  
  
# метод search  
res = re.search('Ilya', my_string)  
  
print(res)  
# <re.Match object; span=(11, 15), match='Ilya'>  
# span=(11, 15) индексы начальной и конечной строки, которую мы искали в строке  
# match то слово, которое мы нашли  
  
  
# класс Match который находится в модуле re  
print(type(res))  
# <class 're.Match'>  
  
# '.' заменяет любой символ  
res = re.search('I..a', my_string)  
print(res)  
# <re.Match object; span=(11, 15), match='Ilya'>  
  
# '$' указывает на конец строки  
res = re.search('I..a$', my_string)  
print(res)  
# <re.Match object; span=(11, 15), match='Ilya'>  
  
# '^' начало строки  
# '.*' всё что угодно  
res = re.search('^M.*name', my_string)  
print(res)  
# <re.Match object; span=(0, 7), match='My name'>  
  
# "\" escape символ в регулярных выражениях  
my_string2 = "My name is Ilya."  
res = re.search('I..a\.$', my_string2)  
print(res)  
  
# '\n' символ перехода на следующую строку  
print('I..a\n.$')  
# I..a  
# .$  
  
# если надо использовать \n в паттернах регулярных выражений  
print(r'I..a\n.$')  
# I..a\n.$
```
>Необходимо использовать `r-строки` 
>В регулярных выражениях чаще всего используют `r-строки`, а не обычные строки, и потому следует всегда перед паттерном добавлять `r`  

**В объекте `res` есть доступ к определенным методам и атрибутам**
`span()` - кортеж из двух элементов, начало-конец результирующей строки, которую мы нашли используя `search`
`start()` и `end()` - начало и конец соответственно

**Сохранение паттерна в отдельном объекте**
```Python
import re  
  
my_string = "My name is Ilya."  
other_string = "My name is Ilya!"  
  
# Создаем паттерн на основании регулярного выражения
my_pattern = re.compile(r'I..a\.$')  
print(my_pattern)  
# re.compile('I..a\\.$')  
  
# для поиска в строке мы передаем паттерн  
print(my_pattern.search(my_string))  
# <re.Match object; span=(11, 16), match='Ilya.'>  
  
# поиск совпадений  
my_pattern = re.compile(r'^My.*\.$')  
print(my_pattern.match(my_string))  
# <re.Match object; span=(0, 16), match='My name is Ilya.'>  
  
# строка не соответствует регулярному выражению  
print(my_pattern.match(other_string))  
# None  
  
# findall позволяет найти все части строки, которые соответствуют паттерну  
other_string2 = "My name is Ilya! Ilya is student"  
my_pattern = re.compile(r'I..a')  
print(my_pattern.findall(other_string2))
# ['Iaaa', 'Ilya']
```

**Проверка корректности написания email или пароля**

 `fullmatch()` полезен, когда вы хотите найти совпадение, которое полностью соответствует всей целевой строке, без учета дополнительных символов до или после совпадения.
```Python
import re  
  
  
def check_email(email):  
    email_regexp = r'^[\w\.-]+@[\w\.-]+\.\w+$'  
    email_check_pattern = re.compile(email_regexp)  
    # если валидация проходит успешно, метод fullmatch возвращает экземпляр  
    # класса match, а это правдивое значение (True), иначе если валидация    # прошла неуспешно, то возвращается None, а это ложное значение.    validation_result = "Valid" if email_check_pattern.fullmatch(email) else "Invalid"  
    return email, validation_result  
  
  
# Valid  
print(check_email('bs@gmail.com'))  
print(check_email('b_s@gmail.com'))  
print(check_email('b.s@gmail.com'))  
print(check_email('b.s@sub.gmail.com'))  
  
# Not valid  
print(check_email('bsgmail.com'))  
print(check_email('bs@gmailcom'))  
print(check_email('@gmail.com'))  
print(check_email('bs@'))

# ('bs@gmail.com', 'Valid')  
# ('b_s@gmail.com', 'Valid')  
# ('b.s@gmail.com', 'Valid')  
# ('b.s@sub.gmail.com', 'Valid')  
# ('bsgmail.com', 'Invalid')  
# ('bs@gmailcom', 'Invalid')  
# ('@gmail.com', 'Invalid')  
# ('bs@', 'Invalid')
```

>[!Задача: проверка пароля]
>1. Создайте функцию для проверки пароля
>2. Пароль должен быть минимум 8 символов
>3. В пароле должны быть:
>	- буквы в нижнем регистре
>	- буквы в верхнем регистре
>	- цифры
>	- специальные символы
>4. Попросите пользователя ввести пароль в терминале и проверьте его

##### Решение
```Python
import re  
  
  
def check_password(password):  
    # '\S' - любые символы кроме tab, space, перехода на новую строку  
    length_pattern = re.compile(r"\S{8,}")  
    # '+' - означает что любая буква от a-z должна присутствовать хотя бы 1 и  
    # более раз    lowercase_pattern = re.compile(r"^.*[a-z]+.*$")  
    uppercase_pattern = re.compile(r"^.*[A-Z]+.*$")  
    number_pattern = re.compile(r"^.*[0-9]+.*$")  
	special_symbol_pattern = re.compile(r"^.*[!@#$%^&*()_+\-=\[\]{};':\"\\|,"  
                                        r".<>\/?]+.*$")
    no_whitespace_pattern = re.compile(r"^\S*$")  
  
    if not re.fullmatch(no_whitespace_pattern, password):  
        return False, "Password must not contain whitespaces"  
  
    if not re.fullmatch(length_pattern, password):  
        return False, "Password must have at least 8 symbols"  
  
    # если есть return, то нет необходимости делать elif  
    if not re.fullmatch(lowercase_pattern, password):  
        return False, "Password must have at least 1 lowercase letter"  
  
    if not re.fullmatch(uppercase_pattern, password):  
        return False, "Password must have at least 1 uppercase letter"  
  
    if not re.fullmatch(number_pattern, password):  
        return False, "Password must have at least 1 digit"  
  
    if not re.fullmatch(special_symbol_pattern, password):  
        return False, "Password must have at least 1 special symbol"  
  
    return True, "Password is valid!"  
  
  
# print(check_password('asdFAS3dsa   !234'))  
# print(check_password('123'))  # (False, 'Password must have at least 8 symbols')  
# print(check_password('12345678'))  # (False, 'Password must have at least 1 lowercase letter')  
# print(check_password('1234567a'))  # (False, 'Password must have at least 1 uppercase letter')  
# print(check_password('asdbASDAF'))  # (False, 'Password must have at least 1 digit')  
# print(check_password('321sdDSAF'))  # (False, 'Password must have at least 1 special symbol')  
# print(check_password('asdFAS321!#@'))  # (True, 'Password is valid!')  
  
while True:  
    password = input('Введите пароль из 8 символов: ')  
    result = check_password(password)  
    if result[0]:  
        print(result[1])  
        break  
    print(result[1])
```

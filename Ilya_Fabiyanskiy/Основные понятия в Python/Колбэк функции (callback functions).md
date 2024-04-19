Это функция которая **передается как аргумент в другую функцию** и там **вызывается**

 Пример №1
```
def other_fn():
	 # some actions...
	 pass


def fn_with_callback(callback_fn):  # В теле этой функции  
                                    # вызывается колбэк функция
	callback_fn()


fn_with_callback(other_fn)
```

Пример №2
```
def print_number_info(num):
	if (num % 2) == 0:
		print("Entered number is even")
	else:
		print("Entered number is odd")


def process_number(num, callback_fn):
	callback_fn(num)  # Функция вызывается внутри другой функции

entered_num = int(input('Enter any number: '))

process_number(entered_num, print_number_info)
```
> Переменная `print_number_info` и `callback_fn` ссылаются на один и тот же объект в памяти - на функцию `def print_number_info()`


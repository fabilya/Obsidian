> _В твоём коде есть несколько полезных функций: возможно, ты сам или кто-то из твоих коллег захочет повторно применить их в другом проекте. Старайся писать код так, чтобы обеспечить эту возможность._
> 
> _Отдели код, который может впоследствии переиспользоваться (функции и классы) от исполняемого кода конструкцией_ `if __name__ == '__main__'`.

Вроде бы ревьюер и похвалил код («...несколько полезных функций») — а доделывать всё равно придётся. Да, в коде есть многое, что может пригодиться в других проектах, а сколько всего ещё будет впереди! К этой рекомендации однозначно стоит прислушаться.

Подсказка в письме есть, но что за конструкция `if __name__ == '__main__'` и что это за переменная `__name__`, откуда она берётся и что делает?

Стас честно попробовал разобраться с этим вопросом по документации, но там `__name__` и `'__main__'` описаны довольно смутно. Пришлось просить консультации у коллег.

После часа разговоров и трёх кружек кофе Стас примерно понял, в чём состоит суть дела.

### Когда `__name__` == `'__main__'`?

Переменная `__name__` — это особая переменная в Python, получающая значение в зависимости от того, каким образом выполняется код программы: импортирован он или нет. Из [официальной документации](https://docs.python.org/3/reference/import.html?highlight=__name__#__name__) следует что эта переменная доступна на уровне всего модуля или программы.

Проще всего поэкспериментировать на коде. Создайте в директории проекта файл с именем _name_demo.py_ и добавьте в него код:

Скопировать кодPYTHON

```
# kittybot/name_demo.py

def simple_add(a, b):
    return a + b

print(simple_add(2, 2))
print(__name__) 
```

Если запустить этот файл — значение переменной `__name__` будет равно `'__main__'`.

![image](https://pictures.s3.yandex.net/resources/S8_31_1632740947.png)

Создайте в директории проекта ещё один файл, _name_demo2.py_, импортируйте в него функцию `simple_add()` из файла _name_demo.py_.

В этом же файле _name_demo2.py_ вызовите функцию `simple_add(5, 3)` и напечатайте результат вызова. И, дополнительно, из этого же файла напечатайте значение переменной `__name__`.

Скопировать кодPYTHON

```
# kittybot/name_demo2.py

from name_demo import simple_add

print(simple_add(5, 3))
print(__name__) 
```

Запустите файл _name_demo2.py_: в терминал будет выведена такая информация:

![image](https://pictures.s3.yandex.net/resources/S8_32_1632740973.png)

Разберёмся, что тут выведено и почему именно так.

1.  Первым делом из файла _name_demo.py_ импортируется функция `simple_add()`. Помимо функции `simple_add()` в файле есть исполняемый код, и этот код автоматически выполняется при импорте.
    
    Скопировать кодPYTHON
    
    ```
     # kittybot/name_demo.py
    
     # Хотели импортировать только эту функцию
     def simple_add(a, b):
         return a + b
    
     # Но в момент импорта выполнился и этот код:
     print(simple_add(2, 2))
     print(__name__)
      
    ```
    
    Значение переменной `__name__` для этого файла равно `'name_demo'`, а не `'__main__'`: значение изменилось, потому что теперь файл импортирован, а не выполнен как программа.
    
    ![image](https://pictures.s3.yandex.net/resources/S8_33_1632741004.png)
    
2.  После импорта выполнился код из файла _name_demo2.py_:
    
    Скопировать кодPYTHON
    
    ```
     # kittybot/name_demo2.py
    
     from name_demo import simple_add
    
     # Этот код выполнился после импорта
     print(simple_add(5, 3))
     print(__name__)
      
    ```
    
    Этот код вывел в терминал результат работы импортированной функции `simple_add()` и значение переменной `__name__`**:** для файла _name_demo2.py_ она равна `'__main__'` — ведь запущен именно этот файл.
    
    ![image](https://pictures.s3.yandex.net/resources/S07_10_1634025340.png)
    

Кажется, разобрались:

-   если файл запущен как программа — то для него `__name__ == '__main__'`
-   если файл импортирован — то для него `__name__ != '__main__'`

### Какой код импортировать?

Для повторного применения в других проектах будут полезны классы и функции, именно их разработчики захотят импортировать из вашего кода. Но файлы, где хранятся эти классы и функции, могут содержать и исполняемый код — например, вызов функций; этот исполняемый код импортировать не нужно.

Скопировать кодPYTHON

```
# kittybot/name_demo.py

# Полезная функция, пригодится в будущем для импорта в другой проект
def simple_add(a, b):
    return a + b

# Исполняемый код, при импорте он только помешает
print(simple_add(2, 2))
print(__name__) 
```

Конструкция `if __name__ == '__main__'` поможет отделить код, который не нужно импортировать: этот код должен быть обёрнут в условие.

Проверим на практике: добавим в файл _name_demo.py_ условие `if __name__ == '__main__'` и спрячем за него исполняемую часть кода:

Скопировать кодPYTHON

```
# kittybot/name_demo.py

def simple_add(a, b):
    return a + b

if __name__ == '__main__':
    print(simple_add(2, 2))
    print(__name__) 
```

Если запустить на исполнение этот файл, то ничего не изменится — результат работы будет тем же, ведь значение переменной name сейчас равно `'__main__'`.

А вот если запустить на выполнение файл _name_demo2.py_ — то результат его работы станет иным:

![image](https://pictures.s3.yandex.net/resources/S8_35_1632741045.png)

При импорте исполняемый код из файла _name_demo.py_ не выполняется, ведь в этот момент значение переменной `__name__` не равно `'__main__'`.

Чтобы код KittyBot можно было импортировать в другие проекты — его стоит переписать примерно так:

Скопировать кодPYTHON

```
# kittybot/kittybot.py
import os

import requests

from telegram import ReplyKeyboardMarkup
from telegram.ext import CommandHandler, Updater

from dotenv import load_dotenv 

load_dotenv()

secret_token = os.getenv('TOKEN')

URL = 'https://api.thecatapi.com/v1/images/search'


def get_new_image():
    try:
        response = requests.get(URL)
    except Exception as error:
        print(error)
        new_url = 'https://api.thedogapi.com/v1/images/search'
        response = requests.get(new_url)
    
    response = response.json()
    random_cat = response[0].get('url')
    return random_cat


def new_cat(update, context):
    chat = update.effective_chat
    context.bot.send_photo(chat.id, get_new_image())


def wake_up(update, context):
    chat = update.effective_chat
    name = update.message.chat.first_name
    button = ReplyKeyboardMarkup([['/newcat']], resize_keyboard=True)

    context.bot.send_message(
        chat_id=chat.id,
        text='Привет, {}. Посмотри какого котика я тебе нашел'.format(name),
        reply_markup=button
    )

    context.bot.send_photo(chat.id, get_new_image())


def main():
    updater = Updater(token=secret_token)

    updater.dispatcher.add_handler(CommandHandler('start', wake_up))
    updater.dispatcher.add_handler(CommandHandler('newcat', new_cat))

    updater.start_polling()
    updater.idle()


if __name__ == '__main__':
    main() 
```
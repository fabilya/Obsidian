Документация по фильтрам https://python-telegram-bot.readthedocs.io/en/stable/telegram.ext.filters.html
Документация по обработчикам - https://docs.python-telegram-bot.org/en/stable/telegram.ext.html#handlers
### Отправка сообщений: класс Bot()

Начнём с самого простого: создадим экземпляр класса `Bot()` и отправим сообщение. Полная информация об этом классе есть в [документации](https://python-telegram-bot.readthedocs.io/en/stable/telegram.bot.html).

### Класс Updater()

Для получения и обработки входящих сообщений применим класс `Updater()`.

При создании объекта класса `Updater()` в него передаётся токен, так же, как и в случае с классом `Bot()`:

Скопировать кодPYTHON

```
from telegram.ext import Updater

updater = Updater(token='<token>') 
```
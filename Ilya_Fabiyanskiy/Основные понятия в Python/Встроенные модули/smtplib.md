Отправка email по протоколу SMTP
[[Встроенные модули]]
Для отправки email будем использовать SMTP сервер для среды разработки
Для этого потребуется:

* Docker
* Программа `smtp4dev` 
___
1. Проверить `docker version`
2. Проверить какие контейнеры запущены `docker ps`
3. Вставляем команду 

```Python
docker run --rm -it -p 5000:80 -p 2525:25 rnwood/smtp4dev
```
>Веб интерфейс `localhost:5000`

```Python
# создание самого email, конструирование, добавление отправителя, получателя,  
# тела email и т.д.  
from email.message import EmailMessage 
import smtplib  # отправка email сконструированный с помощью EmailMessage  
  
  
my_email = EmailMessage()  
  
# конструирование сообщения  
my_email['from'] = 'Bogdan'  # Отправитель сообщения  
my_email['to'] = 'test@gmail.com'  # Email получателя  
my_email['subject'] = 'Hello from Python'  # Тема письма  
my_email.set_content("Hey! How are you doing?")  # Содержимое письма  
  
# Отправка письма с помощью smtplib  
with smtplib.SMTP(host='localhost', port=2525) as smtp_server:  
    smtp_server.ehlo()  # Связь с smtp-сервером  
    # smtp_server.starttls()  # Начало шифрования    # smtp_server.login('username', 'password')  # Авторизация    smtp_server.send_message(my_email)  # Отправка письма  
    print('Email was sent!')
```

**HTML шаблоны для отправки email**
[[Шаблоны HTML]] - готовые HTML шаблоны красивых писем

`main.py`
```Python
from email.message import EmailMessage  
import smtplib  
from string import Template  
from pathlib import Path  
  
my_email = EmailMessage()  
  
# передача содержимого HTML документа в текстовом формате  
html_template = Template(Path("templates/index.html").read_text())  
# Метод, который позволяет заменить значение переменных в шаблоне HTML  
html_content = html_template.substitute({'name': 'Bogdan', 'date': 'tomorrow'})  
  
my_email['from'] = 'Bogdan'  
my_email['to'] = 'friend@gmail.com'  
my_email['subject'] = "Let's go out"  
my_email.set_content(html_content, 'html')  
  
with smtplib.SMTP(host='localhost', port=2525) as smtp_server:  
    smtp_server.ehlo()  
    smtp_server.send_message(my_email)  
    print('Email was sent!')
```

`index.html`
```HTML
<!doctype html>  
<html lang="en">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport"  
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">  
    <meta http-equiv="X-UA-Compatible" content="ie=edge">  
    <title>Email</title>  
</head>  
<body>  
    <h1>Greetings email</h1>  
    <h2>Hello $name, how are you?</h2>  
    <h2>Let's go out $date</h2>  
</body>  
</html>
```

**Отправка вложений (картинки) в email c `add_attachment()`**

`main.py`
```Python
from email.message import EmailMessage  
import smtplib  
from string import Template  
from pathlib import Path  
  
my_email = EmailMessage()  
  
html_template = Template(Path("templates/index.html").read_text())  
html_content = html_template.substitute({'name': 'Bogdan', 'date': 'tomorrow'})  
  
my_email['from'] = 'Ilya <bs@gmail.com>'  
my_email['to'] = 'friend@gmail.com'  
my_email['subject'] = "Email with image"  
my_email.set_content(html_content, 'html')  
  
# открываем файл в режиме бинарного чтения  
with open('images/cats.jpg', 'rb') as img:  
    # читаем содержимое файла в бинарном режиме  
    image_data = img.read()  
    # добавляем в письмо вложение  
    my_email.add_attachment(image_data,  
                            maintype='image',  
                            subtype='jpg',  
                            filename='cats.jpg')  
  
with smtplib.SMTP(host='localhost', port=2525) as smtp_server:  
    smtp_server.ehlo()  
    smtp_server.send_message(my_email)  
    print('Email was sent!')
```

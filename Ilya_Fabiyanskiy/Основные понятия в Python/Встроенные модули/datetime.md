[[Встроенные модули]]
**date - это класс для работы с датами**
```Python
from datetime import date
my_date = date(2100, 4, 15) # создаем экземпляр класса date
print(type(my_date)) # <class 'type'> это объект, является классом, из него создаются                        экземпляры класса
print(my_date)       # 2100-4-15

# атрибуты и методы доступные my_date
print(my_date.day)   # 15
print(my_date.year)  # 2100
print(my_date.month) # 4

print(my_date.isocalendar()) # datetime.IsoCalendarDate(year=2100, week=15, weekday=4)
```

**time - это класс для работы со временем**
```Python
from datetime import time

my_time = time(18, 10, 45) # создаем экземпляр класса time
print(my_time) # 18:10:45

# атрибуты экземпляра класса my_time
print(my_time.hour)   # 18
print(my_time.minute)  # 10
print(my_time.second) # 45
```

**datetime - из этого класса можно создавать сразу даты и время**
```Python
from datetime import datetime

my_datetime = datetime(2222, 12, 10, 18, 10, 45)
print(my_datetime) # 2222-12-10 18:10:45

# атрибуты
print(my_datetime.year) # 2222
print(my_datetime.second)  # 45
print(my_datetime.microsecond)  # 0

# методы
print(my_datetime.isoformat()) # 2222-12-10T18:10:45
print(my_datetime.now()) # текущая дата и время, создастся новый экземпляр datetime,                             после чего мы можем получить доступ к атрибутам
```

Методы отформатировать дату и время
```Python
from datetime import datetime

my_datetime = datetime(2222, 12, 10, 18, 10, 45)

print(my_datetime.strftime('%d-%b-%Y')) # 10-Dec-2222
print(my_datetime.strftime('%d-%m-%Y')) # 10-12-2222
print(my_datetime.strftime('%d/%m/%Y')) # 10/12/2222
print(my_datetime.strftime('%d-%b-%Y %H:%M:%S')) # 10-Dec-2222 18:10:45
```

**Создание даты из строки создать экземпляр класса `datetime`**
```Python
from datetime import datetime

my_datetime = datetime(2222, 12, 10, 18, 10, 45)

print(my_datetime.strftime('%d/%m/%Y'))
print(my_datetime.strftime('%d-%b-%Y %H:%M:%S')

date_str = '10/12/2222'

converted_date = datetime.strptime(date_str, '%d/%m/%Y')
print(converted_date) # 2222-12-10 00:00:00
```

Использование класса `timedelta`
```Python
from datetime import datetime, timedelta

my_datetime = datetime(2222, 12, 10, 18, 10, 45)

print(timedelta)  # <class 'datetime.timedelta'>

print(my_datetime + timedelta(days=100)) # 2223-03-20 18:10:45
print(my_datetime + timedelta(days=100, hours=2)) # 2223-03-20 20:10:45
print(my_datetime - timedelta(days=100, hours=2)) # 2222-09-01 16:10:45
```
> Можно выполнять разные операции по добавлению или отнять определённого количества дней к текущей дате
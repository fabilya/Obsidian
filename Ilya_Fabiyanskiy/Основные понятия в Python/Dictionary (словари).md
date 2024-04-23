***Словарь***   - это набор элементов `ключ: значение`, **не упорядоченная последовательность** элементов. Все ключи в словаре всегда уникальны.
Значение может быть любым типом

[[Распаковка (unpucking)#^5cb962|Распаковка словаря]]
[[Циклы#^0835eb|Итерация по ключам с значениями в словаре]]

Структура и синтаксис
```
my_motorbike = {
	'brand': 'Ducati',  # Ключи уникальны в словаре, если одинаковые - перезапишет
	'price': 25000,
	'engine_vol': 1.2,
}
```

Порядок элементов в словаре ***не имеет значения***
У элементов в словаре (`ключ: значение`) ***нет уникальных индексов*** (как например есть в списках)

**Получение значений** (всегда стоит использовать метод [[#^0f7d4d |get]])
```
my_motorbike = {
	'brand': 'Ducati',
	'price': 25000,
	'engine_vol': 1.2,
}

print(my_motorbike['brand'])
# Ducati

print(my_motorbike['price'])
# 25000
```

**Изменение значений**
```
my_motorbike['price'] = 20000
print(my_motorbike['price'])
# 20000
```

**Добавление новых элементов**
```
my_motorbike['is_new'] = True  # если такой ключ существует - будет перезаписан
print(my_motorbike)
# {'brand': 'Ducati', 'price': 20000, 'engine_vol': 1.2, 'is_new': True,}
```

**Удаление элементов**
```
del my_motorbike['engine_vol']
print(my_motorbike)
# {'brand': 'Ducati', 'price': 20000, 'is_new': True}
```

**Доступ к значению элемента с помощью переменной**
```
key_name = 'brand'
my_motorbike[key_name] = 'BMW'
print(my_motorbike)
# {'brand': 'BMW', 'price': 20000, 'is_new': True}
```

**Вложенные словари**
```
my_motorbike = {
	'brand': 'Ducati',
	'engine_vol': 1.2,
	'price_info': {              # Значением может быть словарь
		'price': 25000,
		'is_available': True
	}
}

print(my_motorbike['price_info']['price'])
# 25000
print(my_motorbike['price_info']['is_available'])
# True
```

**Использование переменных**
```
brand = 'Ducati'
bike_price = 25000
engine_volume = 1.2

my_motorbike = {
	'brand': brand,
	'price': bike_price,
	'engine_vol': engine_volume,
}

print(my_motorbike)
# {'brand': 'Ducati', 'price': 25000, 'engine_vol': 1.2}
```

**Длина словаря**
```
print(len(my_motorbike))  # считает количество пар ключей (ключ: значение) словаря
# 3
```

Несуществующие ключи
```
print(my_motorbike['model'])    # такого ключа нет в словаре
# KeyError: 'model'             # Ошибка ключа, если не обработать, код остановится
```

**Что делать если не уверены есть ли определенный ключ в словаре?**
В таком случае нужно использовать метод `get` для получения значений ключей
Это более предпочтительный вариант получения значения ключа в словаре 
```
print(my_motorbike.get('model'))
# None                              # Ошибки ключа нет
```

Задать значение по умолчанию для **ключа** если он отсутствует
```
print(get_motorbike.get('model', 0))
# 0
```

Метод `get` для получения значений ключей ^0f7d4d
```
print(get_motorbike.get('brand'))
# Ducati
print(get_motorbike.get('price'))
# 25000
print(get_motorbike.get('model', 0))
# 0
```


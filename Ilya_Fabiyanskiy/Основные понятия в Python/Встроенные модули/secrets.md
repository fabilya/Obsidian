[[Встроенные модули]]
Модуль для генерации паролей
```Python
import secrets  
import string  

# список всех букв, цифр и символов
all_chars = string.ascii_letters + string.digits + string.punctuation  

# генерация паролей
print(''.join(secrets.choice(all_chars) for i in range(30)))
# ]tW}UlJ/(S7&_%|g!+t"p(K`O&hz.:

```
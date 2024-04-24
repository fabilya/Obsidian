[[Встроенные модули]]
**Объектно-ориентированный подход к работе с файлами**
```Python
from pathlib import Path

print(Path('.').absolute())
# D:\Dev\pythonProject

print(type(Path))
# <class 'type'>
```
>Импортируем класс `Path` (почему это класс? Потому что название с большой буквы), далее мы создаем экземпляр этого класса, вызываем функцию конструктор `Path()`, и ей передаем аргумент - строку с путем к текущей директории (относительный путь) и далее получаем новый экземпляр класса `Path`, для него будут доступны различные методы, которые наследуются из класса `Path`, в том числе метод `absolute()` и с помощью вызова этого метода, можно найти абсолютный путь к текущей папке.

**Атрибуты `pathlib Path`**
```Python
from pathlib import Path

file_path = Path('test.txt')  # Относительный путь к файлу

print([m for m in dir(file_path) if not m.startswith('_')])
# ['absolute', 'anchor', 'as_posix', 'as_uri', 'chmod', 'cwd', 'drive', 'exists', 'expanduser', 'glob', 'group', 'home', 'is_absolute', 'is_block_device', 'is_char_device', 'is_dir', 'is_fifo', 'is_file', 'is_mount', 'is_relative_to', 'is_reserved', 'is_socket', 'is_symlink', 'iterdir', 'joinpath', 'lchmod', 'link_to', 'lstat', 'match', 'mkdir', 'name', 'open', 'owner', 'parent', 'parents', 'parts', 'read_bytes', 'read_text', 'readlink', 'relative_to', 'rename', 'replace', 'resolve', 'rglob', 'rmdir', 'root', 'samefile', 'stat', 'stem', 'suffix', 'suffixes', 'symlink_to', 'touch', 'unlink', 'with_name', 'with_stem', 'with_suffix', 'write_bytes', 'write_text']
```

**Путь к текущей директории (пример вызова определенного метода через класс)**
```Python
from pathlib import Path

print(Path.cwd())  # абсолютный путь к текущей папке, где выполняется файл
# D:\Dev\pythonProject
```
> Это можно сделать тогда, когда определенный метод, является `staticmethod` определенным на уровне класса. Ему не нужно передавать экземпляр этого класса.
> `cwd()` - current working directory (текущая рабочая директория)

**Формирование путей на MAC и UNIX**
```Python
from pathlib import Path

print(Path('usr').joinpath('local').joinpath('bin'))
# usr/local/bin

print(Path('usr') / 'local' / 'bin')
# usr/local/bin
```

Формирование путей для WINDOWS
```Python
from pathlib import Path

print(Path('C:/').joinpath('Users').joinpath('ilya'))
# C:\Users\ilya

print(Path('C:/') / 'Users' / 'ilya')
# C:\Users\ilya
```

**Проверка присутствия директории или файла**
```Python
from pathlib import Path

print(Path('main.py').exists())
# True

print(Path('/Users/bogdan/Desktop').exists())
# True

print(Path('other.py').exists())
# False
```

**Как проверить директория или файл?**
```Python
from pathlib import Path

print(Path('main.py').is_file())
# True

print(Path('../python').is_file())
# False

print(Path('../python').is_dir())
# True
```

**Список файлов и папок**
```Python
from pathlib import Path

for f in Path('.').iterdir():
	print(f)

#.env
# .idea
# .venv
# main.py
# other.py
# test.txt
# __pycache__
```
> Можно в цикле проверить, является ли определенный элемент - файлом или директорией, и сформировать список только из файлов, исключив директории, используя метод `is_file()`

**Создать новую папку или удалить папку**
```Python
from pathlib import Path  
  
my_dir = Path('D:/') / 'Dev' / 'pythonProject' / 'django'  

# классический метод
if not my_dir.exists():  # Создание папки 
    my_dir.mkdir()  

# с использованием аргумента exist_ok=True
my_dir.mkdir(exist_ok=True)

if my_dir.exists():    # Удаление папки
    my_dir.rmdir()
```
>Если папка существует, выдаст ошибку, поэтому нужно использовать инструкцию `if`, либо можно вызвать именованный аргумент в функции `mkdir(exist_ok=True)`


**Чтение и запись файлов** ^a44b22
```Python
with open('new.txt', 'w') as new_file:
	new_file.write("First line in the new file\n")
```
> Записывать файл можно при вызове функции `open()` с передачей аргумента `'w'` - открыть файл для записи, при этом, если в файле было содержимое, то здесь это содержимое **пере запишется** (т.к. файл открывается в режиме записи `'w'`)
> При использовании инструкции `with` после завершения всех операций с файлом, метод `close()` вызовется автоматически

```Python
with open('new.txt') as new_file:
	print(new_file.read())
	# First line in the new file
```
> По умолчанию если не передавать второй аргумент в вызове функции `open` то файл открывается для чтения, и записать туда ничего нельзя

```Python
with open('new.txt', 'a') as new_file:
	new_file.write("Second line in the new file\n")

with open('new.txt') as new_file:
	print(new_file.read())
	# First line in the new file
	# Second line in the new file
```
> Открыть файл для **до записи** (`'a'` (append)), в таком случае эта строка будет добавлена внизу существующих строк 

**Удаления файла**
```Python
from pathlib import Path

print(Path('new.txt').exists())
# True

Path('new.txt').unlink()

print(Path('new.txt').exists())
# False
```

>[!Задача]
>1. Создайте папку `files` в текущей папке
>2. Добавьте два файла `first.txt` и `second.txt` в эту папку и запишите в них по 2-3 строки текста
>3. Прочитайте все строки первого файла
>4. Прочитайте строки второго файла одна за другой
>5. Удалите оба файла
>6. Удалите папку `files`

##### Решение
```Python
from pathlib import Path  
  
files_dir = Path('files')  
files_dir.mkdir(exist_ok=True)  
  
first_file = files_dir / 'first.txt'  
second_file = files_dir / 'second.txt'  
  
with open(first_file, 'w') as f:  
    f.write('Hello world!\n'  
            'This is my first file.\n'  
            'I am learning Python.\n')  
  
with open(second_file, 'w') as f:  
    lines = [  
        "First line in the second file",  
        "Second line in the second file",  
        "Last line in the second file"  
    ]  
    for line in lines:  
        f.write(line + '\n')  
  
with open(first_file) as f:  
    print(f.read())  
  
with open(second_file) as f:  
    # Option 1  
    for line in f:  
        print(line.strip())  
  
    # Option 2 
    # while True:
    #     line = f.readline()
    #     print(line.strip())    
    #     if not line:    
    #         break  
    
first_file.unlink()  
second_file.unlink()  
  
files_dir.rmdir()
```
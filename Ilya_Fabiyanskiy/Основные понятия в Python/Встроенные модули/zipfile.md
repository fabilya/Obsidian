[[Встроенные модули]]
**Создание zip архива**
```Python
from zipfile import ZipFile  
from pathlib import Path  
  
  
with ZipFile('my-files.zip', mode='w') as my_zip_file:  
    for file in Path('my-files').iterdir():   # Итерация по директории
        print(file)  # my-files/first.txt  # my-files/second.txt
        my_zip_file.write(file, file.name)  # запись файла в zip архив
```
>`my-files.zip` название архива, будет создан в корневой директории.
>`w` - режим "записи"

**Распаковка zip архива**
```Python
from zipfile import ZipFile  
  
  
with ZipFile('my-files.zip') as my_zip_file:  
    my_zip_file.extractall('my-files-unzipped')
```



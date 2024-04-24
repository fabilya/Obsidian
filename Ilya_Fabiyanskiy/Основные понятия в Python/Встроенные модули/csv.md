[[Встроенные модули]]
Работа с CSV файлами
CSV - это универсальный формат сохранения данных, которые разделяются определенными символами.

**Создание csv файла**
```Python
import csv  
  
with open('test.csv', 'w') as csv_file:  
    writer = csv.writer(csv_file, lineterminator='\n')  
    writer.writerow(['user_id', 'user_name', 'comments_qty'])  
    writer.writerow([5235, 'ilya', 1352])  
    writer.writerow([4428, 'mike', 246])  
    writer.writerow([1684, 'alice', 73])
```

**Чтение из csv файла**
```Python
import csv


with open('test.csv') as csv_file:  
    reader = csv.reader(csv_file)  
    for line in reader:  
        print(line)
```
>По объекту `reader` можно выполнить итерацию только один раз
>Потому, если необходимо прочесть csv файл несколько раз, необходимо несколько раз создавать соответствующий объект `reader` и выполнять по нему итерацию. 
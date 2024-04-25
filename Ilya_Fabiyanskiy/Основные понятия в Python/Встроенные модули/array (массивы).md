[[Встроенные модули]]
Использование таких массивов более эффективно нежели использование списков, в массивах доступно больше методов для работы с такой структурой данных (если необходимо создавать однотипные структуры данных)

```Python
from array import array  
  
my_int_array = array('i', [4, 10, 5, 5, 5, 7])  
  
with open('my_array.bin', 'wb') as my_file:  
    my_int_array.tofile(my_file)  
  
  
imported_array = array('i')  
  
with open('my_array.bin', 'rb') as my_file:  
    imported_array.fromfile(my_file, 3)  
    print(imported_array)  
  
  
imported_array.reverse()  
print(imported_array)
```
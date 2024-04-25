[[Встроенные модули]]
`sys.argv` - Работа с аргументами программы
```Python
import sys  
  
# аргументы при вызове файла  
print(sys.argv)  # ['main.py', 'dsahjkdas', '1231231']  
  
if len(sys.argv) < 3:  
    raise IOError("You must provide username and password")  
  
# username = sys.argv[1]  
# password = sys.argv[2]  
  
filename, username, password = sys.argv  
  
print(username, password)  # dsahjkdas 1231231
```

![[Pasted image 20240425114159.png]]
[Who likes it?](https://www.codewars.com/kata/5266876b8f4bf2da9b000362/solutions/python)
You probably know the "like" system from Facebook and other pages. People can "like" blog posts, pictures or other items. We want to create the text that should be displayed next to such an item.

Implement the function which takes an array containing the names of people that like an item. It must return the display text as shown in the examples:

```Python
[]                                -->  "no one likes this"
["Peter"]                         -->  "Peter likes this"
["Jacob", "Alex"]                 -->  "Jacob and Alex like this"
["Max", "John", "Mark"]           -->  "Max, John and Mark like this"
["Alex", "Jacob", "Mark", "Max"]  -->  "Alex, Jacob and 2 others like this"
```

Note: For 4 or more names, the number in `"and 2 others"` simply increases.

### Решение с использованием словаря
```Python
def likes(names):
    n = len(names)
    return {
        0: 'no one likes this',
        1: '{} likes this', 
        2: '{} and {} like this', 
        3: '{}, {} and {} like this', 
        4: '{}, {} and {others} others like this'
    }[min(4, n)].format(*names[:3], others=n-2)
```

___

[Thinkful - Logic Drills: Traffic light](https://www.codewars.com/kata/58649884a1659ed6cb000072/solutions/python)
You're writing code to control your town's traffic lights. You need a function to handle each change from `green`, to `yellow`, to `red`, and then to `green` again.

Complete the function that takes a string as an argument representing the current state of the light and returns a string representing the state the light should change to.

For example, when the input is `green`, output should be `yellow`.

### Решение с использованием словаря
```Python
def update_light(current):
    return {"green": "yellow", "yellow": "red", "red": "green"}[current]
```

___

[Will there be enough space?](https://www.codewars.com/kata/5875b200d520904a04000003/solutions/python)
Bob is working as a bus driver. However, he has become extremely popular amongst the city's residents. With so many passengers wanting to get aboard his bus, he sometimes has to face the problem of not enough space left on the bus! He wants you to write a simple program telling him if he will be able to fit all the passengers.

### Task Overview:

You have to write a function that accepts three parameters:

- `cap` is the amount of people the bus can hold excluding the driver.
- `on` is the number of people on the bus excluding the driver.
- `wait` is the number of people waiting to get on to the bus excluding the driver.

If there is enough space, return 0, and if there isn't, return the number of passengers he can't take.

### Решение с использованием `max()`
```Python
def enough(cap, on, wait):
    return max(0, wait - (cap - on))
```

___

[Is it a palindrome?](https://www.codewars.com/kata/57a1fd2ce298a731b20006a4/solutions/python)
Write a function that checks if a given string (case insensitive) is a [palindrome](https://en.wikipedia.org/wiki/Palindrome).

A palindrome is a word, number, phrase, or other sequence of symbols that reads the same backwards as forwards, such as `madam` or `racecar`.

```Python
def is_palindrome(s):  
    start = 0  # Указатель 1 начинает начало строки
    end = len(s) - 1  # Указатель 2 начинается в конце строки
    while start < end: # Пока первый указатель меньше второго 
    # Сравнивает значения первого и последнего символов строки
        if s[start] == s[end]:  
            start += 1 # Увеличивает положение указателя 1
            end -= 1 # Уменьшает положение указателя 1
            continue  
        else: # Возвращает false, если значения не совпадают
            return False  
    return True # Если цикл while прерывается, возвращает true
```

___

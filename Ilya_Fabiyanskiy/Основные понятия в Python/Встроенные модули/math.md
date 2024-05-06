[[Встроенные модули]]
```Python
import math  
  
# константа ПИ и константа Е  
print(math.pi)  
print(math.e)  
  
# корень квадртаный из определенного числа  
print(math.sqrt(25))  
  
# логорифмы  
print(math.log(100))  
  
# факториал  
print(math.factorial(10))

# произведение всех элементов
math.prod([4, 1, 1, 4]) # 16
math.prod([4, 1, 1, 4], start=2) # 32

# посмотреть все доступные атрибуты  
print(dir(math))  
# ['__doc__', '__loader__', '__name__', '__package__', '__spec__', 'acos', 'acosh', 'asin', 'asinh', 'atan', 'atan2', 'atanh', 'ceil', 'comb', 'copysign', 'cos', 'cosh', 'degrees', 'dist', 'e', 'erf', 'erfc', 'exp', 'expm1', 'fabs', 'factorial', 'floor', 'fmod', 'frexp', 'fsum', 'gamma', 'gcd', 'hypot', 'inf', 'isclose', 'isfinite', 'isinf', 'isnan', 'isqrt', 'lcm', 'ldexp', 'lgamma', 'log', 'log10', 'log1p', 'log2', 'modf', 'nan', 'nextafter', 'perm', 'pi', 'pow', 'prod', 'radians', 'remainder', 'sin', 'sinh', 'sqrt', 'tan', 'tanh', 'tau', 'trunc', 'ulp']
```



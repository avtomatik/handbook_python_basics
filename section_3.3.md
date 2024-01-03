# 3. Коллекции и работа с памятью

## 3.3. Списочные выражения. Модель памяти для типов языка Python

### A. Список квадратов
```python
[_ ** 2 for _ in range(a, 1 + b)]
```

### B. Таблица умножения 2.0
```python
[[(1 + i) * (1 + j) for i in range(n)] for j in range(n)]
```

### C. Длины всех слов
```python
[len(_) for _ in sentence.split()]
```

### D. Множество нечетных чисел
```python
{_ for _ in numbers if _ % 2 == 1}
```

### E. Множество всех полных квадратов
```python
{_ for _ in numbers if _ ** .5 % 1 == 0}
```

### F. Буквенная статистика
```python
{_: text.lower().count(_) for _ in set(filter(str.isalpha, text.lower()))}
```

### G. Делители
```python
{
    number: [1 + _ for _ in range(number) if number % (1 + _) == 0]
    for number in numbers
}
```

### H. Аббревиатура
```python
''.join(_[0] for _ in string.split()).upper()
```

### I. Преобразование в строку
```python
' - '.join(str(_) for _ in sorted(set(numbers)))
```

### J. RLE наоборот
```python
''.join(symbol for symbol, count in rle for _ in range(count))
```

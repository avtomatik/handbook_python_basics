# 4. Функции и их особенности в Python

## 4.1. Функции. Области видимости. Передача параметров в функции

### A. Функциональное приветствие
```python
def print_hello(string: str) -> None:
    print(f'Hello, {string}!')
```

### B. Функциональный НОД
```python
def gcd(a: int, b: int) -> int:
    while b:
        a, b = b, a % b
    return a
```

### C. Длина числа
```python
def number_length(number: int) -> int:
    number, deg = abs(number), 1

    while divmod(number, 10 ** deg)[0]:
        deg += 1
    return deg
```

### D. Имя of the month
```python
def month(number: int, language: str) -> str:
    MONTHS = {
        'ru': [
            'январь',
            'февраль',
            'март',
            'апрель',
            'май',
            'июнь',
            'июль',
            'август',
            'сентябрь',
            'октябрь',
            'ноябрь',
            'декабрь'
        ],
        'en': [
            'january',
            'february',
            'march',
            'april',
            'may',
            'june',
            'july',
            'august',
            'september',
            'october',
            'november',
            'december'
        ]
    }

    return dict(enumerate(MONTHS.get(language), 1)).get(number).title()
```

### E. Числовая строка
```python
def split_numbers(feed: str) -> tuple[int]:
    return tuple(map(int, feed.split()))
```

### F. Модернизация системы вывода
```python
def modern_print(prompt: str, prompts_tracked: set[str] = set()) -> None:
    if prompt not in prompts_tracked:
        prompts_tracked.add(prompt)
        print(prompt)
```

### G. Шахматный «обед»
```python
from operator import sub


def can_eat(start: tuple[int], final: tuple[int]) -> bool:
    return sum(map(lambda _: _ ** 2, map(sub, final, start))) == 5
```

### H. А роза упала на лапу Азора 7.0
```python
def is_palindrome(feed):
    if isinstance(feed, int):
        feed = str(feed)
    return all(x == y for x, y in zip(feed[:len(feed) // 2], feed[len(feed) // 2:][::-1]))
```

### I. Простая задача 5.0
```python
import math


def is_prime(number: int) -> bool:
    if number <= 1:
        return False

    for _ in range(2, 1 + int(math.sqrt(number))):
        if number % _ == 0:
            return False
    return True
```

### J. Слияние
```python
def merge(left: tuple[int], right: tuple[int]) -> tuple[int]:

    left, right, combined = list(left), list(right), list()

    while left and right:
        if min(left) < min(right):
            combined.append(left.pop(0))
        else:
            combined.append(right.pop(0))

    if left:
        combined.extend(left)
    else:
        combined.extend(right)

    return tuple(combined)
```
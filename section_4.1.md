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
def can_eat(start: tuple[int, int, int], final: tuple[int, int, int]) -> bool:
    return sum(abs(f - s) for s, f in zip(start, final)) == 3
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
def is_prime(n: int) -> bool:
    if n <= 1:
        return False
    if n <= 3:
        return True
    if n % 2 == 0 or n % 3 == 0:
        return False
    i = 5
    while i * i <= n:
        if n % i == 0 or n % (i + 2) == 0:
            return False
        i += 6
    return True
```

### J. Слияние
```python
def merge(left: tuple[int], right: tuple[int]) -> tuple[int]:

    combined = []

    left_ix, right_ix = 0, 0

    left_sz, right_sz = len(left), len(right)

    while left_ix < left_sz and right_ix < right_sz:
        if left[left_ix] <= right[right_ix]:
            combined.append(left[left_ix])
            left_ix += 1
        else:
            combined.append(right[right_ix])
            right_ix += 1

    combined.extend(left[left_ix:])
    combined.extend(right[right_ix:])

    return tuple(combined)
```
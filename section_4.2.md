# 4. Функции и их особенности в Python

## 4.2. Позиционные и именованные аргументы. Функции высших порядков. Лямбда-функции

### A. Генератор списков
```python
from typing import Any


def make_list(length: int, value: Any = 0) -> list[Any]:
    return [value for _ in range(length)]
```

### B. Генератор матриц
```python
from typing import Any


def make_matrix(size: tuple[int] | int, value: Any = 0) -> list[list[Any]]:

    if isinstance(size, tuple):
        width, height = size
    else:
        width, height = size, size

    return [[value for _ in range(width)] for i in range(height)]
```

### C. Функциональный нод 2.0
```python
from functools import reduce


def gcd(*args):

    def main(a: int, b: int) -> int:
        while b:
            a, b = b, a % b
        return a

    return reduce(main, args)
```

### D. Имя of the month 2.0
```python
def month(number: int, language: str = 'ru') -> str:
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

### E. Подготовка данных
```python
def to_string(*args, sep: str = ' ', end: str = '\n') -> str:
    return f'{sep.join(map(str, args))}{end}'
```

### F. Кофейня
```python
def order(*beverages: tuple[str]) -> str:
    global in_stock

    FORMULAE = {
        'Эспрессо': {'coffee': 1},
        'Капучино': {'coffee': 1, 'milk': 3},
        'Макиато': {'coffee': 2, 'milk': 1},
        'Кофе по-венски': {'coffee': 1, 'cream': 2},
        'Латте Макиато': {'coffee': 1, 'milk': 2, 'cream': 1},
        'Кон Панна': {'coffee': 1, 'cream': 1},
    }

    for beverage in beverages:
        if all(
            value <= in_stock.get(key)
            for key, value in FORMULAE.get(beverage).items()
        ):
            in_stock = {
                key: value - FORMULAE.get(beverage).get(key, 0)
                for key, value in in_stock.items()
            }
            return beverage
    return 'К сожалению, не можем предложить Вам напиток'
```

### G. В эфире рубрика «Эксперименты»
```python
numbers = []


def enter_results(*args) -> None:
    global numbers

    numbers.extend([*args])


def get_sum() -> tuple[float]:
    return round(sum(numbers[::2]), 2), round(sum(numbers[1::2]), 2)


def get_average() -> tuple[float]:
    return (
        round(2 * sum(numbers[::2]) / len(numbers), 2),
        round(2 * sum(numbers[1::2]) / len(numbers), 2)
    )
```

### H. Длинная сортировка
```python
lambda _: (len(_), _.lower())
```

### I. Чётная фильтрация
```python
lambda _: sum(map(int, str(_))) % 2 == 0
```

### J. Ключевой секрет
```python
from itertools import cycle


def secret_replace(string: str, **kwargs: dict[str, str]) -> str:
    swaps = {key: cycle(value) for key, value in kwargs.items()}

    enciphered = []

    for letter in string:
        swap_cycle = swaps.get(letter)
        enciphered.append(
            next(swap_cycle)
        ) if swap_cycle else enciphered.append(letter)

    return ''.join(enciphered)
```

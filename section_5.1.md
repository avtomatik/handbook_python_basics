# 5. Объектно-ориентированное программирование

## 5.1. Объектная модель Python. Классы, поля и методы

### A. Классная точка
```python
class Point:

    def __init__(self, x: int, y: int):
        self.x = x
        self.y = y
```

### B. Классная точка 2.0
```python
class Point:

    def __init__(self, x: int, y: int):
        self.x = x
        self.y = y

    def move(self, x: int, y: int):
        self.x += x
        self.y += y

    def length(self, other) -> float:
        return round(
            (
                sum(
                    map(lambda _: _ ** 2, (self.x - other.x, self.y - other.y))
                )
            ) ** .5,
            2
        )
```

### C. Не нажимай красную кнопку!
```python
class RedButton:

    def __init__(self):
        self.counter = 0

    def click(self):
        print('Тревога!')
        self.counter += 1

    def count(self):
        return self.counter
```

### D. Работа не волк
```python
class Programmer:

    def __init__(self, name, grade):
        self.BASE_HOURLY_WAGES = {
            'Junior': 10,
            'Middle': 15,
            'Senior': 20,
        }
        self.name = name
        self.grade = grade
        self.time = 0
        self.wage = 0
        self.hourly_wage = self.BASE_HOURLY_WAGES.get(self.grade, 0)

    def work(self, time):
        self.time += time
        self.wage += self.hourly_wage * time

    def rise(self):
        if self.grade == 'Senior':
            self.hourly_wage += 1
        elif self.grade == 'Junior':
            self.grade = 'Middle'
            self.hourly_wage = self.BASE_HOURLY_WAGES.get(self.grade, 0)
        elif self.grade == 'Middle':
            self.grade = 'Senior'
            self.hourly_wage = self.BASE_HOURLY_WAGES.get(self.grade, 0)

    def info(self):
        return f'{self.name} {self.time}ч. {self.wage}тгр.'
```

### E. Классный прямоугольник
```python
from functools import reduce
from operator import mul, sub


class Rectangle:

    def __init__(self, vertex, opposite):
        self.vertex = vertex
        self.opposite = opposite

    def perimeter(self):
        return 2 * round(
            sum(map(abs, map(sub, self.vertex, self.opposite))),
            2
        )

    def area(self):
        return round(
            reduce(mul, map(abs, map(sub, self.vertex, self.opposite))),
            2
        )
```

### F. Классный прямоугольник 2.0
```python
from functools import reduce
from itertools import chain
from operator import sub


class Rectangle:

    def __init__(self, *corners):
        self.corners = corners
        self.coordinates = tuple(chain(*self.corners))

        self.width = round(
            reduce(sub, sorted(self.coordinates[::2], reverse=True)),
            2
        )
        self.height = round(
            reduce(sub, sorted(self.coordinates[1::2], reverse=True)),
            2
        )

    def perimeter(self):
        return round(2 * sum(self.get_size()), 2)

    def area(self):
        return round(self.width * self.height, 2)

    def get_pos(self):
        return min(self.coordinates[::2]), max(self.coordinates[1::2])

    def get_size(self):
        return self.width, self.height

    def move(self, dx, dy):
        self.coordinates = tuple(
            map(
                lambda _: round(_, 2),
                (
                    _ + dx if idx % 2 == 0 else _ + dy
                    for idx, _ in enumerate(self.coordinates)
                )
            )
        )

    def resize(self, width, height):
        x, y = self.get_pos()
        self.__init__((x, y), (round(x + width, 2), round(y - height, 2)))
```

### G. Классный прямоугольник 3.0
```
Неверное решение
```

### H. Шашки
```python
class Checkers:

    def __init__(self):
        self.cols, self.rows = 'ABCDEFGH', '12345678'

        pre_board = {
            self._flatten(f'{col}{row}'): self._set_out(f'{col}{row}')
            for col in self.cols
            for row in self.rows
        }

        self.board = list(dict(sorted(pre_board.items())).values())

    def move(self, f, t):
        if self.board[self._flatten(t)].status() in ['X']:
            self.board[self._flatten(t)] = self.board[self._flatten(f)]
            self.board[self._flatten(f)] = Cell('X')

    def get_cell(self, p):
        return self.board[self._flatten(p)]

    def _flatten(self, address: str, letters: str = 'ABCDEFGH') -> int:
        col, row = address
        return ord(col) % 64 + (int(row) - 1) * len(letters) - 1

    def _is_main(self, address: str) -> bool:
        col, row = address
        return (ord(col) % 64 + int(row)) % 2 == 0

    def _set_out(self, address: str, letters: str = 'ABCDEFGH') -> str:

        flag, characteristic, xn = self._is_main(
            address), self._flatten(address), len(letters)

        if flag and characteristic <= 3 * xn:
            return Cell('W')

        if flag and characteristic > 5 * xn:
            return Cell('B')

        return Cell('X')


class Cell:

    def __init__(self, state):
        self.state = state

    def status(self):
        return self.state
```

### I. Очередь
```python
class Queue:

    def __init__(self):
        self.container = []

    def push(self, item):
        self.container.append(item)

    def pop(self):
        return self.container.pop(0)

    def is_empty(self):
        return not bool(self.container)
```

### J. Стек
```python
class Stack:

    def __init__(self):
        self.container = []

    def push(self, item):
        self.container.append(item)

    def pop(self):
        return self.container.pop()

    def is_empty(self):
        return not bool(self.container)
```

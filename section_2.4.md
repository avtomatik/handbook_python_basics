# 2. Базовые конструкции Python

## 2.4. Вложенные циклы

### A. Таблица умножения
```python
feed = int(input())


for i in range(feed):
    print(' '.join(str((1 + i) * (1 + j)) for j in range(feed)))
```

### B. Не таблица умножения
```python
feed = int(input())


for i in range(feed):
    for j in range(feed):
        print(f'{(1 + j)} * {(1 + i)} = {(1 + i) * (1 + j)}')
```

### C. Новогоднее настроение
```python
import math


def get_level(number: int) -> int:
    return math.ceil(math.sqrt(.25 + 2 * number) - .5)


def get_bound(number: int) -> float:
    return 1 + number * (number - 1) / 2


def get_fir_tree(feed: int) -> list[list[int | None]]:
    fir_tree = []
    for j in range(1 + get_level(feed)):
        branch = []
        for i in range(j):
            current = get_bound(j) + i
            if current > feed:
                break

            branch.append(int(current))

        fir_tree.append(branch)
    return fir_tree


def main(fir_tree: list[list[int | None]]) -> None:
    for branch in fir_tree:
        if branch:
            print(' '.join(map(str, branch)))


if __name__ == '__main__':
    main(get_fir_tree(int(input())))
```

### D. Суммарная сумма
```python
def main(feed: list[str]) -> int:
    return sum(map(lambda _: sum(map(int, _)), feed))


if __name__ == '__main__':
    print(main([input() for _ in range(int(input()))]))
```

### E. Зайка — 5
```python
def count_entries(localities: list[str], target: str = 'зайка') -> int:
    return sum(map(lambda _: target in _, localities))


localities, locality = [], []

for num in range(int(input())):
    while (entry := input()) != 'ВСЁ':
        locality.append(entry)
    else:
        localities.append(locality)
        locality = []

print(count_entries(localities))
```

### F. НОД 2.0
```python
from itertools import combinations


def gcd(a: int, b: int) -> int:
    while b:
        a, b = b, a % b
    return a


feed = [int(input()) for _ in range(int(input()))]

print(min(map(lambda _: gcd(*_), combinations(feed, 2))))
```

### G. На старт! Внимание! Марш!
```python
for j in range(int(input())):
    for i in range(3 + j, 0, -1):
        print(f'До старта {i} секунд(ы)')
    print(f'Старт {1 + j}!!!')
```

### H. Максимальная сумма
```python
players, scores = [], []

for _ in range(2 * int(input())):
    if _ % 2 == 0:
        players.append(input())
    else:
        scores.append(sum(map(int, input())))


BOARD = dict(zip(players, scores))


winner, max_score = '', 0

for player, score in BOARD.items():
    if score >= max_score:
        winner = player
        max_score = score

print(winner)
```

### I. Большое число
```python
feeds = [input() for _ in range(int(input()))]

print(''.join(max(feed) for feed in feeds))
```

### J. Мы делили апельсин
```python
from itertools import product


number = int(input())

print(*list('АБВ'))

for pair in product(range(1, number - 1), repeat=2):
    rest = number - sum(pair)
    if rest > 0:
        print(*pair, rest)
```

### K. Простая задача 3.0
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


print(sum(map(is_prime, [int(input()) for _ in range(int(input()))])))
```

### L. Числовой прямоугольник
```python
rows, cols = int(input()), int(input())

width = len(str(rows * cols))

for row in range(rows):
    print(' '.join(f'{1 + row * cols + col:>{width}}' for col in range(cols)))
```

### M. Числовой прямоугольник 2.0
```python
rows, cols = int(input()), int(input())

width = len(str(rows * cols))

for row in range(rows):
    print(' '.join(f'{1 + row + rows * col:>{width}}' for col in range(cols)))
```

### N. Числовая змейка
```python
def get_elem(unit: int, total: int, orthogonal: int) -> int:
    return orthogonal * total + (
        1 + unit if orthogonal % 2 == 0 else total - unit
    )


rows, cols = int(input()), int(input())

width = len(str(rows * cols))

for row in range(rows):
    print(
        ' '.join(f'{get_elem(col, cols, row):>{width}}' for col in range(cols))
    )
```

### O. Числовая змейка 2.0
```python
def get_elem(unit: int, total: int, orthogonal: int) -> int:
    return orthogonal * total + (
        1 + unit if orthogonal % 2 == 0 else total - unit
    )


rows, cols = int(input()), int(input())

width = len(str(rows * cols))

for row in range(rows):
    print(
        ' '.join(f'{get_elem(row, rows, col):>{width}}' for col in range(cols))
    )
```

### P. Редизайн таблицы умножения
```python
dim, width = int(input()), int(input())


for row in range(2 * dim - 1):
    if row % 2 == 0:
        print(
            '|'.join(
                f'{(1 + row // 2) * (1 + col):^{width}}' for col in range(dim)
            )
        )
    else:
        print(f'{"":{"-"}^{(1 + width) * dim - 1}}')
```

### Q. А роза упала на лапу Азора 3.0
```python
def is_palindrome(pseudonumber: str) -> bool:
    return all(
        x == y for x, y in zip(pseudonumber[:len(pseudonumber) // 2], pseudonumber[len(pseudonumber) // 2:][::-1])
    )


feeds = [input() for _ in range(int(input()))]

print(sum(map(is_palindrome, feeds)))
```

### R. Новогоднее настроение 2.0
```python
import math


def get_level(number: int) -> int:
    return math.ceil(math.sqrt(.25 + 2 * number) - .5)


def get_bound(number: int) -> float:
    return 1 + number * (number - 1) / 2


def get_fir_tree(feed: int) -> list[list[int | None]]:
    fir_tree = []
    for j in range(1 + get_level(feed)):
        branch = []
        for i in range(j):
            current = get_bound(j) + i
            if current > feed:
                break

            branch.append(int(current))

        fir_tree.append(branch)
    return fir_tree


def main(fir_tree: list[list[int | None]], width: int) -> None:
    for branch in fir_tree:
        if branch:
            print(f'{" ".join(map(str, branch)):^{width}}')


if __name__ == '__main__':

    fir_tree = get_fir_tree(int(input()))

    width = len(' '.join(map(str, fir_tree[-1])))
    
    main(fir_tree, width)
```

### S. Числовой квадрат
```python
def get_value(dim, row, col):
    return (1 + dim) / 2 - max(abs(row + (1 - dim) / 2), abs(col + (1 - dim) / 2))


def get_square(dim):
    return [
        list(map(int, (get_value(dim, row, col) for col in range(dim)))) for row in range(dim)
    ]


dim = int(input())
width = len(str((1 + dim) // 2))
square = get_square(dim)

for row in square:
    print(' '.join(map(lambda _: f'{_:>{width}}', map(str, row))))
```

### T. Математическая выгода
```python
def convert_base(number, base) -> list[int]:
    result = []
    current = number
    while current:
        result.append(current % base)
        current //= base

    return result[::-1]


number = int(input())


board = {}
for base in range(2, 11):
    board[base] = sum(convert_base(number, base))


print(max(board, key=board.get))
```

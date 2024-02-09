# 2. Базовые конструкции Python

## 2.2. Условный оператор

### A. Просто здравствуй, просто как дела
```python
FEEDBACK = {
    'хорошо': 'Я за вас рада!',
    'плохо': 'Всё наладится!',
}

NEW_LINE = '\n'

print(f'Здравствуйте, {input(f"Как Вас зовут?{NEW_LINE}")}!')

print(f'{FEEDBACK.get(input(f"Как дела?{NEW_LINE}"))}')
```

### B. Кто быстрее?
```python
print('Петя' if int(input()) > int(input()) else 'Вася')
```

### C. Кто быстрее на этот раз?
```python
BOARD = dict(zip('Петя Вася Толя'.split(), (int(input()), int(input()), int(input()))))

print(max(BOARD, key=BOARD.get))
```

### D. Список победителей
```python
BOARD = dict(
    zip(
        'Петя Вася Толя'.split(),
        (int(input()), int(input()), int(input()))
    )
)

for _, key in enumerate(dict(sorted(BOARD.items(), key=lambda item: item[1], reverse=True)).keys(), 1):
    print(f'{_}. {key}')
```

### E. Яблоки
```python
print('Петя' if int(input()) > 6 + int(input()) else 'Вася')
```

### F. Сила прокрастинации
```python
year = int(input())

print('YES' if year % 4 == 0 and (year % 100 != 0 or year % 400 == 0) else 'NO')
```

### G. А роза упала на лапу Азора
```python
def is_palindrome(feed: str) -> bool:
    return all(
        x == y for x, y in zip(feed[:len(feed) // 2], feed[len(feed) // 2:][::-1])
    )


print('YES' if is_palindrome(input()) else 'NO')
```

### H. Зайка — 1
```python
print('YES' if 'зайка' in input().split() else 'NO')
```

### I. Первому игроку приготовиться
```python
print(min([input(), input(), input()]))
```

### J. Лучшая защита — шифрование
```python
feed = input()

sum_low = sum(map(int, feed[-2:]))
sum_fore = sum(map(int, feed[:2]))

print(f'{max((sum_low, sum_fore))}{min((sum_low, sum_fore))}')
```

### K. Красота спасёт мир
```python
numbers = sorted(list(map(int, input())))
min_val = numbers.pop(0)
max_val = numbers.pop(-1)
mid_val = numbers.pop()

print('YES' if 2 * mid_val == min_val + max_val else 'NO')
```

### L. Музыкальный инструмент
```python
a, b, c = int(input()), int(input()), int(input())

print('YES' if 2 * max((a, b, c)) < sum((a, b, c)) else 'NO')
```

### M. Властелин Чисел: Братство общей цифры
```python
elves, dwarves, humans = input(), input(), input()

low = set(map(lambda _: _[-1], (elves, dwarves, humans)))
high = set(map(lambda _: _[0], (elves, dwarves, humans)))

for cat in (low, high):
    if len(cat) == 1:
        elem = cat.pop()

print(int(elem))
```

### N. Властелин Чисел: Две Башни
```python
def main(feed: str) -> str:
    digits_sorted = sorted(feed)
    return ' '.join(
        [get_min_two_digits(digits_sorted), get_max_two_digits(digits_sorted)]
    )


def get_min_two_digits(digits: list[str]) -> str:
    if '0' in digits:
        return f'{"".join(digits[:2][::-1])}'
    return f'{"".join(digits[:2])}'


def get_max_two_digits(digits: list[str]) -> str:
    return f'{"".join(digits[1:][::-1])}'


if __name__ == '__main__':
    print(main(input()))
```

### O. Властелин Чисел: Возвращение Цезаря
```python
def main(one: str, another: str) -> str:
    digits_sorted = sorted(''.join([one, another]))
    return ''.join(
        [
            digits_sorted[-1],
            str(sum(map(int, digits_sorted[1:3])) % 10),
            digits_sorted[0]
        ]
    )


if __name__ == '__main__':
    print(main(input(), input()))
```

### P. Легенды велогонок возвращаются: кто быстрее?
```python
WIDTH = 8

BOARD = dict(
    zip('Петя Вася Толя'.split(), (int(input()), int(input()), int(input())))
)


for _, key in enumerate(dict(sorted(BOARD.items(), key=lambda item: item[1], reverse=True)).keys()):
    if _ % 2 == 0:
        print(f'{"":^{_ * WIDTH}}{key:^{(len(BOARD) - _) * WIDTH}}')
    else:
        print(f'{key:^{_ * WIDTH}}{"":^{(len(BOARD) - _) * WIDTH}}')

print(f'{"II":^{WIDTH}}{"I":^{WIDTH}}{"III":^{WIDTH}}')
```

### Q. Корень зла
```python
import math


def find_roots(a: float, b: float, c: float) -> str:
    if a == .0 and b == .0 and c == .0:
        return 'Infinite solutions'

    elif a == .0 and b != .0:
        X = [-c / b]

    elif a == .0:
        return 'No solution'

    else:
        d = b ** 2 - 4 * a * c

        if d < .0:
            return 'No solution'
        elif d == .0:
            X = [-b / (2 * a)]
        else:
            X = [-(b + math.sqrt(d)) / (2 * a), (-b + math.sqrt(d)) / (2 * a)]

    return ' '.join(map(lambda _: f'{_:.2f}', sorted(X)))


print(find_roots(float(input()), float(input()), float(input())))
```

### R. Территория зла
```python
def spell_out(edges: tuple[int]) -> str:
    edges = sorted(edges)

    largest = edges.pop(-1)

    cos = sum(map(lambda _: _ ** 2, edges)) - largest ** 2

    if cos == .0:
        return '100%'
    if cos < .0:
        return 'велика'
    return 'крайне мала'


NUMBER = 3

print(spell_out(tuple(map(int, [input() for _ in range(NUMBER)]))))
```

### S. Автоматизация безопасности
```python
def is_in_sea(x: float, y: float) -> bool:
    return x ** 2 + y ** 2 > 100


def is_in_danger_zone(x: float, y: float) -> bool:
    if y < 0:
        return y > ((1 + x) / 2) ** 2 - 9
    elif x < 0:
        return y < 5 * (7 + x) / 3 and y < 5
    else:
        return x ** 2 + y ** 2 < 25


def main(x: float, y: float) -> str:
    if is_in_sea(x, y):
        return 'Вы вышли в море и рискуете быть съеденным акулой!'
    if is_in_danger_zone(x, y):
        return 'Опасность! Покиньте зону как можно скорее!'
    return 'Зона безопасна. Продолжайте работу.'


if __name__ == '__main__':
    print(main(float(input()), float(input())))
```

### T. Зайка — 2
```python
result = min(
    filter(lambda _: 'зайка' in _.split(), [input(), input(), input()])
)
print(result, len(result))
```

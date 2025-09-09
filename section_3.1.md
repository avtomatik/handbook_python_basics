# 3. Коллекции и работа с памятью

## 3.1. Строки, кортежи, списки

### A. Азбука
```python
TARGET = 'абв'


def is_in_target(feed: list[str], target: str) -> bool:
    return set(map(lambda _: _[0].lower(), feed)) <= set(target)


feed = [input() for _ in range(int(input()))]

print('YES' if is_in_target(feed, TARGET) else 'NO')
```

### B. Кручу-верчу
```python
for _ in input():
    print(_)
```

### C. Анонс новости
```python
length = int(input())
feed = [input() for _ in range(int(input()))]


for line in feed:
    print(line if len(line) <= length else f'{line[:length - 3]}...')
```

### D. Очистка данных
```python
def custom_trim(line: str) -> str | None:
    if line.endswith('@@@'):
        return
    if line.startswith('##'):
        return line[2:]
    return line


while (line := input()):
    result = custom_trim(line)
    if result:
        print(result)
```

### E. А роза упала на лапу Азора 4.0
```python
def is_palindrome(feed: str) -> bool:
    return all(x == y for x, y in zip(feed[:len(feed) // 2], feed[len(feed) // 2:][::-1]))


print('YES' if is_palindrome(input()) else 'NO')
```

### F. Зайка — 6
```python
feeds = [input() for _ in range(int(input()))]


print(
    sum(
        sum(map(lambda _: 'зайка' in _, feed.split())) for feed in feeds
    )
)
```

### G. А и Б сидели на трубе
```python
print(sum(map(int, input().split())))
```

### H. Зайка — 7
```python
def detect_target(string: str, sub: str) -> None:
    try:
        print(1 + string.index(sub))
    except ValueError:
        print('Заек нет =(')


TARGET = 'зайка'


feed = [input() for _ in range(int(input()))]

for line in feed:
    detect_target(line, TARGET)
```

### I. Без комментариев
```python
while (line := input()):
    try:
        if line.index('#'):
            print(line.split('#')[0].rstrip())
    except ValueError:
        print(line)
```

### J. Частотный анализ на минималках
```python
counter = {}

while (line := input()) != 'ФИНИШ':
    for letter in line.lower().replace(' ', ''):
        counter[letter] = counter.get(letter, 0) + 1

print(max(counter, key=counter.get))
```

### K. Найдётся всё
```python
headers = [input() for _ in range(int(input()))]
qwery = input()


for header in headers:
    if qwery.lower() in header.lower():
        print(header)
```

### L. Меню питания
```python
PORRIDGES = [
    'Манная',
    'Гречневая',
    'Пшённая',
    'Овсяная',
    'Рисовая',
]

number = int(input())

for i in range(number):
    print(PORRIDGES[i % len(PORRIDGES)])
```

### M. Массовое возведение в степень
```python
numbers = [int(input()) for _ in range(int(input()))]
degree = int(input())

for number in numbers:
    print(number ** degree)
```

### N. Массовое возведение в степень 2.0
```python
numbers, degree = input(), int(input())

for number in map(int, numbers.split()):
    print(number ** degree, end=' ')
```

### O. НОД 3.0
```python
from itertools import combinations


def gcd(a: int, b: int) -> int:
    while b:
        a, b = b, a % b
    return a


print(min(map(lambda _: gcd(*_), combinations(map(int, input().split()), 2))))
```

### P. Анонс новости 2.0
```python
SPARE = 3

length = int(input())
feed = [input() for _ in range(int(input()))]

for line in feed:
    if len(line) + SPARE < length:
        print(line)
        length -= len(line)
    else:
        print(f"{line[:(length - SPARE)]}...")
        break
```

### Q. А роза упала на лапу Азора 5.0
```python
def is_palindrome(feed: str) -> bool:
    return all(x == y for x, y in zip(feed[:len(feed) // 2], feed[len(feed) // 2:][::-1]))


feed = ''.join(input().lower().split())


print('YES' if is_palindrome(feed) else 'NO')
```

### R. RLE
```python
feed = input()

current, count = feed[0], 1

for symbol in feed[1:]:
    if symbol == current:
        count += 1
    else:
        print(current, count)
        current, count = symbol, 1

print(current, count)
```

### S. Польский калькулятор
```python
OPERATIONS_BIN = '+-*'

stack = []

for token in input().split():
    if token in OPERATIONS_BIN:
        operand_r, operand_l = stack.pop(), stack.pop()
        stack.append(eval(f'{operand_l} {token} {operand_r}'))
    else:
        stack.append(int(token))

print(stack.pop())
```

### T. Польский калькулятор — 2
```python
import math


OPERATIONS_UNR = '~!#'
OPERATIONS_BIN = '+-*/'
OPERATIONS_TER = '@'


stack = []


for token in input().split():
    if token in OPERATIONS_UNR:
        operand = stack.pop()
        if token == '~':
            stack.append(-operand)
        elif token == '!':
            stack.append(math.factorial(operand))
        elif token == '#':
            stack.extend([operand, operand])
    elif token in OPERATIONS_BIN:
        if token == '/':
            token = '//'
        operand_r, operand_l = stack.pop(), stack.pop()
        stack.append(eval(f'{operand_l} {token} {operand_r}'))
    elif token in OPERATIONS_TER:
        operand_r, operand_m, operand_l = stack.pop(), stack.pop(), stack.pop()
        stack.extend([operand_m, operand_r, operand_l])
    else:
        stack.append(int(token))

print(stack.pop())
```

# 2. Базовые конструкции Python

## 2.3. Циклы

### A. Раз, два, три! Ёлочка, гори!
```python
while input() != "Три!":
    print("Режим ожидания...")
print("Ёлочка, гори!")
```

### B. Зайка — 3
```python
feeds = []
while (feed := input()) != "Приехали!":
    feeds.append(feed)

print(sum(map(lambda _: 'зайка' in _, feeds)))
```

### C. Считалочка
```python
print(' '.join(map(str, range(int(input()), 1 + int(input())))))
```

### D. Считалочка 2.0
```python
start, stop = int(input()), int(input())

step = 1 if start < stop else -1
stop += step

print(' '.join(map(str, range(start, stop, step))))
```

### E. Внимание! Акция!
```python
TRESHOLD = 500
DISCOUNT = .1

feeds = []
while (feed := float(input())) != .0:
    feeds.append(feed)

print(sum(map(lambda _: (1 - DISCOUNT) * _ if _ >= TRESHOLD else _, feeds)))
```

### F. НОД
```python
def gcd(a: int, b: int) -> int:
    while b:
        a, b = b, a % b
    return a


print(gcd(int(input()), int(input())))
```

### G. НОК
```python
def gcd(a: int, b: int) -> int:
    while b:
        a, b = b, a % b
    return a


def lcm(a: int, b: int) -> int:
    return int(a * b / gcd(a, b))


print(lcm(int(input()), int(input())))
```

### H. Излишняя автоматизация 2.0
```python
feed, times = input(), int(input())

for _ in range(times):
    print(feed)
```

### I. Факториал
```python
def factorial(n: int) -> int:
    if n == 0:
        return 1
    return n * factorial(n - 1)


print(factorial(int(input())))
```

### J. Маршрут построен
```python
DIRECTIONS = 'СЕВЕР ВОСТОК ЮГ ЗАПАД'.split()
DIRECTIONS_MAP = dict(zip(DIRECTIONS, [1, 1, -1, -1]))


feeds = []
while (feed := input()) != "СТОП":
    feeds.append(feed)


latitudes, longitudes = [], []
for direction, value in zip(feeds[::2], map(int, feeds[1::2])):
    if direction in DIRECTIONS[::2]:
        latitudes.append(value * DIRECTIONS_MAP[direction])
    else:
        longitudes.append(value * DIRECTIONS_MAP[direction])


print(sum(latitudes))
print(sum(longitudes))
```

### K. Цифровая сумма
```python
print(sum(map(int, input())))
```

### L. Сильная цифра
```python
print(max(map(int, input())))
```

### M. Первому игроку приготовиться 2.0
```python
print(min(input() for _ in range(int(input()))))
```

### N. Простая задача
```python
import math


def is_prime(number: int) -> bool:
    if number <= 1:
        return False

    for _ in range(2, 1 + int(math.sqrt(number))):
        if number % _ == 0:
            return False
    return True


print("YES" if is_prime(int(input())) else "NO")
```

### O. Зайка - 4
```python
print(sum(map(lambda _: 'зайка' in _, [input() for _ in range(int(input()))])))
```

### P. А роза упала на лапу Азора 2.0
```python
def is_palindrome(feed: str) -> bool:
    return all(x == y for x, y in zip(feed[:len(feed) // 2], feed[len(feed) // 2:][::-1]))


print('YES' if is_palindrome(input()) else 'NO')
```

### Q. Чётная чистота
```python
print(''.join(filter(lambda _: _ not in map(str, range(0, 10, 2)), input())))
```

### R. Простая задача 2.0
```python
import math


def is_prime(number: int) -> bool:
    if number <= 1:
        return False

    for _ in range(2, 1 + int(math.sqrt(number))):
        if number % _ == 0:
            return False
    return True


def get_primes(number: int):
    return filter(
        lambda _: is_prime(_),
        range(2, 1 + number)
    )


feed = int(input())


divisors = []
remainder = feed

for prime in get_primes(feed):
    if remainder % prime == 0:
        remainder /= prime
        divisors.append(prime)


factors = []
remainder = feed

for divisor in divisors:
    while remainder % divisor == 0:
        remainder /= divisor
        factors.append(divisor)

print(' * '.join(map(str, factors)))
```

### S. Игра в «Угадайку»
```python
min_val = 1
max_val = 1000

print((max_val + min_val) // 2)

answer = input()

while answer != 'Угадал!':
    if answer == 'Меньше':
        max_val = (max_val + min_val) // 2 - 1
    else:
        min_val = (max_val + min_val) // 2 + 1
    print((max_val + min_val) // 2)
    answer = input()
```

### T. Хайпанём немножечко!
```python
def get_m(number: int) -> int:
    return number // 2 ** 16


def get_r(number: int) -> int:
    return number // 2 ** 8 - number // 2 ** 16 * 2 ** 8


def get_hash(number: int, control: int) -> int:
    return 37 * (control + get_r(number) + get_m(number)) % 2 ** 8


def is_valid_hash(number: int) -> bool:
    return number < 100


def validate(numbers: list[int]) -> int:
    control = 0

    for _, number in enumerate(numbers):
        control = get_hash(number, control)
        if not is_valid_hash(control):
            return _

    else:
        return -1


if __name__ == '__main__':
    print(validate([int(input()) for _ in range(int(input()))]))
```

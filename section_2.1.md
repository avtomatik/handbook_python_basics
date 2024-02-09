# 2. Базовые конструкции Python

## 2.1. Ввод и вывод данных. Операции с числами, строками. Форматирование

### A. Привет, Яндекс!
```python
print('Привет, Яндекс!')
```

### B. Привет, всем!
```python
print(f'Привет, {input("Как Вас зовут?")}')
```

### C. Излишняя автоматизация
```python
string = input()
for _ in range(3):
    print(string)
```

### D. Сдача
```python
weight_kilo = 2.5
price_rub_per_kilo = 38
face_value = int(input())

change = face_value - weight_kilo * price_rub_per_kilo

print(int(change))
```

### E. Магазин
```python
price_rub_per_kilo = int(input())
weight_kilo = int(input())
face_value = int(input())

change = face_value - weight_kilo * price_rub_per_kilo

print(int(change))
```

### F. Чек
```python
product = input()
price_rub_per_kilo = int(input())
weight_kilo = int(input())
face_value = int(input())

change = face_value - weight_kilo * price_rub_per_kilo

print(
    f'''Чек
{product} - {weight_kilo}кг - {price_rub_per_kilo}руб/кг
Итого: {weight_kilo * price_rub_per_kilo}руб
Внесено: {face_value}руб
Сдача: {int(change)}руб'''
)
```

### G. Делу — время, потехе — час
```python
for _ in range(int(input())):
    print('Купи слона!')
```

### H. Наказание
```python
times, action = int(input()), input()

for _ in range(times):
    print(f'Я больше никогда не буду писать "{action}"!')
```

### I. Деловая колбаса
```python
minutes, children = int(input()), int(input())

print(children * minutes // 2)
```

### J. Детский сад — штаны на лямках
```python
name, locker_id = input(), input()

print(f'''Группа №{locker_id[0]}.
{locker_id[-1]}. {name}.
Шкафчик: {locker_id}.
Кроватка: {locker_id[1]}.''')
```

### K. Автоматизация игры
```python
number = int(input())

print(
    number // 100 % 10 * 1000 + number // 1000 *
    100 + number % 10 * 10 + number // 10 % 10
)
```

### L. Интересное сложение
```python
print(
    sum(
        10 ** (2 - _) * ((int(dig_l) + int(dig_r)) % 10)
        for _, (dig_l, dig_r) in enumerate(zip(f'{int(input()):03}', f'{int(input()):03}'))
    )
)
```

### M. Дед Мороз и конфеты
```python
children, candies = int(input()), int(input())

for number in divmod(candies, children):
    print(number)
```

### N. Шарики и ручки
```python
red, _, blue = int(input()), input(), int(input())

print(1 + red + blue)
```

### O. В ожидании доставки
```python
time = int(input()) * 60 + int(input()) + int(input())

print(f'{time // 60 % 24:02}:{time % 60:02}')
```

### P. Доставка
```python
subtrahend, minuend = int(input()), int(input())

print(f'{(minuend - subtrahend) / int(input()):.2f}')
```

### Q. Ошибка кассового аппарата
```python
print(sum((int(input()), int(input(), 2))))
```

### R. Сдача 10
```python
purchase, face_value = int(input(), 2), int(input())

print(face_value - purchase)
```

### S. Украшение чека
```python
product = input()
price_rub_per_kilo = int(input())
weight_kilo = int(input())
face_value = int(input())


WIDTH = 35


HEADERS = '''Товар:
Цена:
Итого:
Внесено:
Сдача:'''.split('\n')


STRINGS = (
    product,
    f'{weight_kilo}кг * {price_rub_per_kilo}руб/кг',
    f'{weight_kilo * price_rub_per_kilo:>26}руб',
    f'{face_value}руб',
    f'{face_value - weight_kilo * price_rub_per_kilo}руб'
)


print(f'{"Чек":=^{WIDTH}}')

for header, string in zip(HEADERS, STRINGS):
    print(f'{header}{string:>{WIDTH - len(header)}}')

print(f'{"":=^{WIDTH}}')
```

### T. Мухи отдельно, котлеты отдельно
```python
quantities_sum = int(input())
price_blended = int(input())
price_k_1 = int(input())
price_k_2 = int(input())

quantity = int(
    (price_blended - price_k_2) * quantities_sum / (price_k_1 - price_k_2)
)

print(quantity, quantities_sum - quantity)
```

# 3. Коллекции и работа с памятью

## 3.4. Встроенные возможности по работе с коллекциями

### A. Автоматизация списка
```python
for _, name in enumerate(input().split(), 1):
    print(f'{_}. {name}')
```

### B. Сборы на прогулку
```python
for left, right in zip(input().split(', '), input().split(', ')):
    print(f'{left} - {right}')
```

### C. Рациональная считалочка
```python
current, stop, step = map(float, input().split())

while current <= stop:
    print(f'{current:,.2f}')
    current += step
```

### D. Словарная ёлка
```python
from itertools import accumulate


feed = input().replace(' ', '? ')

for subsentence in accumulate(feed.split('?')):
    print(subsentence)
```

### E. Список покупок
```python
from itertools import chain


for _, item in enumerate(
    sorted(
        chain.from_iterable([input().split(', ') for _ in range(3)])
    ),
    start=1
):
    print(f'{_}. {item}')
```

### F. Колода карт
```python
from itertools import product


SUITS = [
    'пик',
    'треф',
    'бубен',
    'червей',
]

DECKS = list(map(str, range(2, 11))) + [
    'валет',
    'дама',
    'король',
    'туз',
]

SUITS.remove(input())

for _ in product(DECKS, SUITS):
    print(' '.join(_))
```

### G. Игровая сетка
```python
from itertools import product


SUITS = [
    'пик',
    'треф',
    'бубен',
    'червей',
]

DECKS = list(map(str, range(2, 11))) + [
    'валет',
    'дама',
    'король',
    'туз',
]

SUITS.remove(input())

for _ in product(DECKS, SUITS):
    print(' '.join(_))
```

### H. Меню питания 2.0
```python
porridges = [input() for _ in range(int(input()))]


number = int(input())

for i in range(number):
    print(porridges[i % len(porridges)])
```

### I. Таблица умножения 3.0
```python
from itertools import islice, product, starmap
from operator import mul


def batched(iterable, n):
    # batched('ABCDEFG', 3) --> ABC DEF G
    if n < 1:
        raise ValueError('n must be at least one')
    it = iter(iterable)
    while batch := tuple(islice(it, n)):
        yield batch


number = int(input())
for batch in batched(starmap(mul, product(range(1, 1 + number), repeat=2)), number):
    print(' '.join(map(str, batch)))
```

### J. Мы делили апельсин 2.0
```python
from itertools import product


number = int(input())

print(*list('АБВ'))

for pair in product(range(1, number - 1), repeat=2):
    rest = number - sum(pair)
    if rest > 0:
        print(*pair, rest)
```

### K. Числовой прямоугольник 3.0
```python
from itertools import islice


def batched(iterable, n):
    # batched('ABCDEFG', 3) --> ABC DEF G
    if n < 1:
        raise ValueError('n must be at least one')
    it = iter(iterable)
    while batch := tuple(islice(it, n)):
        yield batch


rows, cols = int(input()), int(input())

width = len(str(rows * cols))

for batch in batched(range(1, 1 + rows * cols), cols):
    print(' '.join(map(lambda _: f'{_:>{width}}', batch)))
```

### L. Список покупок 2.0
```python
from itertools import chain


for _, item in enumerate(
    sorted(
        chain.from_iterable([input().split(', ') for _ in range(int(input()))])
    ),
    start=1
):
    print(f'{_}. {item}')
```

### M. Расстановка спортсменов
```python
from itertools import permutations


competitors = [input() for _ in range(int(input()))]


for permutation in permutations(sorted(competitors)):
    print(', '.join(permutation))
```

### N. Спортивные гадания
```python
from itertools import permutations


competitors = [input() for _ in range(int(input()))]


for permutation in permutations(sorted(competitors), 3):
    print(', '.join(permutation))
```

### O. Список покупок 3.0
```python
from itertools import chain, permutations

items = chain.from_iterable(input().split(', ') for _ in range(int(input())))

for permutation in permutations(sorted(items), 3):
    print(' '.join(permutation))
```

### P. Расклад таков...
```python
from itertools import combinations, count, product

SUITS = {
    'пики': 'пик',
    'трефы': 'треф',
    'буби': 'бубен',
    'черви': 'червей',
}

DECKS = list(map(str, range(2, 11))) + [
    'валет',
    'дама',
    'король',
    'туз',
]

NUMBER_TO_DISPLAY = 10


suit_bound = SUITS.get(input())

DECKS.remove(input())

counter = count(1)

for deal in combinations(
    map(lambda _: ' '.join(_), product(sorted(DECKS), sorted(SUITS.values()))),
    3
):
    deal_string = ', '.join(deal)
    if suit_bound not in deal_string:
        continue
    if next(counter) > NUMBER_TO_DISPLAY:
        break
    print(deal_string)
```

### Q. А есть ещё варианты?
```python
from itertools import combinations, product

SUITS = {
    'пики': 'пик',
    'трефы': 'треф',
    'буби': 'бубен',
    'черви': 'червей',
}

DECKS = list(map(str, range(2, 11))) + [
    'валет',
    'дама',
    'король',
    'туз',
]


suit_bound = SUITS.get(input())

DECKS.remove(input())

deals = []

for deal in combinations(
    map(lambda _: ' '.join(_), product(sorted(DECKS), sorted(SUITS.values()))),
    3
):
    deal_string = ', '.join(deal)
    if suit_bound not in deal_string:
        continue
    deals.append(deal_string)


next_by_previous = dict(zip(deals, deals[1:]))

print(next_by_previous.get(input()))
```

### R. Таблица истинности
```python
from itertools import product

expression = input()

print('a b c f')

for triplet in product([0, 1], repeat=3):
    a, b, c = triplet
    print(*triplet, int(eval(expression)))
```

### S. Таблица истинности 2
```python
from itertools import product

expression = input()

variables = tuple(filter(str.isupper, sorted(set(expression))))

print(' '.join((*variables, 'F')))

for values in product([0, 1], repeat=len(tuple(variables))):
    print(
        *values,
        int(eval(expression, {'__builtins__': dict(zip(variables, values))}))
    )
```

### T. Таблицы истинности 3
```python
from itertools import product

OPERATIONS_UNR = {'not': 7}

OPERATIONS_BIN = {
    'and': 6,  # Conjunction
    'or': 5,   # Disjunction
    '^': 4,    # Exclusive Disjunction
    '->': 3,   # Implication
    '~': 2     # Equality
}

IS_LEFT_ASSOCIATIVE = {
    'not': False, 'and': True, 'or': True, '^': True, '->': True, '~': True
}

OPERATIONS = OPERATIONS_UNR | OPERATIONS_BIN

OPERATIONS_EXT = [*OPERATIONS_UNR, *OPERATIONS_BIN, '(', ')']

RANGE = [0, 1]


def parse(expression: str) -> str:
    """
    https://en.wikipedia.org/wiki/Shunting_yard_algorithm

    Parameters
    ----------
    expression : str.

    Returns
    -------
    str.

    """
    output_queue, operator_stack = [], []

    for token in expression.split():
        if token not in OPERATIONS_EXT:
            output_queue.append(token)
        elif token in OPERATIONS:
            if (operator_stack and operator_stack[0] != '(') and \
                (OPERATIONS.get(operator_stack[0]) > OPERATIONS.get(token) or
                 (OPERATIONS.get(operator_stack[0]) == OPERATIONS.get(token)
                  and IS_LEFT_ASSOCIATIVE.get(token))):
                output_queue.append(operator_stack.pop(0))
            operator_stack.insert(0, token)
        elif token == '(':
            operator_stack.insert(0, token)
        elif token == ')':
            if operator_stack[0] != '(':
                assert operator_stack
                output_queue.append(operator_stack.pop(0))
            assert operator_stack[0] == '('
            operator_stack.remove('(')

    assert output_queue[0] != '('
    output_queue.extend(operator_stack)

    return ' '.join(output_queue)


def evaluate(expression: str, scope: dict) -> int:
    output_queue = []

    for token in expression.split():
        if token in OPERATIONS_UNR:
            operand = output_queue.pop()
            if token == 'not':
                output_queue.append(
                    eval(f'not {operand}', scope)
                )
        elif token in OPERATIONS_BIN:
            operand_r, operand_l = output_queue.pop(), output_queue.pop()
            if token == '^':
                output_queue.append(
                    eval(f'sum(({operand_l}, {operand_r})) % 2', scope)
                )
            elif token == '->':
                output_queue.append(
                    eval(
                        f'0 if ({operand_l}, {operand_r})  == (1, 0) else 1',
                        scope
                    )
                )
            elif token == '~':
                output_queue.append(
                    eval(f'(1 + sum(({operand_l}, {operand_r}))) % 2', scope)
                )
            else:
                output_queue.append(
                    eval(f'{operand_l} {token} {operand_r}', scope)
                )
        else:
            output_queue.append(token)

    return output_queue.pop()


def main():
    expression = input().replace('(', '( ').replace(')', ' )')

    variables = tuple(filter(str.isupper, sorted(set(expression))))

    print(' '.join((*variables, 'F')))

    for values in product(RANGE, repeat=len(tuple(variables))):
        kwargs = dict(zip(variables, values))

        print(
            *values,
            int(evaluate(parse(expression), kwargs))
        )


if __name__ == '__main__':
    main()
```

# 3. Коллекции и работа с памятью

## 3.2. Множества, словари

### A. Символическая выжимка
```python
print(''.join(set(input())))
```

### B. Символическая разница
```python
print(''.join(set(input()) & set(input())))
```

### C. Зайка — 8
```python
entities = []

for _ in range(int(input())):
    entities.extend(input().split())

for entity in set(entities):
    print(entity)
```

### D. Кашееды
```python
n, m = int(input()), int(input())
students_n = [input() for _ in range(n)]
students_m = [input() for _ in range(m)]

students = set(students_n) & set(students_m)
if students:
    print(len(students))
else:
    print('Таких нет')
```

### E. Кашееды — 2
```python
students = [input() for _ in range(int(input()) + int(input()))]

students_single_cereal = set()

for student in students:
    if student in students_single_cereal:
        students_single_cereal.remove(student)
    else:
        students_single_cereal.add(student)


if students_single_cereal:
    print(len(students_single_cereal))
else:
    print('Таких нет')
```

### F. Кашееды — 3
```python
students = [input() for _ in range(int(input()) + int(input()))]

students_single_cereal = set()

for student in students:
    if student in students_single_cereal:
        students_single_cereal.remove(student)
    else:
        students_single_cereal.add(student)


if students_single_cereal:
    for student in sorted(students_single_cereal):
        print(student)
else:
    print('Таких нет')
```

### G. Азбука Морзе
```python
MAP = {
    'A': '.-', 'B': '-...', 'C': '-.-.',
    'D': '-..', 'E': '.', 'F': '..-.',
    'G': '--.', 'H': '....', 'I': '..',
    'J': '.---', 'K': '-.-', 'L': '.-..',
    'M': '--', 'N': '-.', 'O': '---',
    'P': '.--.', 'Q': '--.-', 'R': '.-.',
    'S': '...', 'T': '-', 'U': '..-',
    'V': '...-', 'W': '.--', 'X': '-..-',
    'Y': '-.--', 'Z': '--..',
    '0': '-----', '1': '.----', '2': '..---',
    '3': '...--', '4': '....-', '5': '.....',
    '6': '-....', '7': '--...', '8': '---..',
    '9': '----.'
}

feed = input()

for word in feed.split():
    print(' '.join(MAP.get(_) for _ in word.upper()))
```

### H. Кашееды — 4
```python
feeds = [input() for _ in range(int(input()))]
cereal = input()


preferences, cereals = {}, set()


for feed in feeds:
    slice_by = feed.find(' ')
    preference = feed[slice_by:].split()
    preferences[feed[:slice_by]] = preference
    cereals |= set(preference)


if cereal in cereals:
    for student, preference in dict(sorted(preferences.items())).items():
        if cereal in preference:
            print(student)
else:
    print('Таких нет')
```

### I. Зайка — 9
```python
from collections import Counter


counter = Counter()

while (feed := input()):
    counter.update(feed.split())

for key, value in counter.items():
    print(key, value)
```

### J. Транслитерация
```python
MAP = {
    'А': 'A',
    'Б': 'B',
    'В': 'V',
    'Г': 'G',
    'Д': 'D',
    'Е': 'E',
    'Ё': 'E',
    'Ж': 'ZH',
    'З': 'Z',
    'И': 'I',
    'Й': 'I',
    'К': 'K',
    'Л': 'L',
    'М': 'M',
    'Н': 'N',
    'О': 'O',
    'П': 'P',
    'Р': 'R',
    'С': 'S',
    'Т': 'T',
    'У': 'U',
    'Ф': 'F',
    'Х': 'KH',
    'Ц': 'TC',
    'Ч': 'CH',
    'Ш': 'SH',
    'Щ': 'SHCH',
    'Ъ': '',
    'Ы': 'Y',
    'Ь': '',
    'Э': 'E',
    'Ю': 'IU',
    'Я': 'IA',
}


def transliterate(letter: str, mapping: dict[str, str] = MAP) -> str:
    if letter.islower():
        return mapping.get(letter.upper(), letter).lower()
    if letter.isupper():
        return mapping.get(letter.upper(), letter).title()
    return letter


print(''.join(map(lambda _: transliterate(_), input())))
```

### K. Однофамильцы
```python
from collections import Counter


feed = [input() for _ in range(int(input()))]

print(sum(filter(lambda _: _ > 1, dict(Counter(feed)).values())))
```

### L. Однофамильцы — 2
```python
from collections import Counter


feed = [input() for _ in range(int(input()))]


namesakes = dict(filter(lambda _: _[-1] > 1, dict(Counter(feed)).items()))

namesakes = dict(sorted(namesakes.items()))

if namesakes:
    for name, occurences in namesakes.items():
        print(f'{name} - {occurences}')
else:
    print('Однофамильцев нет')
```

### M. Дайте чего-нибудь новенького!
```python
import itertools


meals_servable = [input() for _ in range(int(input()))]
meals_served = [
    [input() for _ in range(int(input()))] for i in range(int(input()))
]


meals_to_be_served = sorted(
    set(meals_servable) - set(itertools.chain(*meals_served))
)

if meals_to_be_served:
    for meal in meals_to_be_served:
        print(meal)
else:
    print('Готовить нечего')
```

### N. Это будет шедевр!
```python
food_items = [input() for _ in range(int(input()))]
recipes = {
    input(): [input() for _ in range(int(input()))] for i in range(int(input()))
}


meals_to_be_served = [
    meal for meal, ingredients in recipes.items() if set(ingredients) <= set(food_items)
]

if meals_to_be_served:
    for meal in sorted(meals_to_be_served):
        print(meal)
else:
    print('Готовить нечего')
```

### O. Двоичная статистика!
```python
import json
from collections import Counter


def get_representation(number: int) -> str:
    bins = dict(Counter(bin(number)[2:]))
    return {
        'digits': sum(bins.values()),
        'units': bins.get('1', 0),
        'zeros': bins.get('0', 0)
    }


feed = input()


with open('data.json', 'w', encoding='utf-8') as file_out:
    json.dump(
        list(map(get_representation, map(int, feed.split()))),
        file_out,
        ensure_ascii=False,
        indent=4
    )

with open('data.json') as file:
    for line in file.readlines():
        print(line, end='')
```

### P. Зайка — 10
```python
TARGET = 'зайка'

words_adjacent = []

while (feed := input()):
    words_in_line = feed.split()

    words_to_left, words_to_right = [], []

    for word_to_left, word in zip(words_in_line, words_in_line[1:]):
        if word == TARGET:
            words_to_left.append(word_to_left)
        if word_to_left == TARGET:
            words_to_right.append(word)

    words_adjacent.extend(words_to_left + words_to_right)


for word_adjacent in set(words_adjacent):
    print(word_adjacent)
```

### Q. Друзья друзей
```python
from itertools import chain


friends_first = {}

while (feed := input()):
    name, friend = feed.split()

    if name in friends_first:
        friends_first[name] += [friend]
    else:
        friends_first[name] = [friend]

    if friend in friends_first:
        friends_first[friend] += [name]
    else:
        friends_first[friend] = [name]


container_raw = {}

for name, friends in friends_first.items():
    for friend in friends:
        if name in container_raw:
            container_raw[name] += [friends_first[friend]]
        else:
            container_raw[name] = [friends_first[friend]]


friends_second = {}

for name in container_raw:
    friends = set(
        chain.from_iterable(container_raw[name])
    ) - set([name] + friends_first[name])
    friends_second[name] = sorted(friends)


friends_second = dict(sorted(friends_second.items()))

for name, friends in friends_second.items():
    print(f'{name}: {", ".join(friends)}')
```

### R. Карта сокровищ
```python
from collections import Counter


if __name__ == '__main__':
    feeds = [input() for _ in range(int(input()))]
    counter = Counter(
        tuple(map(lambda _: _ // 10, map(int, feed.split()))) for feed in feeds
    )
    print(counter.most_common(1)[-1][-1])
```

### S. Частная собственность
```python
from itertools import chain


common, container = set(), []

for _ in range(int(input())):
    _, toys = input().split(': ')
    toys_set = set(toys.split(', '))
    if common:
        common &= toys_set
    else:
        common.update(toys_set)
    container.append(toys_set)


toys_unique = sorted(
    chain.from_iterable(entry - common for entry in container)
)

for toy in toys_unique:
    print(toy)
```

### T. Простая задача 4.0
```python
from itertools import permutations


def gcd(a: int, b: int) -> int:
    while b:
        a, b = b, a % b
    return a


numbers = sorted(set(map(int, input().split('; '))))

coprimes = {}

for one, another in permutations(numbers, 2):
    if gcd(one, another) == 1:
        if one in coprimes:
            coprimes[one] += [another]
        else:
            coprimes[one] = [another]


for number, these_coprimes in coprimes.items():
    print(f'{number} - {", ".join(map(str, these_coprimes))}')
```

# 3. Коллекции и работа с памятью

## 3.5. Потоковый ввод/вывод. Работа с текстовыми файлами. JSON

### A. A+B+...
```python
from sys import stdin


print(sum(sum(map(int, _.split())) for _ in stdin))
```

### B. Средний рост
```python
from sys import stdin


def subtract(line: str) -> int:
    height_month_ago, height_now = map(int, line.split()[1:])
    return height_now - height_month_ago


heights = tuple(map(subtract, stdin))

print(round(sum(heights) / len(heights)))
```

### C. Без комментариев 2.0
```python
from sys import stdin


for line in stdin:
    try:
        if line.index('#'):
            print(line.split('#')[0].rstrip())
    except ValueError:
        print(line.rstrip())
```

### D. Найдётся всё 2.0
```python
from sys import stdin


headers = list(map(lambda _: _.rstrip(), stdin))

qwery = headers.pop()

for header in headers:
    if qwery.lower() in header.lower():
        print(header)
```

### E. А роза упала на лапу Азора 6.0
```python
from sys import stdin


def is_palindrome(feed: str) -> bool:
    feed = feed.lower()
    return all(
        x == y for x, y in zip(feed[:len(feed) // 2], feed[len(feed) // 2:][::-1])
    )


palindromes = sorted(
    set(
        word for line in stdin for word in line.rstrip().split() if is_palindrome(word)

    )
)

for palindrome in palindromes:
    print(palindrome)
```

### F. Транслитерация 2.0
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


with open('transliteration.txt', 'w', encoding='utf-8') as file_exp:
    with open('cyrillic.txt', encoding='utf-8') as file_src:
        for line in file_src.readlines():
            file_exp.write(
                ''.join(
                    map(lambda _: transliterate(_), line)
                )
            )
```

### G. Файловая статистика
```python
def get_numbers(file_name: str) -> list[int]:
    numbers = []

    with open(file_name) as file:
        for _ in file.readlines():
            numbers.extend(map(int, _.rstrip().split()))
        return numbers


def main():
    numbers = get_numbers(input())

    print(len(numbers))
    print(sum(number > 0 for number in numbers))
    print(min(numbers))
    print(max(numbers))
    print(sum(numbers))
    print(round(sum(numbers) / len(numbers), 2))


if __name__ == '__main__':
    main()
```

### H. Файловая разница
```python
NUMBER = 3

file_names = [input() for _ in range(NUMBER)]

file_name_exp = file_names.pop()

words_by_files = {}

for file_name in file_names:
    words = []

    with open(file_name) as file:
        for _ in file.readlines():
            words.extend(_.rstrip().split())

    words_by_files[file_name] = words

with open(file_name_exp, 'w') as file:
    for word in sorted(
        set(
            words_by_files[file_names[0]]
        ) ^ set(
            words_by_files[file_names[-1]]
        )
    ):
        print(word, file=file)
```

### I. Файловая чистка
```python
NUMBER = 2

file_name_src, file_name_exp = [input() for _ in range(NUMBER)]

with open(file_name_exp, 'w', encoding='utf-8') as file_exp:
    with open(file_name_src, encoding='utf-8') as file_src:
        for line in file_src.readlines():
            line_clean = line.rstrip()
            if line_clean:
                if '\t' in line_clean:
                    print(
                        ' '.join(line_clean.replace('\t', '').split()),
                        file=file_exp
                    )
                else:
                    print(' '.join(line_clean.split()), file=file_exp)
```

### J. Хвост
```python
file_name, number_tail = input(), int(input())


with open(file_name, 'rb') as file:
    number_lines = sum(map(bool, file))

with open(file_name, encoding='utf-8') as file:
    for _, line in enumerate(file.readlines(), 1):
        if _ > number_lines - number_tail:
            print(line.rstrip())
```

### K. Файловая статистика 2.0
```python
import json


def get_numbers(file_name: str) -> list[int]:
    numbers = []

    with open(file_name) as file:
        for _ in file.readlines():
            numbers.extend(map(int, _.rstrip().split()))
        return numbers


def get_number_struct(numbers: list[int]) -> tuple[int, float]:
    return (
        len(numbers),
        sum(number > 0 for number in numbers),
        min(numbers),
        max(numbers),
        sum(numbers),
        round(sum(numbers) / len(numbers), 2),
    )


def main():
    NUMBER = 2

    HEADERS = 'count positive_count min max sum average'

    file_name_src, file_name_exp = [input() for _ in range(NUMBER)]

    with open(file_name_exp, 'w', encoding='utf-8') as file_exp:
        json.dump(
            dict(
                zip(
                    HEADERS.split(),
                    get_number_struct(get_numbers(file_name_src))
                )
            ),
            file_exp,
            ensure_ascii=False,
            indent=4
        )


if __name__ == '__main__':
    main()
```

### L. Разделяй и властвуй
```python

from enum import Enum, auto


class Parity(Enum):

    EVEN = auto()
    ODD = auto()
    EQ = auto()


def classify(number: str) -> Parity:
    digits_even = sum(int(_) % 2 == 0 for _ in number)
    half_length = len(number) / 2
    if digits_even == half_length:
        return Parity.EQ
    if digits_even < half_length:
        return Parity.ODD
    return Parity.EVEN


NUMBER = 4

file_names = [input() for _ in range(NUMBER)]

file_name_src = file_names.pop(0)

for file_name, parity in zip(file_names, Parity):
    with open(file_name, 'w', encoding='utf-8') as file:
        with open(file_name_src, encoding='utf-8') as file_src:
            lines = [
                list(
                    filter(
                        lambda _: classify(_) == parity, line.rstrip().split()
                    )
                )
                for line in file_src.readlines()
            ]

        for line in lines:
            print(' '.join(line), file=file)
```

### M. Обновление данных
```python
import json
from sys import stdin


file_name = input()


with open(file_name, encoding='utf-8') as file:
    data = json.load(file)


with open(file_name, 'w', encoding='utf-8') as file:
    json.dump(
        data | dict(map(lambda _: _.rstrip().split(' == '), stdin)),
        file,
        ensure_ascii=False,
        indent=4
    )
```

### N. Слияние данных
```python
import json


file_name = input()


with open(file_name, encoding='utf-8') as file:
    data = {_.pop('name'): _ for _ in json.load(file)}


with open(input(), encoding='utf-8') as file:
    data_upd = {_.pop('name'): _ for _ in json.load(file)}


for name, attributes in data_upd.items():
    if name in data:
        for key, value in data_upd[name].items():
            if key in data[name]:
                data[name][key] = max(data[name][key], value)
            else:
                data[name][key] = value
    else:
        data[name] = attributes


with open(file_name, 'w', encoding='utf-8') as file:
    json.dump(data, file, ensure_ascii=False, indent=4)
```

### O. Поставь себя на моё место
```python
import json
from sys import stdin


FILE_NAME = 'scoring.json'

with open(FILE_NAME, encoding='utf-8') as file:

    scores_by_patterns = []

    for test_group in json.load(file):
        scores = test_group.pop('points')
        test_pairs = test_group.get('tests')
        for test_pair in test_pairs:
            scores_by_patterns.append(
                (test_pair.get('pattern'), scores // len(test_pairs))
            )


tests_success = list(
    filter(
        lambda _: _[0] == _[-1][0],
        zip(map(lambda _: _.rstrip(), stdin.readlines()), scores_by_patterns)
    )
)

print(sum(map(lambda _: _[-1][-1], tests_success)))
```

### P. Найдётся всё 3.0
```python
from sys import stdin


feed = list(map(lambda _: _.rstrip(), stdin))

qwery = feed.pop(0)


file_names = []

for file_name in feed:
    with open(file_name, encoding='utf-8') as file:
        if qwery.lower() in ' '.join(filter(bool, file.read().lower().split())):
            file_names.append(file_name)

if file_names:
    for file_name in file_names:
        print(file_name)
else:
    print('404. Not Found')
```

### Q. Прятки
```python
FILE_NAME = 'secret.txt'

with open(FILE_NAME, encoding='utf-8') as file:
    print(''.join(chr(ord(_) % 2 ** 8) for _ in file.read()))
```

### R. Сколько вешать в байтах?
```python
from math import ceil
from pathlib import Path


def get_repr(volume_bytes: int) -> str:
    if volume_bytes < 2 ** 0:
        print(f'{ceil(volume_bytes * 2 ** 3)}б')
    elif volume_bytes < 2 ** 10:
        print(f'{ceil(volume_bytes)}Б')
    elif volume_bytes < 2 ** 20:
        print(f'{ceil(volume_bytes / 2 ** 10)}КБ')
    elif volume_bytes < 2 ** 30:
        print(f'{ceil(volume_bytes / 2 ** 20)}МБ')
    else:
        print(f'{ceil(volume_bytes / 2 ** 30)}ГБ')


get_repr(Path(input()).stat().st_size)
```

### S. Это будет наш секрет
```python
def do_caesar_shift(symbol: str, shift: int) -> str:

    LOW_BOUND = 65

    COUNT = 26

    GAP = 6

    _LOW_BOUND = sum((LOW_BOUND, COUNT, GAP))

    if ord(symbol) - LOW_BOUND in range(COUNT):
        return chr(LOW_BOUND + (ord(symbol) - LOW_BOUND + shift) % COUNT)

    if ord(symbol) - _LOW_BOUND in range(COUNT):
        return chr(_LOW_BOUND + (ord(symbol) - _LOW_BOUND + shift) % COUNT)

    return symbol


file_name_src, file_name_exp = 'public.txt', 'private.txt'
shift = int(input())

with open(file_name_exp, 'w', encoding='utf-8') as file_exp:
    with open(file_name_src, encoding='utf-8') as file_src:
        print(
            ''.join(do_caesar_shift(_, shift) for _ in file_src.read()),
            file=file_exp
        )
```

### T. Файловая сумма
```python
FILE_NAME = 'numbers.num'

with open(FILE_NAME, 'rb') as file:
    numbers = []
    while True:
        chunk = file.read(2)
        if not chunk:
            break
        numbers.append(int.from_bytes(chunk, byteorder='big'))
    print(sum(numbers) % 2 ** 16)
```

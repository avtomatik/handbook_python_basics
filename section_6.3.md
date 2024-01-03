# 6. Библиотеки для получения и обработки данных

## 6.3. Модуль requests

### A. Проверка системы
```python
from requests import get


SCHEME = "http"

print(get(f'{SCHEME}://127.0.0.1:5000/').text)
```

### B. Суммирование ответов
```python
from requests import get


SCHEME = "http"

entries, feed = [], input()

while (entry := int(get(f'{SCHEME}://{feed}').text)) != 0:
    entries.append(entry)

print(sum(entries))
```

### C. Суммирование ответов 2
```python
from requests import get


SCHEME = "http"

print(
    sum(filter(lambda _: isinstance(_, int), get(f'{SCHEME}://{input()}').json()))
)
```

### D. Конкретное значение
```python
from requests import get


SCHEME = "http"

print(get(f'{SCHEME}://{input()}').json().get(input(), "No data"))
```

### E. Суммирование ответов 3
```python
from sys import stdin

from requests import get


SCHEME = "http"

feed = list(map(lambda _: _.rstrip('\n'), stdin))

host_and_port = feed.pop(0)

print(
    sum(sum(get(f'{SCHEME}://{host_and_port}{path}').json()) for path in feed)
)
```

### F. Список пользователей
```python
from requests import get


SCHEME = "http"

data = get(f'{SCHEME}://{input()}/users').json()

for user in sorted(f'{_["last_name"]} {_["first_name"]}' for _ in data):
    print(user)
```

### G. Рассылка сообщений
```python
from sys import stdin

from requests import get


SCHEME = "http"

response = get(f'{SCHEME}://{input()}/users/{input()}')

if response:
    print(stdin.read().format(**response.json()))
else:
    print("Пользователь не найден")
```

### H. Регистрация нового пользователя
```python
from json import dumps
from sys import stdin

from requests import post


SCHEME = "http"

HEADERS = "username last_name first_name email".split()


post(
    f'{SCHEME}://{input()}/users',
    data=dumps(dict(zip(HEADERS, stdin.read().split("\n"))))
)
```

### I. Изменение данных
```python
from json import dumps
from sys import stdin

from requests import put


SCHEME = "http"
SEP = "="


url = f'{SCHEME}://{input()}/users/{input()}'

patch = {}

for line in stdin:
    key, value = line.rstrip("\n").split(SEP)
    patch[key] = value


put(url, data=dumps(patch))
```

### J. Удаление данных
```python
from requests import delete


SCHEME = "http"


delete(f'{SCHEME}://{input()}/users/{input()}')
```

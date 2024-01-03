# 5. Объектно-ориентированное программирование

## 5.3. Модель исключений Python. Try, except, else, finally. Модули

### A. Обработка ошибок
```python
try:
    func()
    print("No Exceptions")
except Exception as exception:
    print(exception.__class__.__name__)
```

### B. Ломать — не строить
```python
try:
    func(True, None)
except Exception:
    print("Ура! Ошибка!")
```

### C. Ломать — не строить 2
```python
class Breaker:

    def __repr__(self):
        raise Exception


try:
    func(Breaker())
except Exception:
    print("Ура! Ошибка!")
```

### D. Контроль параметров
```python
def only_positive_even_sum(*args):
    if not any(map(lambda _: isinstance(_, int), args)):
        raise TypeError

    if not all(map(lambda _: _ > 0 and _ % 2 == 0, args)):
        raise ValueError

    return sum(args)
```

### E. Слияние с проверкой
```python
from collections.abc import Iterable


def merge_sort(iterable):
    if len(iterable) > 1:
        cut_at = len(iterable) // 2
        return merge(
            merge_sort(iterable[:cut_at]),
            merge_sort(iterable[cut_at:])
        )

    return iterable


def merge(left, right):

    if not all(isinstance(_, Iterable) for _ in (left, right)):
        raise StopIteration

    if len(set(map(type, [*left, *right]))) > 1:
        raise TypeError

    if not all(map(is_sorted, (left, right))):
        raise ValueError

    left, right, combined = list(left), list(right), list()

    while left and right:
        if left[0] < right[0]:
            combined.append(left.pop(0))
        else:
            combined.append(right.pop(0))

    if left:
        combined.extend(left)
    else:
        combined.extend(right)

    return combined


def is_sorted(iterable):
    return not any(x > y for x, y in zip(iterable, iterable[1:]))
```

### F. Корень зла 2
```python
import math


class NoSolutionsError(ArithmeticError):
    ...


class InfiniteSolutionsError(ArithmeticError):
    ...


def find_roots(a: float, b: float, c: float) -> str:

    if not all(isinstance(_, (int, float)) for _ in (a, b, c)):
        raise TypeError

    if a == .0 and b == .0 and c == .0:
        raise InfiniteSolutionsError

    elif a == .0 and b != .0:
        X = [-c / b]

    elif a == .0:
        raise NoSolutionsError

    else:
        d = b ** 2 - 4 * a * c

        if d < .0:
            raise NoSolutionsError
        elif d == .0:
            X = [-b / (2 * a), -b / (2 * a)]
        else:
            X = [-(b + math.sqrt(d)) / (2 * a), (-b + math.sqrt(d)) / (2 * a)]

    return tuple(sorted(X))
```

### G. Валидация имени
```python
class CyrillicError(ValueError):
    ...


class CapitalError(ValueError):
    ...


def name_validation(first_or_last_name):
    if not isinstance(first_or_last_name, str):
        raise TypeError

    RANGE = (*range(1025, 1026), *range(1040, 1072))

    if not all(ord(_) in RANGE for _ in first_or_last_name.upper()):
        raise CyrillicError

    if not first_or_last_name.istitle():
        raise CapitalError

    return first_or_last_name
```

### H. Валидация имени пользователя
```python
class BadCharacterError(ValueError):
    ...


class StartsWithDigitError(ValueError):
    ...


def username_validation(username):
    if not isinstance(username, str):
        raise TypeError

    RANGE = (*range(48, 58), *range(65, 91), *range(95, 96))

    if not all(ord(_) in RANGE for _ in username.upper()):
        raise BadCharacterError

    if username.startswith(tuple(map(str, range(10)))):
        raise StartsWithDigitError

    return username
```

### I. Валидация пользователя
```python
class CyrillicError(ValueError):
    ...


class CapitalError(ValueError):
    ...


class BadCharacterError(ValueError):
    ...


class StartsWithDigitError(ValueError):
    ...


def name_validation(first_or_last_name):
    if not isinstance(first_or_last_name, str):
        raise TypeError

    RANGE = (*range(1025, 1026), *range(1040, 1072))

    if not all(ord(_) in RANGE for _ in first_or_last_name.upper()):
        raise CyrillicError

    if not first_or_last_name.istitle():
        raise CapitalError

    return first_or_last_name


def username_validation(username):
    if not isinstance(username, str):
        raise TypeError

    RANGE = (*range(48, 58), *range(65, 91), *range(95, 96))

    if not all(ord(_) in RANGE for _ in username.upper()):
        raise BadCharacterError

    if username.startswith(tuple(map(str, range(10)))):
        raise StartsWithDigitError

    return username


def user_validation(**kwargs):
    if set(locals()["kwargs"].keys()) != {"last_name", "first_name", "username"}:
        raise KeyError

    if not all(isinstance(_, str) for _ in locals()["kwargs"].values()):
        raise TypeError

    name_validation(locals()["kwargs"]["last_name"])
    name_validation(locals()["kwargs"]["first_name"])
    username_validation(locals()["kwargs"]["username"])

    return locals()["kwargs"]
```

### J. Валидация пароля
```python
from hashlib import sha256
from string import ascii_letters, digits


class MinLengthError(ValueError):
    ...


class PossibleCharError(ValueError):
    ...


class NeedCharError(ValueError):
    ...


def password_validation(
    password,
    min_length=8,
    possible_chars=ascii_letters + digits,
    at_least_one=str.isdigit
):
    if not isinstance(password, str):
        raise TypeError

    if len(password) < min_length:
        raise MinLengthError

    if set(password) - set(possible_chars):
        raise PossibleCharError

    if not any(map(at_least_one, password)):
        raise NeedCharError

    return sha256(password.encode()).hexdigest()
```

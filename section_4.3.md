# 4. Функции и их особенности в Python

## 4.3. Рекурсия. Декораторы. Генераторы

### A. Рекурсивный сумматор
```python
def recursive_sum(*numbers: tuple[int]) -> int:
    if numbers:
        *numbers, last = numbers
        return sum((last, recursive_sum(*numbers)))
    return 0
```

### B. Рекурсивный сумматор цифр
```python
def recursive_digit_sum(number: int) -> int:
    if number:
        number, last = divmod(number, 10)
        return sum((last, recursive_digit_sum(number)))
    return 0
```

### C. Многочлен N-ой степени
```python
def make_equation(*numbers: tuple[int]) -> str:
    if len(numbers) == 1:
        return f"{numbers[-1]}"
    if numbers:
        return f"({make_equation(*numbers[:-1])}) * x + {numbers[-1]}"
```

### D. Декор результата
```python
def answer(func):
    def decorated(*args, **kwargs):
        return f"Результат функции: {func(*args, **kwargs)}"
    return decorated
```

### E. Накопление результата
```python
def result_accumulator(func, method="accumulate"):

    stack = []

    def decorated(*args, method=method, **kwargs):

        nonlocal stack

        stack.append(func(*args, **kwargs))

        if method == "drop":
            final, stack = stack[:], []
            return final

    return decorated
```

### F. Сортировка слиянием
```python
def merge(left: list[int], right: list[int]) -> list[int]:

    combined = []

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


def merge_sort(numbers: list[int]) -> list[int]:
    if len(numbers) > 1:
        cut_at = len(numbers) // 2
        return merge(
            merge_sort(numbers[:cut_at]),
            merge_sort(numbers[cut_at:])
        )

    return numbers
```

### G. Однотипность не порок
```python
def same_type(func):

    def decorated(*args):
        if len(set(map(type, args))) > 1:
            print("Обнаружены различные типы данных")
            return False
        return func(*args)

    return decorated
```

### H. Генератор Фибоначчи
```python
def fibonacci(number: int):
    n_left, n_right = 0, 1
    for _ in range(number):
        yield n_left
        n_left, n_right = n_right, n_left + n_right
```

### I. Циклический генератор
```python
def cycle(iterable: list):
    while True:
        for element in iterable:
            yield element
```

### J. "Выпрямление" списка
```python
def make_linear(iterable):

    linear = []

    for element in iterable:
        if isinstance(element, list):
            linear.extend(make_linear(element))
        else:
            linear.append(element)

    return linear
```

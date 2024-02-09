# 6. Библиотеки для получения и обработки данных

## 6.1. Модули math и numpy

### A. Математика — круто, но это не точно
```python
from math import cos, e, log2, pi, sin


x = float(input())

print(log2(x ** (3 / 16)) / 5 + x ** (cos(pi * x / (2 * e))) - sin(x / pi) ** 2)
```

### B. Потоковый НОД
```python
from math import gcd
from sys import stdin

for _ in stdin:
    print(gcd(*tuple(map(int, _.split()))))
```

### C. Есть варианты?
```python
from math import comb

n, k = map(int, input().split())

print(comb(n - 1, k - 1), comb(n, k))
```

### D. Среднее не арифметическое
```python
from functools import reduce
from operator import mul

feed = tuple(map(float, input().split()))

print(pow(reduce(mul, feed), 1 / len(feed)))
```

### E. Шаг навстречу
```python
from math import cos, dist, sin

start = tuple(map(float, input().split()))
r, phi = tuple(map(float, input().split()))

print(dist((r * cos(phi), r * sin(phi)), start))
```

### F. Матрица умножения
```python
import numpy as np


def multiplication_matrix(number: int) -> np.ndarray:
    return np.arange(1, 1 + number) * np.arange(1, 1 + number).reshape(-1, 1)
```

### G. Шахматная подготовка
```python
import numpy as np


def make_board(number: int) -> np.ndarray:
    return np.array(
        [
            [(col + row - 1) % 2 for col in range(1, 1 + number)]
            for row in range(1, 1 + number)
        ],
        dtype='int8'
    )
```

### H. Числовая змейка 3.0
```python
import numpy as np


def snake(cols: int, rows: int, direction: str = 'H') -> np.ndarray:
    # =========================================================================
    # TODO: Refactor with DRY
    # =========================================================================
    if direction == 'H':
        return np.array(
            [
                [get_elem(col, cols, row) for col in range(cols)]
                for row in range(rows)
            ],
            dtype='int16'
        )

    if direction == 'V':
        return np.array(
            [
                [get_elem(row, rows, col) for col in range(cols)]
                for row in range(rows)
            ],
            dtype='int16'
        )


def get_elem(unit: int, total: int, orthogonal: int) -> int:
    return orthogonal * total + (
        1 + unit if orthogonal % 2 == 0 else total - unit
    )
```

### I. Вращение
```python
import numpy as np


def rotate(array: np.ndarray, angle: int) -> np.ndarray:
    if angle % 360 == 0:
        return array
    if angle % 360 == 90:
        return np.flip(array.transpose(), 1)
    if angle % 360 == 180:
        return np.flip(array)
    if angle % 360 == 270:
        return np.flip(array, 1).transpose()
```

### J. Лесенка
```python
import numpy as np


def stairs(vector: np.ndarray) -> np.ndarray:
    return np.array([np.roll(vector, _) for _ in range(len(vector))])
```

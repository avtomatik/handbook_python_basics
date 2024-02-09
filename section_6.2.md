# 6. Библиотеки для получения и обработки данных

## 6.2. Модуль pandas

### A. Длины всех слов - 2
```python
from string import digits, punctuation

import pandas as pd


def length_stats(sentence, possible_chars=punctuation + digits):
    words = sentence.lower().translate(
        str.maketrans('', '', possible_chars)
    ).split()
    words_dict = {_.lower(): len(_) for _ in sorted(words)}
    return pd.Series(data=words_dict, index=words_dict.keys())
```

### B. Длины всех слов по чётности
```python
from string import digits, punctuation

import pandas as pd


def length_stats(sentence, possible_chars=punctuation + digits):
    words = sentence.lower().translate(
        str.maketrans('', '', possible_chars)
    ).split()
    words_dict_odd, words_dict_even = dict(), dict()
    for _ in sorted(words):
        if len(_) % 2 == 0:
            words_dict_even[_.lower()] = len(_)
        else:
            words_dict_odd[_.lower()] = len(_)

    return (
        pd.Series(
            data=words_dict_odd,
            index=words_dict_odd.keys(),
            dtype='int64'
        ),
        pd.Series(
            data=words_dict_even,
            index=words_dict_even.keys(),
            dtype='int64'
        )
    )
```

### C. Чек - 2
```python
import pandas as pd


def cheque(price_list: pd.Series, **kwargs: dict[str, int]) -> pd.DataFrame:
    price_list.name = 'price'
    df = pd.merge(
        price_list,
        pd.Series(kwargs, name='number'),
        left_index=True,
        right_index=True
    )
    df['cost'] = df['price'].mul(df['number'])
    return df.sort_index().rename_axis('product').reset_index()
```

### D. Акция
```python
import pandas as pd


def cheque(price_list: pd.Series, **kwargs: dict[str, int]) -> pd.DataFrame:
    price_list.name = 'price'
    df = pd.merge(
        price_list,
        pd.Series(kwargs, name='number'),
        left_index=True,
        right_index=True
    )
    df['cost'] = df['price'].mul(df['number'])
    return df.sort_index().rename_axis('product').reset_index()


def discount_cost(df):
    if df['number'] > 2:
        return df['cost'] * .5
    else:
        return df['cost']


def discount(df: pd.DataFrame) -> pd.DataFrame:
    df = df.copy()
    df['cost'] = df.apply(discount_cost, axis=1)
    return df
```

### E. Длинные слова
```python
import pandas as pd


def get_long(series: pd.Series, min_length: int = 5) -> pd.Series:
    return series[series >= min_length]
```

### F. Отчёт успеваемости
```python
import pandas as pd


def best(df: pd.DataFrame, treshold: int = 3) -> pd.DataFrame:
    return df[(df.iloc[:, 1:] > treshold).all(axis=1)]
```

### G. Отчёт неуспеваемости
```python
import pandas as pd


def need_to_work_better(df: pd.DataFrame, target: int = 2) -> pd.DataFrame:
    return df[(df.iloc[:, 1:] == target).any(axis=1)]
```

### H. Обновление журнала
```python
import pandas as pd


def update(df: pd.DataFrame) -> pd.DataFrame:
    df = df.copy()
    df['average'] = df.iloc[:, 1:].mean(axis=1)
    return df.sort_values(by=['average', 'name'], ascending=[False, True])
```

### I. Бесконечный морской бой
```python
import pandas as pd


filepath_or_buffer = 'data.csv'

df = pd.read_csv(filepath_or_buffer)

coordinates = tuple(map(int, ' '.join((input(), input())).split()))

print(
    df[
        df['x'].between(
            *sorted(coordinates[::2])
        ) & df['y'].between(
            *sorted(coordinates[1::2])
        )
    ]
)
```

### J. Экстремум функции
```python
import numpy as np
import pandas as pd


def values(func, start, end, step):
    end += step
    index = np.arange(start, end, step)
    return pd.Series(data=func(index), index=index)


def min_extremum(series):
    return series.idxmin()


def max_extremum(series):
    return series.idxmax()
```

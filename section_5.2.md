# 5. Объектно-ориентированное программирование

## 5.2. Волшебные методы, переопределение методов. Наследование

### A. Классная точка 3.0
```python
class Point:

    def __init__(self, x: int, y: int):
        self.x = x
        self.y = y

    def move(self, x: int, y: int):
        self.x += x
        self.y += y

    def length(self, other) -> float:
        return round(
            (
                sum(
                    map(lambda _: _ ** 2, (self.x - other.x, self.y - other.y))
                )
            ) ** .5,
            2
        )


class PatchedPoint(Point):

    def __init__(self, *args):
        if not args:
            super().__init__(0, 0)

        elif len(args) < 2:
            args, *rest = args
            super().__init__(*args)

        else:
            super().__init__(*args)
```

### B. Классная точка 4.0
```python
class Point:

    def __init__(self, x: int, y: int):
        self.x = x
        self.y = y

    def move(self, x: int, y: int):
        self.x += x
        self.y += y

    def length(self, other) -> float:
        return round(
            (
                sum(
                    map(lambda _: _ ** 2, (self.x - other.x, self.y - other.y))
                )
            ) ** .5,
            2
        )


class PatchedPoint(Point):

    def __init__(self, *args):
        if not args:
            super().__init__(0, 0)

        elif len(args) < 2:
            args, *rest = args
            super().__init__(*args)

        else:
            super().__init__(*args)

    def __str__(self):
        return f"({self.x}, {self.y})"

    def __repr__(self):
        return f"PatchedPoint{self.__str__()}"
```

### C. Классная точка 5.0
```python
class Point:

    def __init__(self, x: int, y: int):
        self.x = x
        self.y = y

    def move(self, x: int, y: int):
        self.x += x
        self.y += y

    def length(self, other) -> float:
        return round(
            (
                sum(
                    map(lambda _: _ ** 2, (self.x - other.x, self.y - other.y))
                )
            ) ** .5,
            2
        )


class PatchedPoint(Point):

    def __init__(self, *args):
        if not args:
            super().__init__(0, 0)

        elif len(args) < 2:
            args, *rest = args
            super().__init__(*args)

        else:
            super().__init__(*args)

    def __str__(self):
        return f"({self.x}, {self.y})"

    def __repr__(self):
        return f"PatchedPoint{self.__str__()}"

    def __add__(self, other):
        x, y = other
        return PatchedPoint(self.x + x, self.y + y)

    def __iadd__(self, other):
        self.move(*other)
        return self
```

### D. Дроби v0.1
```python
class Fraction:

    def __init__(self, *args):
        if len(args) < 2:
            args, *rest = args
            gcd = self._gcd(*self._parse_str(args))
            self.dividend, self.divisor = map(
                lambda _: _ // gcd, self._parse_str(args)
            )

        else:
            gcd = self._gcd(*args)
            self.dividend, self.divisor = map(lambda _: _ // gcd, args)

    def _gcd(self, a: int, b: int) -> int:
        while b:
            a, b = b, a % b
        return a

    def _parse_str(self, args: str):
        return map(int, args.split("/"))

    def numerator(self, number=None):
        if not number:
            return self.dividend
        self.__init__(number, self.divisor)

    def denominator(self, number=None):
        if not number:
            return self.divisor
        self.__init__(self.dividend, number)

    def __str__(self):
        return f"{self.dividend}/{self.divisor}"

    def __repr__(self):
        return f"Fraction({self.dividend}, {self.divisor})"
```

### E. Дроби v0.2
```python
class Fraction:

    def __init__(self, *args):
        if len(args) < 2:
            args, *rest = args
            self.dividend, self.divisor = map(
                lambda _: _ // self._gcd(*self._parse(args)), self._parse(args)
            )

        else:
            self.dividend, self.divisor = map(
                lambda _: _ // self._gcd(*args), args
            )

    def _gcd(self, a: int, b: int) -> int:
        while b:
            a, b = b, a % b
        return a

    def _parse(self, args: str):
        return map(int, args.split("/"))

    def numerator(self, number=None):
        if not number:
            return abs(self.dividend)
        self.__init__(number if self.dividend > 0 else -number, self.divisor)

    def denominator(self, number=None):
        if not number:
            return self.divisor
        self.__init__(self.dividend, number)

    def __str__(self):
        return f"{self.dividend}/{self.divisor}"

    def __repr__(self):
        return f"Fraction('{str(self)}')"

    def __neg__(self):
        return Fraction(-self.dividend, self.divisor)
```

### F. Дроби v0.3
```python
class Fraction:

    def __init__(self, *args):
        if len(args) < 2:
            args, *rest = args
            self.dividend, self.divisor = map(
                lambda _: _ // self._gcd(*self._parse(args)), self._parse(args)
            )

        else:
            self.dividend, self.divisor = map(
                lambda _: _ // self._gcd(*args), args
            )

    def _gcd(self, a: int, b: int) -> int:
        while b:
            a, b = b, a % b
        return a

    def _parse(self, args: str):
        return map(int, args.split("/"))

    def numerator(self, number=None):
        if not number:
            return abs(self.dividend)
        self.__init__(number if self.dividend > 0 else -number, self.divisor)

    def denominator(self, number=None):
        if not number:
            return self.divisor
        self.__init__(self.dividend, number)

    def __str__(self):
        return f"{self.dividend}/{self.divisor}"

    def __repr__(self):
        return f"Fraction('{str(self)}')"

    def __neg__(self):
        return Fraction(-self.dividend, self.divisor)

    def __add__(self, other):
        return Fraction(
            self.dividend * other.divisor + self.divisor * other.dividend,
            self.divisor * other.divisor
        )

    def __sub__(self, other):
        return Fraction(
            self.dividend * other.divisor - self.divisor * other.dividend,
            self.divisor * other.divisor
        )

    def __iadd__(self, other):
        self.__init__(
            self.dividend * other.divisor + self.divisor * other.dividend,
            self.divisor * other.divisor
        )
        return self

    def __isub__(self, other):
        self.__init__(
            self.dividend * other.divisor - self.divisor * other.dividend,
            self.divisor * other.divisor
        )
        return self
```

### G. Дроби v0.4
```python
class Fraction:

    def __init__(self, *args):
        if len(args) < 2:
            args, *rest = args
            self.dividend, self.divisor = map(
                lambda _: _ // self._gcd(*self._parse(args)), self._parse(args)
            )

        else:
            self.dividend, self.divisor = map(
                lambda _: _ // self._gcd(*args), args
            )

    def _gcd(self, a: int, b: int) -> int:
        while b:
            a, b = b, a % b
        return a

    def _parse(self, args: str):
        return map(int, args.split("/"))

    def numerator(self, number=None):
        if not number:
            return abs(self.dividend)
        self.__init__(number if self.dividend > 0 else -number, self.divisor)

    def denominator(self, number=None):
        if not number:
            return self.divisor
        self.__init__(self.dividend, number)

    def __str__(self):
        return f"{self.dividend}/{self.divisor}"

    def __repr__(self):
        return f"Fraction('{str(self)}')"

    def __neg__(self):
        return Fraction(-self.dividend, self.divisor)

    def __add__(self, other):
        return Fraction(
            self.dividend * other.divisor + self.divisor * other.dividend,
            self.divisor * other.divisor
        )

    def __sub__(self, other):
        return Fraction(
            self.dividend * other.divisor - self.divisor * other.dividend,
            self.divisor * other.divisor
        )

    def __iadd__(self, other):
        self.__init__(
            self.dividend * other.divisor + self.divisor * other.dividend,
            self.divisor * other.divisor
        )
        return self

    def __isub__(self, other):
        self.__init__(
            self.dividend * other.divisor - self.divisor * other.dividend,
            self.divisor * other.divisor
        )
        return self

    def __mul__(self, other):
        return Fraction(self.dividend * other.dividend, self.divisor * other.divisor)

    def __truediv__(self, other):
        return Fraction(self.dividend * other.divisor, self.divisor * other.dividend)

    def __imul__(self, other):
        self.__init__(
            self.dividend * other.dividend, self.divisor * other.divisor
        )
        return self

    def __itruediv__(self, other):
        self.__init__(
            self.dividend * other.divisor, self.divisor * other.dividend
        )
        return self

    def reverse(self):
        self.__init__(self.divisor, self.dividend)
        return self
```

### H. Дроби v0.5
```python
class Fraction:

    def __init__(self, *args):
        if len(args) < 2:
            args, *rest = args
            self.dividend, self.divisor = map(
                lambda _: _ // self._gcd(*self._parse(args)), self._parse(args)
            )

        else:
            self.dividend, self.divisor = map(
                lambda _: _ // self._gcd(*args), args
            )

    def _gcd(self, a: int, b: int) -> int:
        while b:
            a, b = b, a % b
        return a

    def _parse(self, args: str):
        return map(int, args.split("/"))

    def numerator(self, number=None):
        if not number:
            return abs(self.dividend)
        self.__init__(number if self.dividend > 0 else -number, self.divisor)

    def denominator(self, number=None):
        if not number:
            return self.divisor
        self.__init__(self.dividend, number)

    def __str__(self):
        return f"{self.dividend}/{self.divisor}"

    def __repr__(self):
        return f"Fraction('{str(self)}')"

    def __neg__(self):
        return Fraction(-self.dividend, self.divisor)

    def __add__(self, other):
        return Fraction(
            self.dividend * other.divisor + self.divisor * other.dividend,
            self.divisor * other.divisor
        )

    def __sub__(self, other):
        return Fraction(
            self.dividend * other.divisor - self.divisor * other.dividend,
            self.divisor * other.divisor
        )

    def __iadd__(self, other):
        self.__init__(
            self.dividend * other.divisor + self.divisor * other.dividend,
            self.divisor * other.divisor
        )
        return self

    def __isub__(self, other):
        self.__init__(
            self.dividend * other.divisor - self.divisor * other.dividend,
            self.divisor * other.divisor
        )
        return self

    def __mul__(self, other):
        return Fraction(self.dividend * other.dividend, self.divisor * other.divisor)

    def __truediv__(self, other):
        return Fraction(self.dividend * other.divisor, self.divisor * other.dividend)

    def __imul__(self, other):
        self.__init__(
            self.dividend * other.dividend, self.divisor * other.divisor
        )
        return self

    def __itruediv__(self, other):
        self.__init__(
            self.dividend * other.divisor, self.divisor * other.dividend
        )
        return self

    def reverse(self):
        self.__init__(self.divisor, self.dividend)
        return self

    def __lt__(self, other):
        return self.dividend * other.divisor < self.divisor * other.dividend

    def __le__(self, other):
        return self.dividend * other.divisor <= self.divisor * other.dividend

    def __eq__(self, other):
        return self.dividend * other.divisor == self.divisor * other.dividend

    def __ne__(self, other):
        return self.dividend * other.divisor != self.divisor * other.dividend

    def __gt__(self, other):
        return self.dividend * other.divisor > self.divisor * other.dividend

    def __ge__(self, other):
        return self.dividend * other.divisor >= self.divisor * other.dividend
```

### I. Дроби v0.6
```python
class Fraction:

    def __init__(self, *args):
        if len(args) < 2:

            SEP = "/"

            args, *rest = args

            if isinstance(args, int):
                self.dividend, self.divisor = args, 1
            elif isinstance(args, str):
                if SEP in args:
                    self.dividend, self.divisor = map(
                        lambda _: _ // self._gcd(*self._parse(args)),
                        self._parse(args)
                    )
                else:
                    self.dividend, self.divisor = int(args), 1

        else:
            self.dividend, self.divisor = map(
                lambda _: _ // self._gcd(*args), args
            )

    def _gcd(self, a: int, b: int) -> int:
        while b:
            a, b = b, a % b
        return a

    def _parse(self, args: str):
        SEP = "/"
        return map(int, args.split(SEP))

    def numerator(self, number=None):
        if not number:
            return abs(self.dividend)
        self.__init__(number if self.dividend > 0 else -number, self.divisor)

    def denominator(self, number=None):
        if not number:
            return self.divisor
        self.__init__(self.dividend, number)

    def __str__(self):
        return f"{self.dividend}/{self.divisor}"

    def __repr__(self):
        return f"Fraction('{str(self)}')"

    def __neg__(self):
        return Fraction(-self.dividend, self.divisor)

    def __add__(self, other):
        if isinstance(other, Fraction):
            return Fraction(
                self.dividend * other.divisor + self.divisor * other.dividend,
                self.divisor * other.divisor
            )
        return Fraction(self.dividend + self.divisor * other, self.divisor)

    def __sub__(self, other):
        if isinstance(other, Fraction):
            return Fraction(
                self.dividend * other.divisor - self.divisor * other.dividend,
                self.divisor * other.divisor
            )
        return Fraction(self.dividend - self.divisor * other, self.divisor)

    def __iadd__(self, other):
        self.__init__(
            self.dividend * other.divisor + self.divisor * other.dividend,
            self.divisor * other.divisor
        )
        return self

    def __isub__(self, other):
        self.__init__(
            self.dividend * other.divisor - self.divisor * other.dividend,
            self.divisor * other.divisor
        )
        return self

    def __mul__(self, other):
        return Fraction(self.dividend * other.dividend, self.divisor * other.divisor)

    def __truediv__(self, other):
        return Fraction(self.dividend * other.divisor, self.divisor * other.dividend)

    def __imul__(self, other):
        self.__init__(
            self.dividend * other.dividend, self.divisor * other.divisor
        )
        return self

    def __itruediv__(self, other):
        self.__init__(
            self.dividend * other.divisor, self.divisor * other.dividend
        )
        return self

    def reverse(self):
        self.__init__(self.divisor, self.dividend)
        return self

    def __lt__(self, other):
        if isinstance(other, Fraction):
            return self.dividend * other.divisor < self.divisor * other.dividend
        return self.dividend < self.divisor * other

    def __le__(self, other):
        if isinstance(other, Fraction):
            return self.dividend * other.divisor <= self.divisor * other.dividend
        return self.dividend <= self.divisor * other

    def __eq__(self, other):
        if isinstance(other, Fraction):
            return self.dividend * other.divisor == self.divisor * other.dividend
        return self.dividend == self.divisor * other

    def __ne__(self, other):
        if isinstance(other, Fraction):
            return self.dividend * other.divisor != self.divisor * other.dividend
        return self.dividend != self.divisor * other

    def __gt__(self, other):
        if isinstance(other, Fraction):
            return self.dividend * other.divisor > self.divisor * other.dividend
        return self.dividend > self.divisor * other

    def __ge__(self, other):
        if isinstance(other, Fraction):
            return self.dividend * other.divisor >= self.divisor * other.dividend
        return self.dividend >= self.divisor * other
```

### J. Дроби v0.7
```
Неверное решение
```
```python
class Fraction:

    def __init__(self, *args):
        dividend_and_divisor = self._parse(*args)
        self.dividend, self.divisor = map(
            lambda _: _ // self._gcd(*dividend_and_divisor),
            dividend_and_divisor
        )

    def _parse(self, *args) -> tuple[int]:

        SEP = "/"

        if len(args) == 1:
            dividend_or_frac_str, *_ = args
            if isinstance(dividend_or_frac_str, int):
                return dividend_or_frac_str, 1
            if isinstance(dividend_or_frac_str, str):
                if SEP not in dividend_or_frac_str:
                    return int(dividend_or_frac_str), 1
                else:
                    return tuple(map(int, dividend_or_frac_str.split(SEP)))
        elif len(args) == 2:
            return args
        else:
            raise Exception

    def _gcd(self, a: int, b: int) -> int:
        while b:
            a, b = b, a % b
        return a

    def _get_rational_from_int_or_str(self, int_or_str):
        return int_or_str if isinstance(
            int_or_str, Fraction
        ) else Fraction(int_or_str)

    def numerator(self, number=None):
        if not number:
            return abs(self.dividend)
        self.__init__(number if self.dividend > 0 else -number, self.divisor)

    def denominator(self, number=None):
        if not number:
            return self.divisor
        self.__init__(self.dividend, number)

    def __str__(self):
        return f"{self.dividend}/{self.divisor}"

    def __repr__(self):
        return f"Fraction('{str(self)}')"

    def __neg__(self):
        return Fraction(-self.dividend, self.divisor)

    def __add__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return Fraction(
            self.dividend * other.divisor + self.divisor * other.dividend,
            self.divisor * other.divisor
        )

    def __sub__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return Fraction(
            self.dividend * other.divisor - self.divisor * other.dividend,
            self.divisor * other.divisor
        )

    def __iadd__(self, other):
        self.__init__(
            self.dividend * other.divisor + self.divisor * other.dividend,
            self.divisor * other.divisor
        )
        return self

    def __isub__(self, other):
        self.__init__(
            self.dividend * other.divisor - self.divisor * other.dividend,
            self.divisor * other.divisor
        )
        return self

    def __mul__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return Fraction(
            self.dividend * other.dividend, self.divisor * other.divisor
        )

    def __truediv__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return Fraction(
            self.dividend * other.divisor, self.divisor * other.dividend
        )

    def __imul__(self, other):
        self.__init__(
            self.dividend * other.dividend, self.divisor * other.divisor
        )
        return self

    def __itruediv__(self, other):
        self.__init__(
            self.dividend * other.divisor, self.divisor * other.dividend
        )
        return self

    def reverse(self):
        self.__init__(self.divisor, self.dividend)
        return self

    def __lt__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return self.dividend * other.divisor < self.divisor * other.dividend

    def __le__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return self.dividend * other.divisor <= self.divisor * other.dividend

    def __eq__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return self.dividend * other.divisor == self.divisor * other.dividend

    def __ne__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return self.dividend * other.divisor != self.divisor * other.dividend

    def __gt__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return self.dividend * other.divisor > self.divisor * other.dividend

    def __ge__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return self.dividend * other.divisor >= self.divisor * other.dividend

    def __radd__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return Fraction(
            self.dividend * other.divisor + self.divisor * other.dividend,
            self.divisor * other.divisor
        )

    def __rsub__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return Fraction(
            self.divisor * other.dividend - self.dividend * other.divisor,
            self.divisor * other.divisor
        )

    def __rmul__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return Fraction(
            self.dividend * other.dividend, self.divisor * other.divisor
        )

    def __rtruediv__(self, other):
        other = self._get_rational_from_int_or_str(other)
        return Fraction(
            self.divisor * other.dividend, self.dividend * other.divisor
        )
```

# Python 

## 10 Standard Library Modules

- [dataclasses](https://docs.python.org/3/library/dataclasses.html)
- [pathlib](https://docs.python.org/3/library/pathlib.html)
- [cache](https://docs.python.org/3/library/functools.html)
- [tomllib](https://docs.python.org/3/library/tomllib.html)
- [graphlib](https://docs.python.org/3/library/graphlib.html)
- [heapq](https://docs.python.org/3/library/heapq.html)
- [secrets](https://docs.python.org/3/library/secrets.html)
- [shutil](https://docs.python.org/3/library/shutil.html)
- [textwrap](https://docs.python.org/3/library/textwrap.html)
- [itertools](https://docs.python.org/3/library/itertools.html) 

```python 
from dataclasses import dataclass


@dataclass
class Product:
    name: str
    price: float
    in_stock: bool = True


print(Product(name="Widget", price=19.99))
# Product(name='Widget', price=19.99, in_stock=True)

```
```python 
import itertools

list(itertools.combinations(["a", "b", "c"], 2))
# [('a', 'b'), ('a', 'c'), ('b', 'c')]
```

## Loops 

```python
from dataclasses import dataclass


@dataclass
class User:
    name: str
    age: int


users: list[User] = [
    {"name": "Alice", "age": 28},
    {"name": "Bob", "age": 17},
    {"name": "Carol", "age": 35},
]

# For loop (faster)
adult_names: list[str] = []
for user in users:
    if user["age"] >= 18:
        adult_names.append(user["name"].upper())

# Map/filter
adult_users = filter(lambda u: u["age"] >= 18, users)
adult_names = list(map(lambda u: u["name"].upper(), adult_users))

# List comprehension
adult_names = [user["name"].upper() for user in users if user["age"] >= 18]
```

--- 

#### Sources

- [10 Standard Library Modules Video](https://www.youtube.com/watch?v=eZ9RqnkJxsk)
- [10 Standard Library Modules Repository](https://github.com/ArjanCodes/examples/tree/main/2025/standard)
- [Let’s Replace All For Loops With Map and Filter Repository](https://github.com/ArjanCodes/examples/blob/main/2025/map/basic_example.py)

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


--- 

#### Sources

- [10 Standard Library Modules Video](https://www.youtube.com/watch?v=eZ9RqnkJxsk)
- [10 Standard Library Modules Repository](https://github.com/ArjanCodes/examples/tree/main/2025/standard)

# chain_dot

Returns the dot product of multiple vectors represented as dicts.



## Parameters

- **xs**



## Examples

```python
>>> from river import utils

>>> x = {'x0': 1, 'x1': 2, 'x2': 1}
>>> y = {'x1': 21, 'x2': 3}
>>> z = {'x1': 2, 'x2': 1 / 3}

>>> utils.math.chain_dot(x, y, z)
85.0
```


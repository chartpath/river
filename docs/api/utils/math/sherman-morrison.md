# sherman_morrison

Sherman–Morrison formula.

This modifies `A_inv` inplace.

## Parameters

- **A_inv** (*dict*)

- **u** (*dict*)

- **v** (*dict*)



## Examples

```python
>>> import pprint
>>> from river import utils

>>> A_inv = {
...     (0, 0): 0.2,
...     (1, 1): 1,
...     (2, 2): 1
... }
>>> u = {0: 1, 1: 2, 2: 3}
>>> v = {0: 4}

>>> inv = sherman_morrison(A_inv, u, v)
>>> pprint.pprint(inv)
{(0, 0): 0.111111,
    (1, 0): -0.888888,
    (1, 1): 1,
    (2, 0): -1.333333,
    (2, 2): 1}
```

## References

[^1]: [Wikipedia article on the Sherman-Morrison formula](https://www.wikiwand.com/en/Sherman%E2%80%93Morrison_formula)s


# Window

Running window data structure.

This is just a convenience layer on top of a `collections.deque`. The only reason this exists is that deepcopying a class which inherits from `collections.deque` seems to bug out when the class has a parameter with no default value.

## Parameters

- **size** (*int*)

    Size of the rolling window.


## Attributes

- **size**


## Examples

```python
>>> from river import utils

>>> window = utils.Window(size=2)

>>> for x in [1, 2, 3, 4, 5, 6]:
...     print(window.append(x))
[1]
[1, 2]
[2, 3]
[3, 4]
[4, 5]
[5, 6]
```

## Methods

???- note "append"

???- note "extend"

???- note "popleft"


# iter_array

Iterates over the rows from an array of features and an array of targets.

This method is intended to work with `numpy` arrays, but should also work with Python lists.

## Parameters

- **X** (*numpy.ndarray*)

    A 2D array of features.

- **y** (*numpy.ndarray*) – defaults to `None`

    An optional array of targets.

- **feature_names** (*List[Hashable]*) – defaults to `None`

    An optional list of feature names. The features will be labeled with integers if no names are provided.

- **target_names** (*List[Hashable]*) – defaults to `None`

    An optional list of output names. The outputs will be labeled with integers if no names are provided. Only applies if there are multiple outputs, i.e. if `y` is a 2D array.

- **shuffle** (*bool*) – defaults to `False`

    Indicates whether or not to shuffle the input arrays before iterating over them.

- **seed** (*int*) – defaults to `None`

    Random seed used for shuffling the data.



## Examples

```python
>>> from river import stream
>>> import numpy as np

>>> X = np.array([[1, 2, 3], [11, 12, 13]])
>>> Y = np.array([True, False])

>>> dataset = stream.iter_array(
...     X, Y,
...     feature_names=['x1', 'x2', 'x3']
... )
>>> for x, y in dataset:
...     print(x, y)
{'x1': 1, 'x2': 2, 'x3': 3} True
{'x1': 11, 'x2': 12, 'x3': 13} False
```


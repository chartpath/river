# numpy2dict

Convert a numpy array to a dictionary.



## Parameters

- **data** (*numpy.ndarray*)

    An one-dimensional numpy.array.



## Examples

```python
>>> import numpy as np
>>> from river.utils import numpy2dict
>>> numpy2dict(np.array([1.0, 2.0, 3.0]))
{0: 1.0, 1: 2.0, 2: 3.0}
```


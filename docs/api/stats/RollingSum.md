# RollingSum

Running sum over a window.



## Parameters

- **window_size** (*int*)

    Size of the rolling window.


## Attributes

- **sum** (*int*)

    The running rolling sum.


## Examples

```python
>>> from river import stats

>>> X = [1, -4, 3, -2, 2, 1]
>>> rolling_sum = stats.RollingSum(2)
>>> for x in X:
...     print(rolling_sum.update(x).get())
1
-3
-1
1
0
3
```

## Methods

???- note "append"

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "extend"

???- note "get"

???- note "popleft"

???- note "revert"

    Revert and return the called instance.

    **Parameters**

    - **x**    
    
???- note "update"

    Update and return the called instance.

    **Parameters**

    - **x**    
    

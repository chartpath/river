# RollingMode

Running mode over a window.

The mode is the most common value.

## Parameters

- **window_size** (*int*)

    Size of the rolling window.


## Attributes

- **counts** (*collections.defaultdict*)

    Value counts.


## Examples

```python
>>> from river import stats

>>> X = ['sunny', 'sunny', 'sunny', 'rainy', 'rainy', 'rainy', 'rainy']
>>> rolling_mode = stats.RollingMode(window_size=2)
>>> for x in X:
...     print(rolling_mode.update(x).get())
sunny
sunny
sunny
sunny
rainy
rainy
rainy

>>> rolling_mode = stats.RollingMode(window_size=5)
>>> for x in X:
...     print(rolling_mode.update(x).get())
sunny
sunny
sunny
sunny
sunny
rainy
rainy
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
    

# Mode

Running mode.

The mode is simply the most common value. An approximate mode can be computed by setting the number of first unique values to count.

## Parameters

- **k** – defaults to `25`

    Only the first `k` unique values will be included. If `k` equals -1, the exact mode is computed.


## Attributes

- **name**


## Examples

```python
>>> from river import stats

>>> X = ['sunny', 'cloudy', 'cloudy', 'rainy', 'rainy', 'rainy']
>>> mode = stats.Mode(k=2)
>>> for x in X:
...     print(mode.update(x).get())
sunny
sunny
cloudy
cloudy
cloudy
cloudy

>>> mode = stats.Mode(k=-1)
>>> for x in X:
...     print(mode.update(x).get())
sunny
sunny
cloudy
cloudy
cloudy
rainy
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "get"

???- note "revert"

    Revert and return the called instance.

    **Parameters**

    - **x**    
    
???- note "update"

    Update and return the called instance.

    **Parameters**

    - **x**    
    

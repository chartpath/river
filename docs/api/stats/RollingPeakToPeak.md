# RollingPeakToPeak

Running peak to peak (max - min) over a window.



## Parameters

- **window_size** (*int*)

    Size of the rolling window.


## Attributes

- **max** (*stats.RollingMax*)

    The running rolling max.

- **min** (*stats.RollingMin*)

    The running rolling min.


## Examples

```python
>>> from river import stats

>>> X = [1, -4, 3, -2, 2, 1]
>>> ptp = stats.RollingPeakToPeak(window_size=2)
>>> for x in X:
...     print(ptp.update(x).get())
0
5
7
5
4
1
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
    

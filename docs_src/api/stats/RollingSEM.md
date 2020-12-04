# RollingSEM

Running standard error of the mean over a window.



## Parameters

- **window_size**

    Size of the rolling window.

- **ddof** – defaults to `1`

    Delta Degrees of Freedom for the variance.


## Attributes

- **correction_factor**

- **name**

- **window_size**


## Examples

```python
>>> import river

>>> X = [1, 4, 2, -4, -8, 0]

>>> rolling_sem = river.stats.RollingSEM(ddof=1, window_size=2)
>>> for x in X:
...     print(rolling_sem.update(x).get())
0.0
1.5
1.0
3.0
2.0
4.0

>>> rolling_sem = river.stats.RollingSEM(ddof=1, window_size=3)
>>> for x in X:
...     print(rolling_sem.update(x).get())
0.0
1.5
0.881917
2.403700
2.905932
2.309401
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
    

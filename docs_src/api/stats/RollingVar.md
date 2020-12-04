# RollingVar

Running variance over a window.



## Parameters

- **window_size**

    Size of the rolling window.

- **ddof** – defaults to `1`

    Delta Degrees of Freedom for the variance.


## Attributes

- **sos** (*float*)

    Sum of squares over the current window.

- **rmean** (*stats.RollingMean*)


## Examples

```python
>>> import river

>>> X = [1, 4, 2, -4, -8, 0]

>>> rvar = river.stats.RollingVar(ddof=1, window_size=2)
>>> for x in X:
...     print(rvar.update(x).get())
0.0
4.5
2.0
18.0
8.0
32.0

>>> rvar = river.stats.RollingVar(ddof=1, window_size=3)
>>> for x in X:
...     print(rvar.update(x).get())
0.0
4.5
2.333333
17.333333
25.333333
16.0
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
    

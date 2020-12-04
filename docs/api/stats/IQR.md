# IQR

Computes the interquartile range.



## Parameters

- **q_inf** – defaults to `0.25`

    Desired inferior quantile, must be between 0 and 1. Defaults to `0.25`.

- **q_sup** – defaults to `0.75`

    Desired superior quantile, must be between 0 and 1. Defaults to `0.75`.


## Attributes

- **name**


## Examples

```python
>>> from river import stats

>>> iqr = stats.IQR(q_inf=0.25, q_sup=0.75)

>>> for i in range(0, 1001):
...     iqr = iqr.update(i)
...     if i % 100 == 0:
...         print(iqr.get())
0
50.0
100.0
150.0
200.0
250.0
300.0
350.0
400.0
450.0
500.0
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
    

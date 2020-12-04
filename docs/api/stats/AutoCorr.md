# AutoCorr

Measures the serial correlation.

This method computes the Pearson correlation between the current value and the value seen `n` steps before.

## Parameters

- **lag** (*int*)


## Attributes

- **name**


## Examples

The following examples are taken from the [pandas documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.autocorr.html).

```python
>>> from river import stats

>>> auto_corr = stats.AutoCorr(lag=1)
>>> for x in [0.25, 0.5, 0.2, -0.05]:
...     print(auto_corr.update(x).get())
0
0
-1.0
0.103552

>>> auto_corr = stats.AutoCorr(lag=2)
>>> for x in [0.25, 0.5, 0.2, -0.05]:
...     print(auto_corr.update(x).get())
0
0
0
-1.0

>>> auto_corr = stats.AutoCorr(lag=1)
>>> for x in [1, 0, 0, 0]:
...     print(auto_corr.update(x).get())
0
0
0
0
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
    

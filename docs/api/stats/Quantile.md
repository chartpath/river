# Quantile

Running quantile.

Uses the P² algorithm, which is also known as the "Piecewise-Parabolic quantile estimator". The code is inspired by LiveStat's implementation [^2].

## Parameters

- **q** – defaults to `0.5`

    Determines which quantile to compute, must be comprised between 0 and 1.


## Attributes

- **name**


## Examples

```python
>>> from river import stats
>>> import numpy as np

>>> np.random.seed(42 * 1337)
>>> mu, sigma = 0, 1
>>> s = np.random.normal(mu, sigma, 500)

>>> median = stats.Quantile(0.5)
>>> for x in s:
...    _ = median.update(x)

>>> print(f'The estimated value of the 50th (median) quantile is {median.get():.4f}')
The estimated value of the 50th (median) quantile is -0.0275
>>> print(f'The real value of the 50th (median) quantile is {np.median(s):.4f}')
The real value of the 50th (median) quantile is -0.0135

>>> percentile_17 = stats.Quantile(0.17)
>>> for x in s:
...    _ = percentile_17.update(x)

>>> print(f'The estimated value of the 17th quantile is {percentile_17.get():.4f}')
The estimated value of the 17th quantile is -0.8652
>>> print(f'The real value of the 17th quantile is {np.percentile(s,17):.4f}')
The real value of the 17th quantile is -0.9072
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
    
## References

[^1]: [The P² Algorithm for Dynamic Univariateal Computing Calculation of Quantiles and Editor Histograms Without Storing Observations](https://www.cse.wustl.edu/~jain/papers/ftp/psqr.pdf)
[^2]: [LiveStats](https://github.com/cxxr/LiveStats)
[^3]: [P² quantile estimator: estimating the median without storing values](https://aakinshin.net/posts/p2-quantile-estimator/)


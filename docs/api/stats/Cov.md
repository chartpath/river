# Cov

Covariance.



## Parameters

- **ddof** – defaults to `1`

    Delta Degrees of Freedom.



## Examples

```python
>>> from river import stats

>>> x = [-2.1,  -1,  4.3]
>>> y = [   3, 1.1, 0.12]

>>> cov = stats.Cov()

>>> for xi, yi in zip(x, y):
...     print(cov.update(xi, yi).get())
0.0
-1.044999
-4.286
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "get"

    Return the current value of the statistic.

    
???- note "update"

    Update and return the called instance.

    **Parameters**

    - **x**    
    - **y**    
    
## References

[^1]: [Wikipedia article on algorithms for calculating variance](https://www.wikiwand.com/en/Algorithms_for_calculating_variance#/Covariance)


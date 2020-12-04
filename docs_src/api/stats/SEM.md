# SEM

Running standard error of the mean using Welford's algorithm.



## Parameters

- **ddof** – defaults to `1`

    Delta Degrees of Freedom. The divisor used in calculations is `n - ddof`, where `n` is the number of seen elements.


## Attributes

- **n** (*int*)

    Number of observations.


## Examples

```python
>>> import river.stats

>>> X = [3, 5, 4, 7, 10, 12]

>>> sem = river.stats.SEM()
>>> for x in X:
...     print(sem.update(x).get())
0.0
1.0
0.577350
0.853912
1.240967
1.447219
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
    - **w**     – defaults to `1.0`    
    
## References

[^1]: [Wikipedia article on algorithms for calculating variance](https://www.wikiwand.com/en/Algorithms_for_calculating_variance#/Covariance)


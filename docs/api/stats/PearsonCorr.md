# PearsonCorr

Online Pearson correlation.



## Parameters

- **ddof** – defaults to `1`

    Delta Degrees of Freedom.


## Attributes

- **var_x** (*stats.Var*)

    Running variance of `x`.

- **var_y** (*stats.Var*)

    Running variance of `y`.

- **cov_xy** (*stats.Cov*)

    Running covariance of `x` and `y`.


## Examples

```python
>>> from river import stats

>>> x = [0, 0, 0, 1, 1, 1, 1]
>>> y = [0, 1, 2, 3, 4, 5, 6]

>>> pearson = stats.PearsonCorr()

>>> for xi, yi in zip(x, y):
...     print(pearson.update(xi, yi).get())
0
0
0
0.774596
0.866025
0.878310
0.866025
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
    

# RollingCov

Rolling covariance.



## Parameters

- **window_size**

    Size of the window over which to compute the covariance.

- **ddof** – defaults to `1`

    Delta Degrees of Freedom.


## Attributes

- **window_size**


## Examples

```python
>>> from river import stats

>>> x = [-2.1,  -1, 4.3, 1, -2.1,  -1, 4.3]
>>> y = [   3, 1.1, .12, 1,    3, 1.1, .12]

>>> rcov = stats.RollingCov(3)

>>> for xi, yi in zip(x, y):
...     print(rcov.update(xi, yi).get())
0.0
-1.045
-4.286
-1.382
-4.589
-1.415
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
    

# Var

Running variance using Welford's algorithm.



## Parameters

- **ddof** – defaults to `1`

    Delta Degrees of Freedom. The divisor used in calculations is `n - ddof`, where `n` represents the number of seen elements.


## Attributes

- **mean** (*stats.Mean*)

    The running mean.

- **sos** (*float*)

    The running sum of squares.


## Examples

```python
>>> import river.stats

>>> X = [3, 5, 4, 7, 10, 12]

>>> var = river.stats.Var()
>>> for x in X:
...     print(var.update(x).get())
0.0
2.0
1.0
2.916666
7.7
12.56666
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
    
## Notes

The outcomes of the incremental and parallel updates are consistent with numpy's
batch processing when $\\text{ddof} \le 1$.

## References

[^1]: [Wikipedia article on algorithms for calculating variance](https://www.wikiwand.com/en/Algorithms_for_calculating_variance#/Covariance)
[^2]: [Chan, T.F., Golub, G.H. and LeVeque, R.J., 1983. Algorithms for computing the sample variance: Analysis and recommendations. The American Statistician, 37(3), pp.242-247.](https://amstat.tandfonline.com/doi/abs/10.1080/00031305.1983.10483115)


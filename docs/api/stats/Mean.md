# Mean

Running mean.




## Attributes

- **mean** (*float*)

    The current value of the mean.

- **n** (*float*)

    The current sum of weights. If each passed weight was 1, then this is equal to the number of seen observations.


## Examples

```python
>>> from river import stats

>>> X = [-5, -3, -1, 1, 3, 5]
>>> mean = stats.Mean()
>>> for x in X:
...     print(mean.update(x).get())
-5.0
-4.0
-3.0
-2.0
-1.0
0.0
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
    - **w**     – defaults to `1.0`    
    
???- note "update"

    Update and return the called instance.

    **Parameters**

    - **x**    
    - **w**     – defaults to `1.0`    
    
## References

[^1]: [West, D. H. D. (1979). Updating mean and variance estimates: An improved method. Communications of the ACM, 22(9), 532-535.](https://people.xiph.org/~tterribe/tmp/homs/West79-_Updating_Mean_and_Variance_Estimates-_An_Improved_Method.pdf)
[^2]: [Finch, T., 2009. Incremental calculation of weighted mean and variance. University of Cambridge, 4(11-5), pp.41-42.](https://fanf2.user.srcf.net/hermes/doc/antiforgery/stats.pdf)
[^3]: [Chan, T.F., Golub, G.H. and LeVeque, R.J., 1983. Algorithms for computing the sample variance: Analysis and recommendations. The American Statistician, 37(3), pp.242-247.](https://amstat.tandfonline.com/doi/abs/10.1080/00031305.1983.10483115)


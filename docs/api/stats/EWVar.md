# EWVar

Exponentially weighted variance.

To calculate the variance we use the fact that Var(X) = Mean(x^2) - Mean(x)^2 and internally we use the exponentially weighted mean of x/x^2 to calculate this.

## Parameters

- **alpha** – defaults to `0.5`

    The closer `alpha` is to 1 the more the statistic will adapt to recent values.


## Attributes

- **variance** (*float*)

    The running exponentially weighted variance.


## Examples

```python
>>> from river import stats

>>> X = [1, 3, 5, 4, 6, 8, 7, 9, 11]
>>> ewv = stats.EWVar(alpha=0.5)
>>> for x in X:
...     print(ewv.update(x).get())
0
1.0
2.75
1.4375
1.984375
3.43359375
1.7958984375
2.198974609375
3.56536865234375
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

[^1]: [Finch, T., 2009. Incremental calculation of weighted mean and variance. University of Cambridge, 4(11-5), pp.41-42.](http://people.ds.cam.ac.uk/fanf2/hermes/doc/antiforgery/stats.pdf)
[^2]: [Exponential Moving Average on Streaming Data](https://dev.to/nestedsoftware/exponential-moving-average-on-streaming-data-4hhl)


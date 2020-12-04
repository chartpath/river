# EWMean

Exponentially weighted mean.



## Parameters

- **alpha** – defaults to `0.5`

    The closer `alpha` is to 1 the more the statistic will adapt to recent values.


## Attributes

- **mean** (*float*)

    The running exponentially weighted mean.


## Examples

```python
>>> from river import stats

>>> X = [1, 3, 5, 4, 6, 8, 7, 9, 11]
>>> ewm = stats.EWMean(alpha=0.5)
>>> for x in X:
...     print(ewm.update(x).get())
1
2.0
3.5
3.75
4.875
6.4375
6.71875
7.859375
9.4296875
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


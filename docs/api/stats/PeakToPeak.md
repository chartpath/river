# PeakToPeak

Running peak to peak (max - min).




## Attributes

- **max** (*stats.Max*)

    The running max.

- **min** (*stats.Min*)

    The running min.

- **p2p** (*float*)

    The running peak to peak.


## Examples

```python
>>> from river import stats

>>> X = [1, -4, 3, -2, 2, 4]
>>> ptp = stats.PeakToPeak()
>>> for x in X:
...     print(ptp.update(x).get())
0
5
7
7
7
8
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
    

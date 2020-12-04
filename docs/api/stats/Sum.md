# Sum

Running sum.




## Attributes

- **sum** (*float*)

    The running sum.


## Examples

```python
>>> from river import stats

>>> X = [-5, -3, -1, 1, 3, 5]
>>> mean = stats.Sum()
>>> for x in X:
...     print(mean.update(x).get())
-5.0
-8.0
-9.0
-8.0
-5.0
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
    
???- note "update"

    Update and return the called instance.

    **Parameters**

    - **x**    
    

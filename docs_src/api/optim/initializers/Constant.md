# Constant

Constant initializer which always returns the same value.



## Parameters

- **value** (*float*)



## Examples

```python
>>> from river import optim

>>> init = optim.initializers.Constant(value=3.14)

>>> init(shape=1)
3.14

>>> init(shape=2)
array([3.14, 3.14])
```

## Methods

???- note "__call__"

    Returns a fresh set of weights.

    **Parameters**

    - **shape**     – defaults to `1`    
    
???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    

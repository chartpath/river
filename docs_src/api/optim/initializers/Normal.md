# Normal

Random normal initializer which simulate a normal distribution with specified parameters.



## Parameters

- **mu** – defaults to `0.0`

    The mean of the normal distribution

- **sigma** – defaults to `1.0`

    The standard deviation of the normal distribution

- **seed** – defaults to `None`

    Random number generation seed that can be set for reproducibility.



## Examples

```python
>>> from river import optim

>>> init = optim.initializers.Normal(mu=0, sigma=1, seed=42)

>>> init(shape=1)
0.496714

>>> init(shape=2)
array([-0.1382643 ,  0.64768854])
```

## Methods

???- note "__call__"

    Returns a fresh set of weights.

    **Parameters**

    - **shape**     – defaults to `1`    
    
???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    

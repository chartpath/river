# InverseScaling

Reduces the learning rate using a power schedule.

Assuming an initial learning rate $\eta$, the learning rate at step $t$ is: 

$$\frac{eta}{(t + 1) ^ p}$$ 

where $p$ is a user-defined parameter.

## Parameters

- **learning_rate** (*float*)

- **power** – defaults to `0.5`




## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "get"

    Returns the learning rate at a given iteration.

    **Parameters**

    - **t**     (*int*)    
    

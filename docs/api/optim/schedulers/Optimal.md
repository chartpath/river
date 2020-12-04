# Optimal

Optimal learning schedule as proposed by Léon Bottou.



## Parameters

- **loss** (*[optim.losses.Loss](../../../optim/losses/Loss)*)

- **alpha** – defaults to `0.0001`




## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "get"

    Returns the learning rate at a given iteration.

    **Parameters**

    - **t**     (*int*)    
    
## References

[^1]: [Bottou, L., 2012. Stochastic gradient descent tricks. In Neural networks: Tricks of the trade (pp. 421-436). Springer, Berlin, Heidelberg.](https://cilvr.cs.nyu.edu/diglib/lsml/bottou-sgd-tricks-2012.pdf)


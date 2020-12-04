# BayesianMean

Estimates a mean using outside information.



## Parameters

- **prior** (*float*)

- **prior_weight** (*float*)


## Attributes

- **name**



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

[^1]: [Additive smoothing](https://www.wikiwand.com/en/Additive_smoothing)
[^2]: [Bayesian average](https://www.wikiwand.com/en/Bayesian_average)
[^3]: [Practical example of Bayes estimators](https://www.wikiwand.com/en/Bayes_estimator#/Practical_example_of_Bayes_estimators)


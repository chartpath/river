# Optimizer

Optimizer interface.

Every optimizer inherits from this base interface.

## Parameters

- **lr** (*Union[[optim.schedulers.Scheduler](../../optim/schedulers/Scheduler), float]*)


## Attributes

- **learning_rate** (*float*)

    Returns the current learning rate value.



## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "update_after_pred"

    Updates a weight vector given a gradient.

    Parameters:     w (dict): A dictionary of weight parameters. The weights are modified in-place.     g (dict): A dictionary of gradients.  Returns:     The updated weights.

    **Parameters**

    - **w**     (*dict*)    
    - **g**     (*dict*)    
    
???- note "update_before_pred"

    Updates a weight vector before a prediction is made.

    Parameters:     w (dict): A dictionary of weight parameters. The weights are modified in-place.  Returns:     The updated weights.

    **Parameters**

    - **w**     (*dict*)    
    

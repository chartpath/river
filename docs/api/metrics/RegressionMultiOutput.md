# RegressionMultiOutput

Wrapper for multi-output regression.

This wraps a regression metric to make it compatible with multi-output regression tasks. The value of each output will be fed sequentially to the `get` method of the provided metric.

## Parameters

- **metric** (*'base.RegressionMetric'*)

    The regression metric to evaluate with each output.


## Attributes

- **bigger_is_better**

    Indicates if a high value is better than a low one or not.

- **metric**

    Gives access to the wrapped metric.

- **requires_labels**



## Methods

???- note "get"

    Return the current value of the metric.

    
???- note "revert"

    Revert the metric.

    **Parameters**

    - **y_true**     (*Dict[Union[str, int], Union[float, int]]*)    
    - **y_pred**     (*Dict[Union[str, int], Union[float, int]]*)    
    - **sample_weight**     (*numbers.Number*)     – defaults to `1.0`    
    
???- note "update"

    Update the metric.

    **Parameters**

    - **y_true**     (*Dict[Union[str, int], Union[float, int]]*)    
    - **y_pred**     (*Dict[Union[str, int], Union[float, int]]*)    
    - **sample_weight**     (*numbers.Number*)     – defaults to `1.0`    
    
???- note "works_with"

    Indicates whether or not a metric can work with a given model.

    **Parameters**

    - **model**     (*river.base.estimator.Estimator*)    
    

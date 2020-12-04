# MCC

Matthews correlation coefficient.



## Parameters

- **cm** – defaults to `None`

    This parameter allows sharing the same confusion matrix between multiple metrics. Sharing a confusion matrix reduces the amount of storage and computation time.

- **pos_val** – defaults to `True`

    Value to treat as "positive".


## Attributes

- **bigger_is_better**

    Indicates if a high value is better than a low one or not.

- **requires_labels**

    Indicates if labels are required, rather than probabilities.

- **sample_correction**


## Examples

```python
>>> from river import metrics

>>> y_true = [True, True, True, False]
>>> y_pred = [True, False, True, True]

>>> mcc = metrics.MCC()

>>> for yt, yp in zip(y_true, y_pred):
...     mcc = mcc.update(yt, yp)

>>> mcc
MCC: -0.333333
```

## Methods

???- note "get"

    Return the current value of the metric.

    
???- note "revert"

    Revert the metric.

    **Parameters**

    - **y_true**     (*bool*)    
    - **y_pred**     (*Union[bool, float, Dict[bool, float]]*)    
    - **sample_weight**     – defaults to `1.0`    
    - **correction**     – defaults to `None`    
    
???- note "update"

    Update the metric.

    **Parameters**

    - **y_true**     (*bool*)    
    - **y_pred**     (*Union[bool, float, Dict[bool, float]]*)    
    - **sample_weight**     – defaults to `1.0`    
    
???- note "works_with"

    Indicates whether or not a metric can work with a given model.

    **Parameters**

    - **model**     (*river.base.estimator.Estimator*)    
    
## References

[^1]: [Wikipedia article](https://www.wikiwand.com/en/Matthews_correlation_coefficient)


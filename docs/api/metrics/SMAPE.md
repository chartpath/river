# SMAPE

Symmetric mean absolute percentage error.




## Attributes

- **bigger_is_better**

    Indicates if a high value is better than a low one or not.


## Examples

```python
>>> from river import metrics

>>> y_true = [0, 0.07533, 0.07533, 0.07533, 0.07533, 0.07533, 0.07533, 0.0672, 0.0672]
>>> y_pred = [0, 0.102, 0.107, 0.047, 0.1, 0.032, 0.047, 0.108, 0.089]

>>> metric = metrics.SMAPE()
>>> for yt, yp in zip(y_true, y_pred):
...     metric = metric.update(yt, yp)

>>> metric
SMAPE: 37.869392
```

## Methods

???- note "get"

    Return the current value of the metric.

    
???- note "revert"

    Revert the metric.

    **Parameters**

    - **y_true**     (*numbers.Number*)    
    - **y_pred**     (*numbers.Number*)    
    - **sample_weight**     (*numbers.Number*)     – defaults to `1.0`    
    
???- note "update"

    Update the metric.

    **Parameters**

    - **y_true**     (*numbers.Number*)    
    - **y_pred**     (*numbers.Number*)    
    - **sample_weight**     (*numbers.Number*)     – defaults to `1.0`    
    
???- note "works_with"

    Indicates whether or not a metric can work with a given model.

    **Parameters**

    - **model**    
    

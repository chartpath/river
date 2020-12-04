# MSE

Mean squared error.




## Attributes

- **bigger_is_better**

    Indicates if a high value is better than a low one or not.


## Examples

```python
>>> from river import metrics

>>> y_true = [3, -0.5, 2, 7]
>>> y_pred = [2.5, 0.0, 2, 8]

>>> metric = metrics.MSE()

>>> for yt, yp in zip(y_true, y_pred):
...     print(metric.update(yt, yp).get())
0.25
0.25
0.1666
0.375
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
    

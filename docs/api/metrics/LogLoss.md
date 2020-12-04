# LogLoss

Binary logarithmic loss.




## Attributes

- **bigger_is_better**

    Indicates if a high value is better than a low one or not.

- **requires_labels**

    Indicates if labels are required, rather than probabilities.

- **sample_correction**


## Examples

```python
>>> from river import metrics

>>> y_true = [True, False, False, True]
>>> y_pred = [0.9,  0.1,   0.2,   0.65]

>>> metric = metrics.LogLoss()
>>> for yt, yp in zip(y_true, y_pred):
...     metric = metric.update(yt, yp)
...     print(metric.get())
0.105360
0.105360
0.144621
0.216161

>>> metric
LogLoss: 0.216162
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
    
???- note "update"

    Update the metric.

    **Parameters**

    - **y_true**     (*bool*)    
    - **y_pred**     (*Union[bool, float, Dict[bool, float]]*)    
    - **sample_weight**     – defaults to `1.0`    
    
???- note "works_with"

    Indicates whether or not a metric can work with a given model.

    **Parameters**

    - **model**    
    

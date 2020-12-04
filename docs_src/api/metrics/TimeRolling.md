# TimeRolling

Wrapper for computing metrics over a period of time.



## Parameters

- **metric** (*river.metrics.base.Metric*)

    A metric.

- **period** (*datetime.timedelta*)

    A period of time.


## Attributes

- **bigger_is_better**

    Indicates if a high value is better than a low one or not.

- **metric**

    Gives access to the wrapped metric.

- **requires_labels**


## Examples

```python
>>> import datetime as dt
>>> from river import metrics

>>> y_true = [3, -0.5, 2, 7]
>>> y_pred = [2.5, 0.0, 2, 9]
>>> days = [1, 2, 3, 4]

>>> metric = metrics.TimeRolling(metrics.MAE(), period=dt.timedelta(days=2))

>>> for yt, yp, day in zip(y_true, y_pred, days):
...     t = dt.datetime(2019, 1, day)
...     print(metric.update(yt, yp, t))
MAE: 0.5
MAE: 0.5
MAE: 0.25
MAE: 1.
```

## Methods

???- note "get"

    Return the current value of the metric.

    
???- note "revert"

    Revert the metric.

    **Parameters**

    - **y_true**    
    - **y_pred**    
    
???- note "update"

    Update the metric.

    **Parameters**

    - **y_true**    
    - **y_pred**    
    - **t**    
    
???- note "works_with"

    Indicates whether or not a metric can work with a given model.

    **Parameters**

    - **model**     (*river.base.estimator.Estimator*)    
    

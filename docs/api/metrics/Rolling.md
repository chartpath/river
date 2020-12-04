# Rolling

Wrapper for computing metrics over a window.

This wrapper metric allows you to apply a metric over a window of observations. Under the hood, a buffer with the `window_size` most recent pairs of `(y_true, y_pred)` is memorised. When the buffer is full, the oldest pair is removed and the `revert` method of the metric is called with said pair. 

You should use `metrics.Rolling` to evaluate a metric over a window of fixed sized. You can use `metrics.TimeRolling` to instead evaluate a metric over a period of time.

## Parameters

- **metric** (*river.metrics.base.Metric*)

    A metric.

- **window_size** (*int*)

    The number of most recent `(y_true, y_pred)` pairs on which to evaluate the metric.


## Attributes

- **bigger_is_better**

    Indicates if a high value is better than a low one or not.

- **metric**

    Gives access to the wrapped metric.

- **requires_labels**

- **size**


## Examples

```python
>>> from river import metrics

>>> y_true = [3, -0.5, 2, 7]
>>> y_pred = [2.5, 0.0, 2, 8]

>>> metric = metrics.Rolling(metrics.MSE(), window_size=2)

>>> for yt, yp in zip(y_true, y_pred):
...     print(metric.update(yt, yp))
Rolling of size 2 MSE: 0.25
Rolling of size 2 MSE: 0.25
Rolling of size 2 MSE: 0.125
Rolling of size 2 MSE: 0.5
```

## Methods

???- note "append"

???- note "extend"

???- note "get"

    Return the current value of the metric.

    
???- note "popleft"

???- note "revert"

    Revert the metric.

    **Parameters**

    - **y_true**    
    - **y_pred**    
    - **sample_weight**     – defaults to `1.0`    
    
???- note "update"

    Update the metric.

    **Parameters**

    - **y_true**    
    - **y_pred**    
    - **sample_weight**     – defaults to `1.0`    
    
???- note "works_with"

    Indicates whether or not a metric can work with a given model.

    **Parameters**

    - **model**     (*river.base.estimator.Estimator*)    
    

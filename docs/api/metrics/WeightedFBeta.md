# WeightedFBeta

Weighted-average F-Beta score.

This works by computing the F-Beta score per class, and then performs a global weighted average according to the support of each class.

## Parameters

- **beta**

    Weight of precision in the harmonic mean.

- **cm** – defaults to `None`

    This parameter allows sharing the same confusion matrix between multiple metrics. Sharing a confusion matrix reduces the amount of storage and computation time.


## Attributes

- **bigger_is_better**

    Indicates if a high value is better than a low one or not.

- **requires_labels**

    Indicates if labels are required, rather than probabilities.

- **sample_correction**


## Examples

```python
>>> from river import metrics

>>> y_true = [0, 1, 2, 2, 2]
>>> y_pred = [0, 0, 2, 2, 1]

>>> metric = metrics.WeightedFBeta(beta=0.8)

>>> for yt, yp in zip(y_true, y_pred):
...     print(metric.update(yt, yp))
WeightedFBeta: 1.
WeightedFBeta: 0.310606
WeightedFBeta: 0.540404
WeightedFBeta: 0.655303
WeightedFBeta: 0.626283
```

## Methods

???- note "get"

    Return the current value of the metric.

    
???- note "revert"

    Revert the metric.

    **Parameters**

    - **y_true**    
    - **y_pred**    
    - **sample_weight**     – defaults to `1.0`    
    - **correction**     – defaults to `None`    
    
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
    

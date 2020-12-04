# WeightedRecall

Weighted-average recall score.

This uses the support of each label to compute an average score, whereas `MacroRecall` ignores the support.

## Parameters

- **cm** (*river.metrics.confusion.ConfusionMatrix*) – defaults to `None`

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

>>> metric = metrics.WeightedRecall()

>>> for yt, yp in zip(y_true, y_pred):
...     print(metric.update(yt, yp))
WeightedRecall: 1.
WeightedRecall: 0.5
WeightedRecall: 0.666667
WeightedRecall: 0.75
WeightedRecall: 0.6
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
    

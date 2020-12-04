# MicroF1

Micro-average F1 score.

This computes the F1 score by merging all the predictions and true labels, and then computes a global F1 score.

## Parameters

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

>>> y_true = [0, 1, 2, 2, 0]
>>> y_pred = [0, 1, 1, 2, 1]

>>> metric = metrics.MicroF1()
>>> for yt, yp in zip(y_true, y_pred):
...     metric = metric.update(yt, yp)

>>> metric
MicroF1: 0.6
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
    
## References

[^1]: [Why are precision, recall and F1 score equal when using micro averaging in a multi-class problem?](https://simonhessner.de/why-are-precision-recall-and-f1-score-equal-when-using-micro-averaging-in-a-multi-class-problem/)


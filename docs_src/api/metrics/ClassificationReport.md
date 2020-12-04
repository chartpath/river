# ClassificationReport

A report for monitoring a classifier.

This class maintains a set of metrics and updates each of them every time `update` is called. You can print this class at any time during a model's lifetime to get a tabular visualization of various metrics. 

You can wrap a `metrics.ClassificationReport` with `metrics.Rolling` in order to obtain a classification report over a window of observations. You can also wrap it with `metrics.TimeRolling` to obtain a report over a period of time.

## Parameters

- **decimals** – defaults to `3`

    The number of decimals to display in each cell.

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

>>> y_true = ['pear', 'apple', 'banana', 'banana', 'banana']
>>> y_pred = ['apple', 'pear', 'banana', 'banana', 'apple']

>>> report = metrics.ClassificationReport()

>>> for yt, yp in zip(y_true, y_pred):
...     report = report.update(yt, yp)

>>> print(report)
           Precision   Recall   F1      Support
<BLANKLINE>
   apple       0.000    0.000   0.000         1
  banana       1.000    0.667   0.800         3
    pear       0.000    0.000   0.000         1
<BLANKLINE>
   Macro       0.333    0.222   0.267
   Micro       0.400    0.400   0.400
Weighted       0.600    0.400   0.480
<BLANKLINE>
                 40.0% accuracy
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
    

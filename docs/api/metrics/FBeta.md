# FBeta

Binary F-Beta score.

The FBeta score is a weighted harmonic mean between precision and recall. The higher the `beta` value, the higher the recall will be taken into account. When `beta` equals 1, precision and recall and equivalently weighted, which results in the F1 score (see `metrics.F1`).

## Parameters

- **beta** (*float*)

    Weight of precision in the harmonic mean.

- **cm** – defaults to `None`

    This parameter allows sharing the same confusion matrix between multiple metrics. Sharing a confusion matrix reduces the amount of storage and computation time.

- **pos_val** – defaults to `True`

    Value to treat as "positive".


## Attributes

- **precision** (*metrics.Precision*)

- **recall** (*metrics.Recall*)


## Examples

```python
>>> from river import metrics

>>> y_true = [False, False, False, True, True, True]
>>> y_pred = [False, False, True, True, False, False]

>>> metric = metrics.FBeta(beta=2)
>>> for yt, yp in zip(y_true, y_pred):
...     metric = metric.update(yt, yp)

>>> metric
FBeta: 0.357143
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
    

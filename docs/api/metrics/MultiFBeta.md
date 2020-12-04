# MultiFBeta

Multi-class F-Beta score with different betas per class.

The multiclass F-Beta score is the arithmetic average of the binary F-Beta scores of each class. The mean can be weighted by providing class weights.

## Parameters

- **betas**

    Weight of precision in the harmonic mean of each class.

- **weights**

    Class weights. If not provided then uniform weights will be used.

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

>>> metric = metrics.MultiFBeta(
...     betas={0: 0.25, 1: 1, 2: 4},
...     weights={0: 1, 1: 1, 2: 2}
... )

>>> for yt, yp in zip(y_true, y_pred):
...     print(metric.update(yt, yp))
MultiFBeta: 1.
MultiFBeta: 0.257576
MultiFBeta: 0.628788
MultiFBeta: 0.628788
MultiFBeta: 0.468788
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
    

# ROCAUC

Receiving Operating Characteristic Area Under the Curve.

This metric is an approximation of the true ROC AUC. Computing the true ROC AUC would require storing all the predictions and ground truths, which isn't desirable. The approximation error is not significant as long as the predicted probabilities are well calibrated. In any case, this metric can still be used to reliably compare models between each other.

## Parameters

- **n_thresholds** – defaults to `10`

    The number of thresholds used for discretizing the ROC curve. A higher value will lead to more accurate results, but will also cost more time and memory.

- **pos_val** – defaults to `True`

    Value to treat as "positive".


## Attributes

- **bigger_is_better**

    Indicates if a high value is better than a low one or not.

- **requires_labels**

    Indicates if labels are required, rather than probabilities.

- **sample_correction**


## Examples

```python
>>> from river import metrics

>>> y_true = [ 0,  0,   1,  1]
>>> y_pred = [.1, .4, .35, .8]

>>> metric = metrics.ROCAUC()

>>> for yt, yp in zip(y_true, y_pred):
...     metric = metric.update(yt, yp)

>>> metric
ROCAUC: 0.875

```

The true ROC AUC is in fact 0.75. We can improve the accuracy by increasing the amount
of thresholds. This comes at the cost more computation time and more memory usage.

```python
>>> metric = metrics.ROCAUC(n_thresholds=20)

>>> for yt, yp in zip(y_true, y_pred):
...     metric = metric.update(yt, yp)

>>> metric
ROCAUC: 0.75
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

    - **model**     (*river.base.estimator.Estimator*)    
    

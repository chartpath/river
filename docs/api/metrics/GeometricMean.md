# GeometricMean

Geometric mean score.

The geometric mean is a good indicator of a classifier's performance in the presence of class imbalance because it is independent of the distribution of examples between classes. This implementation computes the geometric mean of class-wise sensitivity (recall). 

$$ gm = \sqrt[n]{s_1\cdot s_2\cdot s_3\cdot \ldots\cdot s_n} $$ 

where $s_i$ is the sensitivity (recall) of class $i$ and $n$ is the number of classes.

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

>>> y_true = ['cat', 'ant', 'cat', 'cat', 'ant', 'bird', 'bird']
>>> y_pred = ['ant', 'ant', 'cat', 'cat', 'ant', 'cat', 'bird']

>>> metric = metrics.GeometricMean()

>>> for yt, yp in zip(y_true, y_pred):
...     metric = metric.update(yt, yp)

>>> metric
GeometricMean: 0.693361
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

[^1]: Barandela, R. et al. “Strategies for learning in class imbalance problems”, Pattern Recognition, 36(3), (2003), pp 849-851.


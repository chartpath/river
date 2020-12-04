# KappaM

Kappa-M score.

The Kappa-M statistic compares performance with the majority class classifier. It is defined as 

$$ \kappa_{m} = (p_o - p_e) / (1 - p_e) $$ 

where $p_o$ is the empirical probability of agreement on the label assigned to any sample (prequential accuracy), and $p_e$ is the prequential accuracy of the `majority classifier`.

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

>>> y_true = ['cat', 'ant', 'cat', 'cat', 'ant', 'bird', 'cat', 'ant', 'cat', 'cat', 'ant']
>>> y_pred = ['ant', 'ant', 'cat', 'cat', 'ant', 'cat', 'ant', 'ant', 'cat', 'cat', 'ant']

>>> metric = metrics.KappaM()

>>> for yt, yp in zip(y_true, y_pred):
...     metric = metric.update(yt, yp)

>>> metric
KappaM: 0.25
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

[1^]: A. Bifet et al. "Efficient online evaluation of big data stream classifiers."
    In Proceedings of the 21th ACM SIGKDD international conference on knowledge discovery
    and data mining, pp. 59-68. ACM, 2015.


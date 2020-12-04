# KappaT

Kappa-T score.

The Kappa-T measures the temporal correlation between samples. It is defined as 

$$ \kappa_{t} = (p_o - p_e) / (1 - p_e) $$ 

where $p_o$ is the empirical probability of agreement on the label assigned to any sample (prequential accuracy), and $p_e$ is the prequential accuracy of the `no-change classifier` that predicts only using the last class seen by the classifier.

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

>>> y_true = ['cat', 'ant', 'cat', 'cat', 'ant', 'bird']
>>> y_pred = ['ant', 'ant', 'cat', 'cat', 'ant', 'cat']

>>> metric = metrics.KappaT()

>>> for yt, yp in zip(y_true, y_pred):
...     metric = metric.update(yt, yp)

>>> metric
KappaT: 0.6
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

[^1]: A. Bifet et al. (2013). "Pitfalls in benchmarking data stream classification
    and how to avoid them." Proc. of the European Conference on Machine Learning
    and Principles and Practice of Knowledge Discovery in Databases (ECMLPKDD'13),
    Springer LNAI 8188, p. 465-479.


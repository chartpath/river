# CohenKappa

Cohen's Kappa score.

Cohen's Kappa expresses the level of agreement between two annotators on a classification problem. It is defined as 

$$ \kappa = (p_o - p_e) / (1 - p_e) $$ 

where $p_o$ is the empirical probability of agreement on the label assigned to any sample (prequential accuracy), and $p_e$ is the expected agreement when both annotators assign labels randomly.

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

>>> metric = metrics.CohenKappa()

>>> for yt, yp in zip(y_true, y_pred):
...     metric = metric.update(yt, yp)

>>> metric
CohenKappa: 0.428571
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

[^1]: J. Cohen (1960). "A coefficient of agreement for nominal scales". Educational and Psychological Measurement 20(1):37-46. doi:10.1177/001316446002000104.


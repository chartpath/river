# Jaccard

Jaccard index for binary multi-outputs.

The Jaccard index, or Jaccard similarity coefficient, defined as the size of the intersection divided by the size of the union of two label sets, is used to compare the set of predicted labels for a sample with the corresponding set of labels in `y_true`. 

The Jaccard index may be a poor metric if there are no positives for some samples or labels. The Jaccard index is undefined if there are no true or predicted labels, this implementation will return a score of 0.0 if this is the case.

## Parameters

- **cm** – defaults to `None`

    This parameter allows sharing the same confusion matrix between multiple metrics. Sharing a confusion matrix reduces the amount of storage and computation time.


## Attributes

- **bigger_is_better**

    Indicates if a high value is better than a low one or not.

- **requires_labels**

- **sample_correction**


## Examples

```python
>>> from river import metrics

>>> y_true = [
...     {0: False, 1: True, 2: True},
...     {0: True, 1: True, 2: False},
... ]

>>> y_pred = [
...     {0: True, 1: True, 2: True},
...     {0: True, 1: False, 2: False},
... ]

>>> jac = metrics.Jaccard()
>>> for yt, yp in zip(y_true, y_pred):
...     jac = jac.update(yt, yp)

>>> jac
Jaccard: 0.583333
```

## Methods

???- note "get"

    Return the current value of the metric.

    
???- note "revert"

    Revert the metric.

    **Parameters**

    - **y_true**     (*Dict[Union[str, int], Union[bool, str, int]]*)    
    - **y_pred**     (*Union[Dict[Union[str, int], Union[bool, str, int]], Dict[Union[str, int], Dict[Union[bool, str, int], float]]]*)    
    - **sample_weight**     (*numbers.Number*)     – defaults to `1.0`    
    - **correction**     – defaults to `None`    
    
???- note "update"

    Update the metric.

    **Parameters**

    - **y_true**     (*Dict[Union[str, int], Union[bool, str, int]]*)    
    - **y_pred**     (*Union[Dict[Union[str, int], Union[bool, str, int]], Dict[Union[str, int], Dict[Union[bool, str, int], float]]]*)    
    - **sample_weight**     (*numbers.Number*)     – defaults to `1.0`    
    
???- note "works_with"

    Indicates whether or not a metric can work with a given model.

    **Parameters**

    - **model**     (*river.base.estimator.Estimator*)    
    
## References

[^1]: [Wikipedia section on similarity of asymmetric binary attributes](https://www.wikiwand.com/en/Jaccard_index#/Similarity_of_asymmetric_binary_attributes)


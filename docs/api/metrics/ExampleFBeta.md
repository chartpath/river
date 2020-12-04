# ExampleFBeta

Example-based F-Beta score.



## Parameters

- **beta** (*float*)

    Weight of precision in the harmonic mean.

- **cm** – defaults to `None`

    This parameter allows sharing the same confusion matrix between multiple metrics. Sharing a confusion matrix reduces the amount of storage and computation time.


## Attributes

- **precision** (*metrics.ExamplePrecision*)

- **recall** (*metrics.ExampleRecall*)


## Examples

```python
>>> from river import metrics

>>> y_true = [
...     {0: False, 1: True, 2: True},
...     {0: True, 1: True, 2: False},
...     {0: True, 1: True, 2: False},
... ]

>>> y_pred = [
...     {0: True, 1: True, 2: True},
...     {0: True, 1: False, 2: False},
...     {0: True, 1: True, 2: False},
... ]

>>> metric = metrics.ExampleFBeta(beta=2)
>>> for yt, yp in zip(y_true, y_pred):
...     metric = metric.update(yt, yp)

>>> metric
ExampleFBeta: 0.843882
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
    

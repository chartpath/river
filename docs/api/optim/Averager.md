# Averager

Averaged stochastic gradient descent.

This is a wrapper that can be applied to any stochastic gradient descent optimiser. Note that this implementation differs than what may be found elsewhere. Essentially, the average of the weights is usually only used at the end of the optimisation, once all the data has been seen. However, in this implementation the optimiser returns the current averaged weights.

## Parameters

- **optimizer** (*[optim.Optimizer](../../optim/Optimizer)*)

    An optimizer for which the produced weights will be averaged.

- **start** (*int*) – defaults to `0`

    Indicates the number of iterations to wait before starting the average. Essentially, nothing happens differently before the number of iterations reaches this value.


## Attributes

- **learning_rate**


## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import linear_model
>>> from river import metrics
>>> from river import optim
>>> from river import preprocessing

>>> dataset = datasets.Phishing()
>>> optimizer = optim.Averager(optim.SGD(0.01), 100)
>>> model = (
...     preprocessing.StandardScaler() |
...     linear_model.LogisticRegression(optimizer)
... )
>>> metric = metrics.F1()

>>> evaluate.progressive_val_score(dataset, model, metric)
F1: 0.878924
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "update_after_pred"

    Updates a weight vector given a gradient.

    Parameters:     w (dict): A dictionary of weight parameters. The weights are modified in-place.     g (dict): A dictionary of gradients.  Returns:     The updated weights.

    **Parameters**

    - **w**     (*dict*)    
    - **g**     (*dict*)    
    
???- note "update_before_pred"

    Updates a weight vector before a prediction is made.

    Parameters:     w (dict): A dictionary of weight parameters. The weights are modified in-place.  Returns:     The updated weights.

    **Parameters**

    - **w**     (*dict*)    
    
## References

[^1]: [Bottou, L., 2010. Large-scale machine learning with stochastic gradient descent. In Proceedings of COMPSTAT'2010 (pp. 177-186). Physica-Verlag HD.](https://leon.bottou.org/publications/pdf/compstat-2010.pdf)
[^2]: [Stochastic Algorithms for One-Pass Learning slides by Léon Bottou](https://leon.bottou.org/slides/onepass/onepass.pdf)
[^3]: [Xu, W., 2011. Towards optimal one pass large scale learning with averaged stochastic gradient descent. arXiv preprint arXiv:1107.2490.](https://arxiv.org/pdf/1107.2490.pdf)


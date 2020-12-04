# Adam

Adam optimizer.



## Parameters

- **lr** – defaults to `0.1`

- **beta_1** – defaults to `0.9`

- **beta_2** – defaults to `0.999`

- **eps** – defaults to `1e-08`


## Attributes

- **m** (*collections.defaultdict*)

- **v** (*collections.defaultdict*)


## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import linear_model
>>> from river import metrics
>>> from river import optim
>>> from river import preprocessing

>>> dataset = datasets.Phishing()
>>> optimizer = optim.Adam()
>>> model = (
...     preprocessing.StandardScaler() |
...     linear_model.LogisticRegression(optimizer)
... )
>>> metric = metrics.F1()

>>> evaluate.progressive_val_score(dataset, model, metric)
F1: 0.86496
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

[^1]: [Kingma, D.P. and Ba, J., 2014. Adam: A method for stochastic optimization. arXiv preprint arXiv:1412.6980.](https://arxiv.org/pdf/1412.6980.pdf)


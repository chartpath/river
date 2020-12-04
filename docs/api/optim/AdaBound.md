# AdaBound

AdaBound optimizer.



## Parameters

- **lr** – defaults to `0.001`

    The learning rate.

- **beta_1** – defaults to `0.9`

- **beta_2** – defaults to `0.999`

- **eps** – defaults to `1e-08`

- **gamma** – defaults to `0.001`

- **final_lr** – defaults to `0.1`


## Attributes

- **m** (*collections.defaultdict*)

- **s** (*collections.defaultdict*)


## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import linear_model
>>> from river import metrics
>>> from river import optim
>>> from river import preprocessing

>>> dataset = datasets.Phishing()
>>> optimizer = optim.AdaBound()
>>> model = (
...     preprocessing.StandardScaler() |
...     linear_model.LogisticRegression(optimizer)
... )
>>> metric = metrics.F1()

>>> evaluate.progressive_val_score(dataset, model, metric)
F1: 0.879004
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

[^1]: [Luo, L., Xiong, Y., Liu, Y. and Sun, X., 2019. Adaptive gradient methods with dynamic bound of learning rate. arXiv preprint arXiv:1902.09843](https://arxiv.org/abs/1902.09843)


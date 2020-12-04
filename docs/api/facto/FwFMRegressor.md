# FwFMRegressor

Field-weighted Factorization Machine for regression.

The model equation is defined as: 

$$\hat{y}(x) = w_{0} + \sum_{j=1}^{p} w_{j} x_{j}  + \sum_{j=1}^{p} \sum_{j'=j+1}^{p} r_{f_j, f_{j'}} \langle \mathbf{v}_j, \mathbf{v}_{j'} \rangle x_{j} x_{j'}$$ 

Where $f_j$ and $f_{j'}$ are $j$ and $j'$ fields, respectively, and $\mathbf{v}_j$ and $\mathbf{v}_{j'}$ are $j$ and $j'$ latent vectors, respectively. 

For more efficiency, this model automatically one-hot encodes strings features considering them as categorical variables. Field names are inferred from feature names by taking everything before the first underscore: `feature_name.split('_')[0]`.

## Parameters

- **n_factors** – defaults to `10`

    Dimensionality of the factorization or number of latent factors.

- **weight_optimizer** (*[optim.Optimizer](../../optim/Optimizer)*) – defaults to `None`

    The sequential optimizer used for updating the feature weights. Note that the intercept is handled separately.

- **latent_optimizer** (*[optim.Optimizer](../../optim/Optimizer)*) – defaults to `None`

    The sequential optimizer used for updating the latent factors.

- **int_weight_optimizer** (*[optim.Optimizer](../../optim/Optimizer)*) – defaults to `None`

    The sequential optimizer used for updating the field pairs interaction weights.

- **loss** (*[optim.losses.RegressionLoss](../../optim/losses/RegressionLoss)*) – defaults to `None`

    The loss function to optimize for.

- **sample_normalization** – defaults to `False`

    Whether to divide each element of `x` by `x`'s L2-norm.

- **l1_weight** – defaults to `0.0`

    Amount of L1 regularization used to push weights towards 0.

- **l2_weight** – defaults to `0.0`

    Amount of L2 regularization used to push weights towards 0.

- **l1_latent** – defaults to `0.0`

    Amount of L1 regularization used to push latent weights towards 0.

- **l2_latent** – defaults to `0.0`

    Amount of L2 regularization used to push latent weights towards 0.

- **intercept** – defaults to `0.0`

    Initial intercept value.

- **intercept_lr** (*Union[[optim.schedulers.Scheduler](../../optim/schedulers/Scheduler), float]*) – defaults to `0.01`

    Learning rate scheduler used for updating the intercept. An instance of `optim.schedulers.Constant` is used if a `float` is passed. No intercept will be used if this is set to 0.

- **weight_initializer** (*[optim.initializers.Initializer](../../optim/initializers/Initializer)*) – defaults to `None`

    Weights initialization scheme. Defaults to `optim.initializers.Zeros()`.

- **latent_initializer** (*[optim.initializers.Initializer](../../optim/initializers/Initializer)*) – defaults to `None`

    Latent factors initialization scheme. Defaults to `optim.initializers.Normal(mu=.0, sigma=.1, random_state=self.random_state)`.

- **clip_gradient** – defaults to `1000000000000.0`

    Clips the absolute value of each gradient value.

- **seed** (*int*) – defaults to `None`

    Randomization seed used for reproducibility.


## Attributes

- **weights**

    The current weights assigned to the features.

- **latents**

    The current latent weights assigned to the features.

- **interaction_weights**

    The current interaction strengths of field pairs.


## Examples

```python
>>> from river import facto

>>> dataset = (
...     ({'user': 'Alice', 'item': 'Superman'}, 8),
...     ({'user': 'Alice', 'item': 'Terminator'}, 9),
...     ({'user': 'Alice', 'item': 'Star Wars'}, 8),
...     ({'user': 'Alice', 'item': 'Notting Hill'}, 2),
...     ({'user': 'Alice', 'item': 'Harry Potter '}, 5),
...     ({'user': 'Bob', 'item': 'Superman'}, 8),
...     ({'user': 'Bob', 'item': 'Terminator'}, 9),
...     ({'user': 'Bob', 'item': 'Star Wars'}, 8),
...     ({'user': 'Bob', 'item': 'Notting Hill'}, 2)
... )

>>> model = facto.FwFMRegressor(
...     n_factors=10,
...     intercept=5,
...     seed=42,
... )

>>> for x, y in dataset:
...     model = model.learn_one(x, y)

>>> model.predict_one({'Bob': 1, 'Harry Potter': 1})
5.236501
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Fits to a set of features `x` and a real-valued target `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*numbers.Number*)    
    - **sample_weight**     – defaults to `1.0`    
    
    **Returns**

    *Regressor*:     self
    
???- note "predict_one"

    Predicts the target value of a set of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    The prediction.
    
## References

[^1]: [Junwei Pan, Jian Xu, Alfonso Lobos Ruiz, Wenliang Zhao, Shengjun Pan, Yu Sun, and Quan Lu, 2018, April. Field-weighted Factorization Machines for Click-Through Rate Prediction in Display Advertising. In Proceedings of the 2018 World Wide Web Conference on World Wide Web. International World Wide Web Conferences Steering Committee, (pp. 1349–1357).](https://arxiv.org/abs/1806.03514)


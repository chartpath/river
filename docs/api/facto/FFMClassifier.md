# FFMClassifier

Field-aware Factorization Machine for binary classification.

The model equation is defined by: 

$$\hat{y}(x) = w_{0} + \sum_{j=1}^{p} w_{j} x_{j}  + \sum_{j=1}^{p} \sum_{j'=j+1}^{p} \langle \mathbf{v}_{j, f_{j'}}, \mathbf{v}_{j', f_j} \rangle x_{j} x_{j'}$$ 

Where \mathbf{v}_{j, f_{j'}} is the latent vector corresponding to $j$ feature for $f_{j'}$ field, and \mathbf{v}_{j', f_j} is the latent vector corresponding to $j'$ feature for $f_j$ field. 

For more efficiency, this model automatically one-hot encodes strings features considering them as categorical variables. Field names are inferred from feature names by taking everything before the first underscore: `feature_name.split('_')[0]`.

## Parameters

- **n_factors** – defaults to `10`

    Dimensionality of the factorization or number of latent factors.

- **weight_optimizer** (*[optim.Optimizer](../../optim/Optimizer)*) – defaults to `None`

    The sequential optimizer used for updating the feature weights. Note that the intercept is handled separately.

- **latent_optimizer** (*[optim.Optimizer](../../optim/Optimizer)*) – defaults to `None`

    The sequential optimizer used for updating the latent factors.

- **loss** (*[optim.losses.BinaryLoss](../../optim/losses/BinaryLoss)*) – defaults to `None`

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


## Examples

```python
>>> from river import facto

>>> dataset = (
...     ({'user': 'Alice', 'item': 'Superman', 'time': .12}, True),
...     ({'user': 'Alice', 'item': 'Terminator', 'time': .13}, True),
...     ({'user': 'Alice', 'item': 'Star Wars', 'time': .14}, True),
...     ({'user': 'Alice', 'item': 'Notting Hill', 'time': .15}, False),
...     ({'user': 'Alice', 'item': 'Harry Potter ', 'time': .16}, True),
...     ({'user': 'Bob', 'item': 'Superman', 'time': .13}, True),
...     ({'user': 'Bob', 'item': 'Terminator', 'time': .12}, True),
...     ({'user': 'Bob', 'item': 'Star Wars', 'time': .16}, True),
...     ({'user': 'Bob', 'item': 'Notting Hill', 'time': .10}, False)
... )

>>> model = facto.FFMClassifier(
...     n_factors=10,
...     intercept=.5,
...     seed=42,
... )

>>> for x, y in dataset:
...     model = model.learn_one(x, y)

>>> model.predict_one({'user': 'Bob', 'item': 'Harry Potter', 'time': .14})
True
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update the model with a set of features `x` and a label `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*Union[bool, str, int]*)    
    - **sample_weight**     – defaults to `1.0`    
    
    **Returns**

    *Classifier*:     self
    
???- note "predict_one"

    Predict the label of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Union[bool, str, int]*:     The predicted label.
    
???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    A dictionary that associates a probability which each label.
    
## References

1. [Juan, Y., Zhuang, Y., Chin, W.S. and Lin, C.J., 2016, September. Field-aware factorization machines for CTR prediction. In Proceedings of the 10th ACM Conference on Recommender Systems (pp. 43-50).](https://www.csie.ntu.edu.tw/~cjlin/papers/ffm.pdf)


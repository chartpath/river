# FunkMF

Funk Matrix Factorization for recommender systems.

The model equation is defined as: 

$$\hat{y}(x) = \langle \mathbf{v}_u, \mathbf{v}_i \rangle = \sum_{f=1}^{k} \mathbf{v}_{u, f} \cdot \mathbf{v}_{i, f}$$ 

where $k$ is the number of latent factors. 

This model expects a dict input with a `user` and an `item` entries without any type constraint on their values (i.e. can be strings or numbers). Other entries are ignored.

## Parameters

- **n_factors** – defaults to `10`

    Dimensionality of the factorization or number of latent factors.

- **optimizer** (*[optim.Optimizer](../../optim/Optimizer)*) – defaults to `None`

    The sequential optimizer used for updating the latent factors.

- **loss** (*[optim.losses.Loss](../../optim/losses/Loss)*) – defaults to `None`

    The loss function to optimize for.

- **l2** – defaults to `0.0`

    Amount of L2 regularization used to push weights towards 0.

- **initializer** (*[optim.initializers.Initializer](../../optim/initializers/Initializer)*) – defaults to `None`

    Latent factors initialization scheme.

- **clip_gradient** – defaults to `1000000000000.0`

    Clips the absolute value of each gradient value.

- **seed** (*int*) – defaults to `None`

    Randomization seed used for reproducibility.


## Attributes

- **u_latents** (*collections.defaultdict*)

    The user latent vectors randomly initialized.

- **i_latents** (*collections.defaultdict*)

    The item latent vectors randomly initialized.

- **u_optimizer** (*optim.Optimizer*)

    The sequential optimizer used for updating the user latent weights.

- **i_optimizer** (*optim.Optimizer*)

    The sequential optimizer used for updating the item latent weights.


## Examples

```python
>>> from river import optim
>>> from river import reco

>>> dataset = (
...     ({'user': 'Alice', 'item': 'Superman'}, 8),
...     ({'user': 'Alice', 'item': 'Terminator'}, 9),
...     ({'user': 'Alice', 'item': 'Star Wars'}, 8),
...     ({'user': 'Alice', 'item': 'Notting Hill'}, 2),
...     ({'user': 'Alice', 'item': 'Harry Potter'}, 5),
...     ({'user': 'Bob', 'item': 'Superman'}, 8),
...     ({'user': 'Bob', 'item': 'Terminator'}, 9),
...     ({'user': 'Bob', 'item': 'Star Wars'}, 8),
...     ({'user': 'Bob', 'item': 'Notting Hill'}, 2)
... )

>>> model = reco.FunkMF(
...     n_factors=10,
...     optimizer=optim.SGD(0.1),
...     initializer=optim.initializers.Normal(mu=0., sigma=0.1, seed=11),
... )

>>> for x, y in dataset:
...     _ = model.learn_one(x, y)

>>> model.predict_one({'user': 'Bob', 'item': 'Harry Potter'})
1.866272
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
    
    **Returns**

    *Regressor*:     self
    
???- note "predict_one"

    Predicts the target value of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *Number*:     The prediction.
    
## References

[^1]: [Netflix update: Try this at home](https://sifter.org/simon/journal/20061211.html)
[^2]: [Matrix factorization techniques for recommender systems](https://datajobs.com/data-science-repo/Recommender-Systems-[Netflix].pdf)


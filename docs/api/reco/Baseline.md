# Baseline

Baseline for recommender systems.

A first-order approximation of the bias involved in target. The model equation is defined as: 

$$\hat{y}(x) = \bar{y} + bu_{u} + bi_{i}$$ 

Where $bu_{u}$ and $bi_{i}$ are respectively the user and item biases. 

This model expects a dict input with a `user` and an `item` entries without any type constraint on their values (i.e. can be strings or numbers). Other entries are ignored.

## Parameters

- **optimizer** (*[optim.Optimizer](../../optim/Optimizer)*) – defaults to `None`

    The sequential optimizer used for updating the weights.

- **loss** (*[optim.losses.Loss](../../optim/losses/Loss)*) – defaults to `None`

    The loss function to optimize for.

- **l2** – defaults to `0.0`

    regularization amount used to push weights towards 0.

- **initializer** (*[optim.initializers.Initializer](../../optim/initializers/Initializer)*) – defaults to `None`

    Weights initialization scheme.

- **clip_gradient** – defaults to `1000000000000.0`

    Clips the absolute value of each gradient value.


## Attributes

- **global_mean** (*stats.Mean*)

    The target arithmetic mean.

- **u_biases** (*collections.defaultdict*)

    The user bias weights.

- **i_biases** (*collections.defaultdict*)

    The item bias weights.

- **u_optimizer** (*optim.Optimizer*)

    The sequential optimizer used for updating the user bias weights.

- **i_optimizer** (*optim.Optimizer*)

    The sequential optimizer used for updating the item bias weights.


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

>>> model = reco.Baseline(optimizer=optim.SGD(0.005))

>>> for x, y in dataset:
...     _ = model.learn_one(x, y)

>>> model.predict_one({'user': 'Bob', 'item': 'Harry Potter'})
6.538120
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

[^1]: [Matrix factorization techniques for recommender systems](https://datajobs.com/data-science-repo/Recommender-Systems-[Netflix].pdf)


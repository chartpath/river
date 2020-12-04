# RandomNormal

Predicts random values sampled from a normal distribution.

The parameters of the normal distribution are fitted with running statistics. This is equivalent to using `surprise.prediction_algorithms.random_pred.NormalPredictor`. 

This model expects a dict input with a `user` and an `item` entries without any type constraint on their values (i.e. can be strings or numbers). Other entries are ignored.

## Parameters

- **seed** – defaults to `None`

    Randomization seed used for reproducibility.


## Attributes

- **mean**

    stats.Mean

- **variance**

    stats.Var


## Examples

```python
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

>>> model = reco.RandomNormal(seed=42)

>>> for x, y in dataset:
...     _ = model.learn_one(x, y)

>>> model.predict_one({'user': 'Bob', 'item': 'Harry Potter'})
6.883895
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
    

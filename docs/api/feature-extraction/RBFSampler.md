# RBFSampler

Extracts random features which approximate an RBF kernel.

This is a powerful way to give non-linear capacity to linear classifiers. This method is also called "random Fourier features" in the literature.

## Parameters

- **gamma** – defaults to `1.0`

    RBF kernel parameter in `(-gamma * x^2)`.

- **n_components** – defaults to `100`

    Number of samples per original feature. Equals the dimensionality of the computed feature space.

- **seed** (*int*) – defaults to `None`

    Random number seed.



## Examples

```python
>>> from river import feature_extraction as fx
>>> from river import linear_model as lm
>>> from river import optim
>>> from river import stream

>>> # XOR function
>>> X = [[0, 0], [1, 1], [1, 0], [0, 1]]
>>> Y = [0, 0, 1, 1]

>>> model = lm.LogisticRegression(optimizer=optim.SGD(.1))

>>> for x, y in stream.iter_array(X, Y):
...     model = model.learn_one(x, y)
...     y_pred = model.predict_one(x)
...     print(y, int(y_pred))
0 0
0 0
1 0
1 1

>>> model = (
...     fx.RBFSampler(seed=3) |
...     lm.LogisticRegression(optimizer=optim.SGD(.1))
... )

>>> for x, y in stream.iter_array(X, Y):
...     model = model.learn_one(x, y)
...     y_pred = model.predict_one(x)
...     print(y, int(y_pred))
0 0
0 0
1 1
1 1
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update with a set of features `x`.

    A lot of transformers don't actually have to do anything during the `learn_one` step because they are stateless. For this reason the default behavior of this function is to do nothing. Transformers that however do something during the `learn_one` can override this method.

    **Parameters**

    - **x**     (*dict*)    
    - **kwargs**    
    
    **Returns**

    *Transformer*:     self
    
???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     – defaults to `None`    
    
    **Returns**

    *dict*:     The transformed values.
    
## References

[^1]: [Rahimi, A. and Recht, B., 2008. Random features for large-scale kernel machines. In Advances in neural information processing systems (pp. 1177-1184](https://people.eecs.berkeley.edu/~brecht/papers/07.rah.rec.nips.pdf)


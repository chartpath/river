# Normalizer

Scales a set of features so that it has unit norm.

This is particularly useful when used after a `feature_extraction.TFIDF`.

## Parameters

- **order** – defaults to `2`

    Order of the norm (e.g. 2 corresponds to the $L^2$ norm).



## Examples

```python
>>> from river import preprocessing
>>> from river import stream

>>> scaler = preprocessing.Normalizer(order=2)

>>> X = [[4, 1, 2, 2],
...      [1, 3, 9, 3],
...      [5, 7, 5, 1]]

>>> for x, _ in stream.iter_array(X):
...     print(scaler.transform_one(x))
{0: 0.8, 1: 0.2, 2: 0.4, 3: 0.4}
{0: 0.1, 1: 0.3, 2: 0.9, 3: 0.3}
{0: 0.5, 1: 0.7, 2: 0.5, 3: 0.1}
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
    
    **Returns**

    *dict*:     The transformed values.
    

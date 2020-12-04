# FeatureHasher

Implements the hashing trick.

Each pair of (name, value) features is hashed into a random integer. A module operator is then used to make sure the hash is in a certain range. We use the Murmurhash implementation from scikit-learn.

## Parameters

- **n_features** – defaults to `1048576`

    The number by which each hash will be moduloed by.

- **seed** (*int*) – defaults to `None`

    Set the seed to produce identical results.



## Examples

```python
>>> import river

>>> hasher = river.preprocessing.FeatureHasher(n_features=10, seed=42)

>>> X = [
...     {'dog': 1, 'cat': 2, 'elephant': 4},
...     {'dog': 2, 'run': 5}
... ]
>>> for x in X:
...     print(hasher.transform_one(x))
Counter({1: 4, 9: 2, 8: 1})
Counter({4: 5, 8: 2})
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
    
## References

[^1]: [Wikipedia article on feature vectorization using the hashing trick](https://www.wikiwand.com/en/Feature_hashing#/Feature_vectorization_using_hashing_trick)


# VarianceThreshold

Removes low-variance features.



## Parameters

- **threshold** – defaults to `0`

    Only features with a variance above the threshold will be kept.

- **min_samples** – defaults to `2`

    The minimum number of samples required to perform selection.


## Attributes

- **variances** (*dict*)

    The variance of each feature.


## Examples

```python
>>> from river import feature_selection
>>> from river import stream

>>> X = [
...     [0, 2, 0, 3],
...     [0, 1, 4, 3],
...     [0, 1, 1, 3]
... ]

>>> selector = feature_selection.VarianceThreshold()

>>> for x, _ in stream.iter_array(X):
...     print(selector.learn_one(x).transform_one(x))
{0: 0, 1: 2, 2: 0, 3: 3}
{1: 1, 2: 4}
{1: 1, 2: 1}
```

## Methods

???- note "check_feature"

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update with a set of features `x`.

    A lot of transformers don't actually have to do anything during the `learn_one` step because they are stateless. For this reason the default behavior of this function is to do nothing. Transformers that however do something during the `learn_one` can override this method.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *Transformer*:     self
    
???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *dict*:     The transformed values.
    

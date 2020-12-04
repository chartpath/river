# MaxAbsScaler

Scales the data to a [-1, 1] range based on absolute maximum.

Under the hood a running absolute max is maintained. This scaler is meant for data that is already centered at zero or sparse data. It does not shift/center the data, and thus does not destroy any sparsity.


## Attributes

- **abs_max** (*dict*)

    Mapping between features and instances of `stats.AbsMax`.


## Examples

```python
>>> from pprint import pprint
>>> import random
>>> from river import preprocessing

>>> random.seed(42)
>>> X = [{'x': random.uniform(8, 12)} for _ in range(5)]
>>> pprint(X)
[{'x': 10.557707},
    {'x': 8.100043},
    {'x': 9.100117},
    {'x': 8.892842},
    {'x': 10.945884}]

>>> scaler = preprocessing.MaxAbsScaler()

>>> for x in X:
...     print(scaler.learn_one(x).transform_one(x))
{'x': 1.0}
{'x': 0.767216}
{'x': 0.861940}
{'x': 0.842308}
{'x': 1.0}
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
    
    **Returns**

    *Transformer*:     self
    
???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *dict*:     The transformed values.
    

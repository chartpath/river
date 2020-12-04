# RobustScaler

Scale features using statistics that are robust to outliers.

This Scaler removes the median and scales the data according to the interquantile range.

## Parameters

- **with_centering** – defaults to `True`

    Whether to centre the data before scaling.

- **with_scaling** – defaults to `True`

    Whether to scale data to IQR.

- **q_inf** – defaults to `0.25`

    Desired inferior quantile, must be between 0 and 1.

- **q_sup** – defaults to `0.75`

    Desired superior quantile, must be between 0 and 1.


## Attributes

- **median** (*dict*)

    Mapping between features and instances of `stats.Quantile(0.5)`.

- **iqr** (*dict*)

    Mapping between features and instances of `stats.IQR`.


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

>>> scaler = preprocessing.RobustScaler()

>>> for x in X:
...     print(scaler.learn_one(x).transform_one(x))
{'x': 0.0}
{'x': -1.0}
{'x': 0.0}
{'x': -0.124499}
{'x': 1.108659}
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
    

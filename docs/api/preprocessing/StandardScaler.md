# StandardScaler

Scales the data so that it has zero mean and unit variance.

Under the hood, a running mean and a running variance are maintained. The scaling is slightly different than when scaling the data in batch because the exact means and variances are not known in advance. However, this doesn't have a detrimental impact on performance in the long run. 

This transformer supports mini-batches as well as single instances. In the mini-batch case, the number of columns and the ordering of the columns are allowed to change between subsequent calls. In other words, this transformer will keep working even if you add and/or remove features every time you call `learn_many` and `transform_many`.



## Examples

```python
>>> from pprint import pprint
>>> import random
>>> from river import preprocessing

>>> random.seed(42)
>>> X = [{'x': random.uniform(8, 12), 'y': random.uniform(8, 12)} for _ in range(6)]
>>> pprint(X)
[{'x': 10.557, 'y': 8.100},
    {'x': 9.100, 'y': 8.892},
    {'x': 10.945, 'y': 10.706},
    {'x': 11.568, 'y': 8.347},
    {'x': 9.687, 'y': 8.119},
    {'x': 8.874, 'y': 10.021}]

>>> scaler = preprocessing.StandardScaler()

>>> for x in X:
...     print(scaler.learn_one(x).transform_one(x))
{'x': 0.0, 'y': 0.0}
{'x': -0.999, 'y': 0.999}
{'x': 0.937, 'y': 1.350}
{'x': 1.129, 'y': -0.651}
{'x': -0.776, 'y': -0.729}
{'x': -1.274, 'y': 0.992}

```

This transformer also supports mini-batch updates. You can call `learn_many` and provide a
`pandas.DataFrame`:

```python
>>> import pandas as pd
>>> X = pd.DataFrame.from_dict(X)

>>> scaler = preprocessing.StandardScaler()
>>> scaler = scaler.learn_many(X[:3])
>>> scaler = scaler.learn_many(X[3:])

```

You can then call `transform_many` to scale a mini-batch of features:

```python
>>> scaler.transform_many(X)
    x         y
0  0.444600 -0.933384
1 -1.044259 -0.138809
2  0.841106  1.679208
3  1.477301 -0.685117
4 -0.444084 -0.914195
5 -1.274664  0.992296
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_many"

    Update with a mini-batch of features.

    Note that the update formulas for mean and variance are slightly different than in the single instance case, but they produce exactly the same result.

    **Parameters**

    - **X**     (*pandas.core.frame.DataFrame*)    
    
???- note "learn_one"

    Update with a set of features `x`.

    A lot of transformers don't actually have to do anything during the `learn_one` step because they are stateless. For this reason the default behavior of this function is to do nothing. Transformers that however do something during the `learn_one` can override this method.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *Transformer*:     self
    
???- note "transform_many"

    Scale a mini-batch of features.

    **Parameters**

    - **X**     (*pandas.core.frame.DataFrame*)    
    
???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *dict*:     The transformed values.
    
## References

[^1]: [Welford's Method (and Friends)](https://www.embeddedrelated.com/showarticle/785.php)
[^2]: [Batch updates for simple statistics](https://notmatthancock.github.io/2017/03/23/simple-batch-stat-updates.html)


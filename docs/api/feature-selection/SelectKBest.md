# SelectKBest

Removes all but the $k$ highest scoring features.



## Parameters

- **similarity** (*river.stats.base.Bivariate*)

- **k** – defaults to `10`

    The number of features to keep.


## Attributes

- **similarities** (*dict*)

    The similarity instances used for each feature.

- **leaderboard** (*dict*)

    The actual similarity measures.


## Examples

```python
>>> from pprint import pprint
>>> from river import feature_selection
>>> from river import stats
>>> from river import stream
>>> from sklearn import datasets

>>> X, y = datasets.make_regression(
...     n_samples=100,
...     n_features=10,
...     n_informative=2,
...     random_state=42
... )

>>> selector = feature_selection.SelectKBest(
...     similarity=stats.PearsonCorr(),
...     k=2
... )

>>> for xi, yi, in stream.iter_array(X, y):
...     selector = selector.learn_one(xi, yi)

>>> pprint(selector.leaderboard)
Counter({9: 0.7898,
        7: 0.5444,
        8: 0.1062,
        2: 0.0638,
        4: 0.0538,
        5: 0.0271,
        1: -0.0312,
        6: -0.0657,
        3: -0.1501,
        0: -0.1895})

>>> selector.transform_one(xi)
{7: -1.2795, 9: -1.8408}
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update with a set of features `x` and a target `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*Union[bool, str, int, numbers.Number]*)    
    
    **Returns**

    *SupervisedTransformer*:     self
    
???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *dict*:     The transformed values.
    

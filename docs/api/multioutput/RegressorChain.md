# RegressorChain

A multi-output model that arranges regressor into a chain.

This will create one model per output. The prediction of the first output will be used as a feature in the second output. The prediction for the second output will be used as a feature for the third, etc. This "chain model" is therefore capable of capturing dependencies between outputs.

## Parameters

- **model** (*[base.Regressor](../../base/Regressor)*)

- **order** (*list*) – defaults to `None`

    A list with the targets order in which to construct the chain. If `None` then the order will be inferred from the order of the keys in the first provided target dictionary. If `'random'` then the order is set at random.

- **seed** (*int*) – defaults to `None`

    Random number generator seed for reproducibility. Only relevant in `order='random'`.



## Examples

```python
>>> from river import evaluate
>>> from river import linear_model
>>> from river import metrics
>>> from river import multioutput
>>> from river import preprocessing
>>> from river import stream
>>> from sklearn import datasets

>>> dataset = stream.iter_sklearn_dataset(
...     dataset=datasets.load_linnerud(),
...     shuffle=True,
...     seed=42
... )

>>> model = multioutput.RegressorChain(
...     model=(
...         preprocessing.StandardScaler() |
...         linear_model.LinearRegression(intercept_lr=0.3)
...     ),
...     order=[0, 1, 2]
... )

>>> metric = metrics.RegressionMultiOutput(metrics.MAE())

>>> evaluate.progressive_val_score(dataset, model, metric)
MAE: 16.396347
```

## Methods

???- note "clear"

    D.clear() -> None.  Remove all items from D.

    
???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "copy"

???- note "fromkeys"

???- note "get"

    D.get(k[,d]) -> D[k] if k in D, else d.  d defaults to None.

    **Parameters**

    - **key**    
    - **default**     – defaults to `None`    
    
???- note "items"

    D.items() -> a set-like object providing a view on D's items

    
???- note "keys"

    D.keys() -> a set-like object providing a view on D's keys

    
???- note "learn_one"

    Fits to a set of features `x` and a real-valued target `y`.

    **Parameters**

    - **x**    
    - **y**    
    
    **Returns**

    self
    
???- note "pop"

    D.pop(k[,d]) -> v, remove specified key and return the corresponding value. If key is not found, d is returned if given, otherwise KeyError is raised.

    **Parameters**

    - **key**    
    - **default**     – defaults to `<object object at 0x110022150>`    
    
???- note "popitem"

    D.popitem() -> (k, v), remove and return some (key, value) pair as a 2-tuple; but raise KeyError if D is empty.

    
???- note "predict_one"

    Predicts the target value of a set of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    The prediction.
    
???- note "setdefault"

    D.setdefault(k[,d]) -> D.get(k,d), also set D[k]=d if k not in D

    **Parameters**

    - **key**    
    - **default**     – defaults to `None`    
    
???- note "update"

    D.update([E, ]**F) -> None.  Update D from mapping/iterable E and F. If E present and has a .keys() method, does:     for k in E: D[k] = E[k] If E present and lacks .keys() method, does:     for (k, v) in E: D[k] = v In either case, this is followed by: for k, v in F.items(): D[k] = v

    **Parameters**

    - **other**     – defaults to `()`    
    - **kwds**    
    
???- note "values"

    D.values() -> an object providing a view on D's values

    

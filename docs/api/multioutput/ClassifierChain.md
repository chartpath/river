# ClassifierChain

A multi-output model that arranges classifiers into a chain.

This will create one model per output. The prediction of the first output will be used as a feature in the second output. The prediction for the second output will be used as a feature for the third, etc. This "chain model" is therefore capable of capturing dependencies between outputs.

## Parameters

- **model** (*[base.Classifier](../../base/Classifier)*)

- **order** (*list*) – defaults to `None`

    A list with the targets order in which to construct the chain. If `None` then the order will be inferred from the order of the keys in the first provided target dictionary. If `'random'` then the order is set at random.

- **seed** (*int*) – defaults to `None`

    Random number generator seed for reproducibility. Only relevant in `order='random'`.



## Examples

```python
>>> from river import feature_selection
>>> from river import linear_model
>>> from river import metrics
>>> from river import multioutput
>>> from river import preprocessing
>>> from river import stream
>>> from sklearn import datasets

>>> dataset = stream.iter_sklearn_dataset(
...     dataset=datasets.fetch_openml('yeast', version=4),
...     shuffle=True,
...     seed=42
... )

>>> model = feature_selection.VarianceThreshold(threshold=0.01)
>>> model |= preprocessing.StandardScaler()
>>> model |= multioutput.ClassifierChain(
...     model=linear_model.LogisticRegression(),
...     order=list(range(14))
... )

>>> metric = metrics.Jaccard()

>>> for x, y in dataset:
...     # Convert y values to booleans
...     y = {i: yi == 'TRUE' for i, yi in y.items()}
...     y_pred = model.predict_one(x)
...     metric = metric.update(y, y_pred)
...     model = model.learn_one(x, y)

>>> metric
Jaccard: 0.451524
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

    Update the model with a set of features `x` and a label `y`.

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

    Predict the label of a set of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    The predicted label.
    
???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    A dictionary that associates a probability which each label.
    
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

    
## References

[^1]: [Multi-Output Chain Models and their Application in Data Streams](https://jmread.github.io/talks/2019_03_08-Imperial_Stats_Seminar.pdf)


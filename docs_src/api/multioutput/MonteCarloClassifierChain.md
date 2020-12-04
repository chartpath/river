# MonteCarloClassifierChain

Monte Carlo Sampling Classifier Chains.

Probabilistic Classifier Chains using Monte Carlo sampling, as described in [^1]. 

m samples are taken from the posterior distribution. Therefore we need a probabilistic interpretation of the output, and thus, this is a particular variety of ProbabilisticClassifierChain.

## Parameters

- **model** (*[base.Classifier](../../base/Classifier)*)

- **m** (*int*) – defaults to `10`

    Number of samples to take from the posterior distribution.

- **seed** (*int*) – defaults to `None`

    Random number generator seed for reproducibility.



## Examples

```python
>>> from river import feature_selection
>>> from river import linear_model
>>> from river import metrics
>>> from river import multioutput
>>> from river import preprocessing
>>> from river import synth

>>> dataset = synth.Logical(seed=42, n_tiles=100)

>>> model = multioutput.MonteCarloClassifierChain(
...     model=linear_model.LogisticRegression(),
...     m=10,
...     seed=42
... )

>>> metric = metrics.Jaccard()

>>> for x, y in dataset:
...    y_pred = model.predict_one(x)
...    metric = metric.update(y, y_pred)
...    model = model.learn_one(x, y)

>>> metric
Jaccard: 0.571846
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

[^1]: Read, J., Martino, L., & Luengo, D. (2014). Efficient monte carlo
      methods for multi-dimensional learning with classifier chains.
      Pattern Recognition, 47(3), 1535-1546.


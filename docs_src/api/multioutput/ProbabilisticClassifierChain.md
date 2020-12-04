# ProbabilisticClassifierChain

Probabilistic Classifier Chains.

The Probabilistic Classifier Chains (PCC) [^1] is a Bayes-optimal method based on the Classifier Chains (CC). 

Consider the concept of chaining classifiers as searching a path in a binary tree whose leaf nodes are associated with a label $y \in Y$. While CC searches only a single path in the aforementioned binary tree, PCC looks at each of the $2^l$ paths, where $l$ is the number of labels. This limits the applicability of the method to data sets with a small to moderate number of labels. The authors recommend no more than about 15 labels for real-world applications.

## Parameters

- **model** (*[base.Classifier](../../base/Classifier)*)



## Examples

```python
>>> from river import feature_selection
>>> from river import linear_model
>>> from river import metrics
>>> from river import multioutput
>>> from river import preprocessing
>>> from river import synth

>>> dataset = synth.Logical(seed=42, n_tiles=100)

>>> model = multioutput.ProbabilisticClassifierChain(
...     model=linear_model.LogisticRegression()
... )

>>> metric = metrics.Jaccard()

>>> for x, y in dataset:
...    y_pred = model.predict_one(x)
...    metric = metric.update(y, y_pred)
...    model = model.learn_one(x, y)

>>> metric
Jaccard: 0.573935
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

[^1]: Cheng, W., Hüllermeier, E., & Dembczynski, K. J. (2010).
      Bayes optimal multilabel classification via probabilistic classifier
      chains. In Proceedings of the 27th international conference on
      machine learning (ICML-10) (pp. 279-286).


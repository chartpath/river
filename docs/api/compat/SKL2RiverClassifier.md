# SKL2RiverClassifier

Compatibility layer from scikit-learn to River for classification.



## Parameters

- **estimator** (*sklearn.base.ClassifierMixin*)

    A scikit-learn regressor which has a `partial_fit` method.

- **classes** (*list*)



## Examples

```python
>>> from river import compat
>>> from river import evaluate
>>> from river import metrics
>>> from river import preprocessing
>>> from river import stream
>>> from sklearn import linear_model
>>> from sklearn import datasets

>>> dataset = stream.iter_sklearn_dataset(
...     dataset=datasets.load_breast_cancer(),
...     shuffle=True,
...     seed=42
... )

>>> model = preprocessing.StandardScaler()
>>> model |= compat.convert_sklearn_to_river(
...     estimator=linear_model.SGDClassifier(
...         loss='log',
...         eta0=0.01,
...         learning_rate='constant'
...     ),
...     classes=[False, True]
... )

>>> metric = metrics.LogLoss()

>>> evaluate.progressive_val_score(dataset, model, metric)
LogLoss: 0.199554
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_many"

???- note "learn_one"

    Update the model with a set of features `x` and a label `y`.

    **Parameters**

    - **x**    
    - **y**    
    
    **Returns**

    self
    
???- note "predict_many"

???- note "predict_one"

    Predict the label of a set of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    The predicted label.
    
???- note "predict_proba_many"

???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    A dictionary that associates a probability which each label.
    

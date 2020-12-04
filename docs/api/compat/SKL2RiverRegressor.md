# SKL2RiverRegressor

Compatibility layer from scikit-learn to River for regression.



## Parameters

- **estimator** (*sklearn.base.BaseEstimator*)

    A scikit-learn transformer which has a `partial_fit` method.



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
...     dataset=datasets.load_boston(),
...     shuffle=True,
...     seed=42
... )

>>> scaler = preprocessing.StandardScaler()
>>> sgd_reg = compat.convert_sklearn_to_river(linear_model.SGDRegressor())
>>> model = scaler | sgd_reg

>>> metric = metrics.MAE()

>>> evaluate.progressive_val_score(dataset, model, metric)
MAE: 11.004415
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_many"

???- note "learn_one"

    Fits to a set of features `x` and a real-valued target `y`.

    **Parameters**

    - **x**    
    - **y**    
    
    **Returns**

    self
    
???- note "predict_many"

???- note "predict_one"

    Predicts the target value of a set of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    The prediction.
    

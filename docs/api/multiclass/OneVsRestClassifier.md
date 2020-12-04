# OneVsRestClassifier

One-vs-the-rest (OvR) multiclass strategy.

This strategy consists in fitting one binary classifier per class. Because we are in a streaming context, the number of classes isn't known from the start. Hence, new classifiers are instantiated on the fly. Likewise, the predicted probabilities will only include the classes seen up to a given point in time. 

Note that this classifier supports mini-batches as well as single instances. 

The computational complexity for both learning and predicting grows linearly with the number of classes. If you have a very large number of classes, then you might want to consider using an `multiclass.OutputCodeClassifier` instead.

## Parameters

- **classifier** (*[base.Classifier](../../base/Classifier)*)

    A binary classifier, although a multi-class classifier will work too.


## Attributes

- **classifiers** (*dict*)

    A mapping between classes and classifiers.


## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import linear_model
>>> from river import metrics
>>> from river import multiclass
>>> from river import preprocessing

>>> dataset = datasets.ImageSegments()

>>> scaler = preprocessing.StandardScaler()
>>> ovr = multiclass.OneVsRestClassifier(linear_model.LogisticRegression())
>>> model = scaler | ovr

>>> metric = metrics.MacroF1()

>>> evaluate.progressive_val_score(dataset, model, metric)
MacroF1: 0.774573

```

This estimator also also supports mini-batching.

```python
>>> for X in pd.read_csv(dataset.path, chunksize=64):
...     y = X.pop('category')
...     y_pred = model.predict_many(X)
...     model = model.learn_many(X, y)
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

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Union[bool, str, int]*:     The predicted label.
    
???- note "predict_proba_many"

???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    A dictionary that associates a probability which each label.
    

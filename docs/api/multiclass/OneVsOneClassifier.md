# OneVsOneClassifier

One-vs-One (OvO) multiclass strategy.

This strategy consists in fitting one binary classifier for each pair of classes. Because we are in a streaming context, the number of classes isn't known from the start, hence new classifiers are instantiated on the fly. 

The number of classifiers is `k * (k - 1) / 2`, where `k` is the number of classes. However, each call to `learn_one` only requires training `k - 1` models. Indeed, only the models that pertain to the given label have to be trained. Meanwhile, making a prediction requires going through each and every model.

## Parameters

- **classifier**

    A binary classifier, although a multi-class classifier will work too.


## Attributes

- **classifiers** (*dict*)

    A mapping between pairs of classes and classifiers. The keys are tuples which contain a pair of classes. Each pair is sorted in lexicographical order.


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
>>> ovo = multiclass.OneVsOneClassifier(linear_model.LogisticRegression())
>>> model = scaler | ovo

>>> metric = metrics.MacroF1()

>>> evaluate.progressive_val_score(dataset, model, metric)
MacroF1: 0.807573
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update the model with a set of features `x` and a label `y`.

    **Parameters**

    - **x**    
    - **y**    
    
    **Returns**

    self
    
???- note "predict_one"

    Predict the label of a set of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    The predicted label.
    
???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Dict[typing.Union[bool, str, int], float]*:     A dictionary that associates a probability which each label.
    

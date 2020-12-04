# StackingClassifier

Stacking for binary classification.



## Parameters

- **classifiers** (*List[[base.Classifier](../../base/Classifier)]*)

- **meta_classifier** (*[base.Classifier](../../base/Classifier)*)

- **include_features** – defaults to `True`

    Indicates whether or not the original features should be provided to the meta-model along with the predictions from each model.



## Examples

```python
>>> from river import compose
>>> from river import datasets
>>> from river import evaluate
>>> from river import expert
>>> from river import linear_model as lm
>>> from river import metrics
>>> from river import preprocessing as pp

>>> dataset = datasets.Phishing()

>>> model = compose.Pipeline(
...     ('scale', pp.StandardScaler()),
...     ('stack', expert.StackingClassifier(
...         classifiers=[
...             lm.LogisticRegression(),
...             lm.PAClassifier(mode=1, C=0.01),
...             lm.PAClassifier(mode=2, C=0.01)
...         ],
...         meta_classifier=lm.LogisticRegression()
...     ))
... )

>>> metric = metrics.F1()

>>> evaluate.progressive_val_score(dataset, model, metric)
F1: 0.881387
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

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Union[bool, str, int]*:     The predicted label.
    
???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    A dictionary that associates a probability which each label.
    
## References

[^1]: [A Kaggler's Guide to Model Stacking in Practice](http://blog.kaggle.com/2016/12/27/a-kagglers-guide-to-model-stacking-in-practice/)


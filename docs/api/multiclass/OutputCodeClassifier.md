# OutputCodeClassifier

Output-code multiclass strategy.

This also referred to as "error-correcting output codes". 

This class allows to learn a multi-class classification problem with a binary classifier. Each class is converted to a code of 0s and 1s. The length of the code is called  the code size. A copy of the classifier made for code. The codes associated with the classes are stored in a code book. 

When a new sample arrives, the label's code is retrieved from the code book. Then, each classifier is trained on the relevant part of code, which is either a 0 or a 1. 

For predicting, each classifier outputs a probability. These are then compared to each code in the code book, and the label which is the "closest" is chosen as the most likely class. Closeness is determined in terms of Manhattan distance. 

One specificity of online learning is that we don't how many classes there are initially. Therefore, a random procedure generates random codes on the fly whenever a previously unseed label appears.

## Parameters

- **classifier** (*[base.Classifier](../../base/Classifier)*)

    A binary classifier, although a multi-class classifier will work too.

- **code_size** (*int*)

    The code size, which dictates how many copies of the provided classifiers to train. Must be strictly positive.

- **seed** (*int*) – defaults to `None`

    A random seed number that can be set for reproducibility.



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
>>> ooc = OutputCodeClassifier(
...     classifier=linear_model.LogisticRegression(),
...     code_size=10,
...     seed=24
... )
>>> model = scaler | ooc

>>> metric = metrics.MacroF1()

>>> evaluate.progressive_val_score(dataset, model, metric)
MacroF1: 0.797119
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
    
## References

[^1]: [Dietterich, T.G. and Bakiri, G., 1994. Solving multiclass learning problems via error-correcting output codes. Journal of artificial intelligence research, 2, pp.263-286.](https://arxiv.org/pdf/cs/9501101.pdf)
[^2]: [Allwein, E.L., Schapire, R.E. and Singer, Y., 2000. Reducing multiclass to binary: A unifying approach for margin classifiers. Journal of machine learning research, 1(Dec), pp.113-141.](https://www.cs.princeton.edu/~schapire/talks/ecoc-icml10.pdf)


# LeveragingBaggingClassifier

Leveraging Bagging ensemble classifier.

Leveraging Bagging [^1] is an improvement over the Oza Bagging algorithm. The bagging performance is leveraged by increasing the re-sampling. It uses a poisson distribution to simulate the re-sampling process. To increase re-sampling it uses a higher `w` value of the Poisson distribution (agerage number of events), 6 by default, increasing the input space diversity, by attributing a different range of weights to the data samples. 

To deal with concept drift, Leveraging Bagging uses the ADWIN algorithm to monitor the performance of each member of the enemble If concept drift is detected, the worst member of the ensemble (based on the error estimation by ADWIN) is replaced by a new (empty) classifier.

## Parameters

- **model** (*[base.Classifier](../../base/Classifier)*)

    The classifier to bag.

- **n_models** (*int*) – defaults to `10`

    The number of models in the ensemble.

- **w** (*float*) – defaults to `6`

    Indicates the average number of events. This is the lambda parameter of the Poisson distribution used to compute the re-sampling weight.

- **adwin_delta** (*float*) – defaults to `0.002`

    The delta parameter for the ADWIN change detector.

- **bagging_method** (*str*) – defaults to `bag`

    The bagging method to use. Can be one of the following:<br/> * 'bag' - Leveraging Bagging using ADWIN.<br/> * 'me' - Assigns $weight=1$ if sample is misclassified,   otherwise $weight=error/(1-error)$.<br/> * 'half' - Use resampling without replacement for half of the instances.<br/> * 'wt' - Resample without taking out all instances.<br/> * 'subag' - Resampling without replacement.<br/>

- **seed** (*int*) – defaults to `None`

    Random number generator seed for reproducibility.


## Attributes

- **bagging_methods**

    Valid bagging_method options.


## Examples

```python
>>> from river import datasets
>>> from river import ensemble
>>> from river import evaluate
>>> from river import linear_model
>>> from river import metrics
>>> from river import optim
>>> from river import preprocessing

>>> dataset = datasets.Phishing()

>>> model = ensemble.LeveragingBaggingClassifier(
...     model=(
...         preprocessing.StandardScaler() |
...         linear_model.LogisticRegression()
...     ),
...     n_models=3,
...     seed=42
... )

>>> metric = metrics.F1()

>>> evaluate.progressive_val_score(dataset, model, metric)
F1: 0.886282
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

    Averages the predictions of each classifier.

    **Parameters**

    - **x**    
    

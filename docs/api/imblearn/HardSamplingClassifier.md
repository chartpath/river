# HardSamplingClassifier

Hard sampling classifier.

This wrapper enables a model to retrain on past samples who's output was hard to predict. This works by storing the hardest samples in a buffer of a fixed size. When a new sample arrives, the wrapped model is either trained on one of the buffered samples with a probability p or on the new sample with a probability (1 - p). 

The hardness of an observation is evaluated with a loss function that compares the sample's ground truth with the wrapped model's prediction. If the buffer is not full, then the sample is added to the buffer. If the buffer is full and the new sample has a bigger loss than the lowest loss in the buffer, then the sample takes it's place.

## Parameters

- **classifier** (*[base.Classifier](../../base/Classifier)*)

- **size** (*int*)

    Size of the buffer.

- **p** (*float*)

    Probability of updating the model with a sample from the buffer instead of a new incoming sample.

- **loss** (*Union[[optim.losses.BinaryLoss](../../optim/losses/BinaryLoss), [optim.losses.MultiClassLoss](../../optim/losses/MultiClassLoss)]*) – defaults to `None`

    Criterion used to evaluate the hardness of a sample.

- **seed** (*int*) – defaults to `None`

    Random seed.



## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import imblearn
>>> from river import linear_model
>>> from river import metrics
>>> from river import optim
>>> from river import preprocessing

>>> model = (
...     preprocessing.StandardScaler() |
...     imblearn.HardSamplingClassifier(
...         classifier=linear_model.LogisticRegression(),
...         p=0.1,
...         size=40,
...         seed=42,
...     )
... )

>>> evaluate.progressive_val_score(
...     dataset=datasets.Phishing(),
...     model=model,
...     metric=metrics.ROCAUC(),
...     print_every=500,
... )
[500] ROCAUC: 0.927112
[1,000] ROCAUC: 0.947515
ROCAUC: 0.950541
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

???- note "predict_one"

???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    A dictionary that associates a probability which each label.
    

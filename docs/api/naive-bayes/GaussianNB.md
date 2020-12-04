# GaussianNB

Gaussian Naive Bayes.

A Gaussian distribution $G_{cf}$ is maintained for each class $c$ and each feature $f$. Each Gaussian is updated using the amount associated with each feature; the details can be be found in `proba.Gaussian`. The joint log-likelihood is then obtained by summing the log probabilities of each feature associated with each class.



## Examples

```python
>>> from river import naive_bayes
>>> from river import stream
>>> import numpy as np

>>> X = np.array([[-1, -1], [-2, -1], [-3, -2], [1, 1], [2, 1], [3, 2]])
>>> Y = np.array([1, 1, 1, 2, 2, 2])

>>> model = naive_bayes.GaussianNB()

>>> for x, y in stream.iter_array(X, Y):
...     _ = model.learn_one(x, y)

>>> model.predict_one({0: -0.8, 1: -1})
1
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "joint_log_likelihood"

    Compute the unnormalized posterior log-likelihood of x.

    The log-likelihood is `log P(c) + log P(x|c)`.

    **Parameters**

    - **x**     (*dict*)    
    
???- note "learn_one"

    Update the model with a set of features `x` and a label `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*Union[bool, str, int]*)    
    
    **Returns**

    *Classifier*:     self
    
???- note "p_class"

???- note "predict_one"

    Predict the label of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Union[bool, str, int]*:     The predicted label.
    
???- note "predict_proba_one"

    Return probabilities using the log-likelihoods.

    **Parameters**

    - **x**     (*dict*)    
    

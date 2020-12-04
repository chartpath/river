# StatisticRegressor

Dummy regressor that uses a univariate statistic to make predictions.



## Parameters

- **statistic** (*river.stats.base.Univariate*)



## Examples

```python
>>> from pprint import pprint
>>> from river import dummy
>>> from river import stats

>>> sentences = [
...     ('glad happy glad', 3),
...     ('glad glad joyful', 3),
...     ('glad pleasant', 2),
...     ('miserable sad glad', -3)
... ]

>>> model = dummy.StatisticRegressor(stats.Mean())

>>> for sentence, score in sentences:
...     model = model.learn_one(sentence, score)

>>> new_sentence = 'glad sad miserable pleasant glad'
>>> model.predict_one(new_sentence)
1.25
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Fits to a set of features `x` and a real-valued target `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*numbers.Number*)    
    
    **Returns**

    *Regressor*:     self
    
???- note "predict_one"

    Predicts the target value of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *Number*:     The prediction.
    

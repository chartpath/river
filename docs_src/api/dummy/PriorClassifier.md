# PriorClassifier

Dummy classifier which uses the prior distribution.

The `predict_one` method will output the most common class whilst `predict_proba_one` will return the normalized class counts.


## Attributes

- **counts** (*collections.Counter*)

    Class counts.

- **n** (*int*)

    Total number of seen instances.


## Examples

Taken from example 2.1 from [this page](https://www.cms.waikato.ac.nz/~abifet/book/chapter_2.html)

```python
>>> from river import dummy

>>> sentences = [
...     ('glad happy glad', '+'),
...     ('glad glad joyful', '+'),
...     ('glad pleasant', '+'),
...     ('miserable sad glad', '−')
... ]

>>> model = dummy.PriorClassifier()

>>> for sentence, label in sentences:
...     model = model.learn_one(sentence, label)

>>> new_sentence = 'glad sad miserable pleasant glad'
>>> model.predict_one(new_sentence)
'+'
>>> model.predict_proba_one(new_sentence)
{'+': 0.75, '−': 0.25}
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update the model with a set of features `x` and a label `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*Union[bool, str, int]*)    
    
    **Returns**

    *Classifier*:     self
    
???- note "predict_one"

    Predict the label of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Union[bool, str, int]*:     The predicted label.
    
???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Dict[typing.Union[bool, str, int], float]*:     A dictionary that associates a probability which each label.
    

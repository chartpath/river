# MultinomialNB

Naive Bayes classifier for multinomial models.

The input vector has to contain positive values, such as counts or TF-IDF values.

## Parameters

- **alpha** – defaults to `1.0`

    Additive (Laplace/Lidstone) smoothing parameter (use 0 for no smoothing).


## Attributes

- **class_dist** (*proba.Multinomial*)

    Class prior probability distribution.

- **feature_counts** (*collections.defaultdict*)

    Total frequencies per feature and class.

- **class_totals** (*collections.Counter*)

    Total frequencies per class.


## Examples

```python
>>> import math
>>> from river import compose
>>> from river import feature_extraction
>>> from river import naive_bayes

>>> docs = [
...     ('Chinese Beijing Chinese', 'yes'),
...     ('Chinese Chinese Shanghai', 'yes'),
...     ('Chinese Macao', 'yes'),
...     ('Tokyo Japan Chinese', 'no')
... ]
>>> model = compose.Pipeline(
...     ('tokenize', feature_extraction.BagOfWords(lowercase=False)),
...     ('nb', naive_bayes.MultinomialNB(alpha=1))
... )
>>> for sentence, label in docs:
...     model = model.learn_one(sentence, label)

>>> model['nb'].p_class('yes')
0.75
>>> model['nb'].p_class('no')
0.25

>>> cp = model['nb'].p_feature_given_class

>>> cp('Chinese', 'yes') == (5 + 1) / (8 + 6)
True

>>> cp('Tokyo', 'yes') == (0 + 1) / (8 + 6)
True
>>> cp('Japan', 'yes') == (0 + 1) / (8 + 6)
True

>>> cp('Chinese', 'no') == (1 + 1) / (3 + 6)
True

>>> cp('Tokyo', 'no') == (1 + 1) / (3 + 6)
True
>>> cp('Japan', 'no') == (1 + 1) / (3 + 6)
True

>>> new_text = 'Chinese Chinese Chinese Tokyo Japan'
>>> tokens = model['tokenize'].transform_one(new_text)
>>> jlh = model['nb'].joint_log_likelihood(tokens)
>>> math.exp(jlh['yes'])
0.000301
>>> math.exp(jlh['no'])
0.000135
>>> model.predict_one(new_text)
'yes'

>>> new_unseen_text = 'Taiwanese Taipei'
>>> tokens = model['tokenize'].transform_one(new_unseen_text)
>>> # P(Taiwanese|yes)
>>> #   = (N_Taiwanese_yes + 1) / (N_yes + N_terms)
>>> cp('Taiwanese', 'yes') == cp('Taipei', 'yes') == (0 + 1) / (8 + 6)
True
>>> cp('Taiwanese', 'no') == cp('Taipei', 'no') == (0 + 1) / (3 + 6)
True

>>> # P(yes|Taiwanese Taipei)
>>> #   ∝ P(Taiwanese|yes) * P(Taipei|yes) * P(yes)
>>> posterior_yes_given_new_text = (0 + 1) / (8 + 6) * (0 + 1) / (8 + 6) * 0.75
>>> jlh = model['nb'].joint_log_likelihood(tokens)
>>> jlh['yes'] == math.log(posterior_yes_given_new_text)
True

>>> model.predict_one(new_unseen_text)
'yes'
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

???- note "p_feature_given_class"

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
    
## References

[^1]: [Naive Bayes text classification](https://nlp.stanford.edu/IR-book/html/htmledition/naive-bayes-text-classification-1.html)


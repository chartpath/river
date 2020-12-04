# ComplementNB

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
>>> from river import feature_extraction
>>> from river import naive_bayes

>>> sentences = [
...     ('food food meat brain', 'health'),
...     ('food meat ' + 'kitchen ' * 9 + 'job' * 5, 'butcher'),
...     ('food food meat job', 'health')
... ]

>>> model = feature_extraction.BagOfWords() | ('nb', naive_bayes.ComplementNB)

>>> for sentence, label in sentences:
...     model = model.learn_one(sentence, label)

>>> model['nb'].p_class('health') == 2 / 3
True
>>> model['nb'].p_class('butcher') == 1 / 3
True

>>> model.predict_proba_one('food job meat')
{'health': 0.779191, 'butcher': 0.220808}
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
    
## References

[^1]: [Rennie, J.D., Shih, L., Teevan, J. and Karger, D.R., 2003. Tackling the poor assumptions of naive bayes text classifiers. In Proceedings of the 20th international conference on machine learning (ICML-03) (pp. 616-623)](https://people.csail.mit.edu/jrennie/papers/icml03-nb.pdf)
[^2]: [StackExchange discussion](https://stats.stackexchange.com/questions/126009/complement-naive-bayes)


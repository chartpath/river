# TFIDF

Computes TF-IDF values from sentences.

The TF-IDF formula is the same one as scikit-learn. The only difference is the fact that the document frequencies are determined online, whereas in a batch setting they can be determined by performing an initial pass through the data. 

Note that the parameters are identical to those of `feature_extraction.BagOfWords`.

## Parameters

- **normalize** – defaults to `True`

    Whether or not the TF-IDF values by their L2 norm.

- **on** (*str*) – defaults to `None`

    The name of the feature that contains the text to vectorize. If `None`, then the input is treated as a document instead of a set of features.

- **strip_accents** – defaults to `True`

    Whether or not to strip accent characters.

- **lowercase** – defaults to `True`

    Whether or not to convert all characters to lowercase.

- **preprocessor** (*Callable*) – defaults to `None`

    Override the preprocessing step while preserving the tokenizing and n-grams generation steps.

- **tokenizer** (*Callable*) – defaults to `None`

    A function used to convert preprocessed text into a `dict` of tokens. By default, a regex formula that works well in most cases is used.

- **ngram_range** – defaults to `(1, 1)`

    The lower and upper boundary of the range n-grams to be extracted. All values of n such that `min_n <= n <= max_n` will be used. For example an `ngram_range` of `(1, 1)` means only unigrams, `(1, 2)` means unigrams and bigrams, and `(2, 2)` means only bigrams. Only works if `tokenizer` is not set to `False`.


## Attributes

- **dfs** (*collections.defaultdict)*)

    Document counts.

- **n** (*int*)

    Number of scanned documents.


## Examples

```python
>>> from river import feature_extraction

>>> tfidf = feature_extraction.TFIDF()

>>> corpus = [
...     'This is the first document.',
...     'This document is the second document.',
...     'And this is the third one.',
...     'Is this the first document?',
... ]

>>> for sentence in corpus:
...     tfidf = tfidf.learn_one(sentence)
...     print(tfidf.transform_one(sentence))
{'this': 0.447, 'is': 0.447, 'the': 0.447, 'first': 0.447, 'document': 0.447}
{'this': 0.333, 'document': 0.667, 'is': 0.333, 'the': 0.333, 'second': 0.469}
{'and': 0.497, 'this': 0.293, 'is': 0.293, 'the': 0.293, 'third': 0.497, 'one': 0.497}
{'is': 0.384, 'this': 0.384, 'the': 0.384, 'first': 0.580, 'document': 0.469}

```

In the above example, a string is passed to `transform_one`. You can also indicate which
field to access if the string is stored in a dictionary:

```python
>>> tfidf = feature_extraction.TFIDF(on='sentence')

>>> for sentence in corpus:
...     x = {'sentence': sentence}
...     tfidf = tfidf.learn_one(x)
...     print(tfidf.transform_one(x))
{'this': 0.447, 'is': 0.447, 'the': 0.447, 'first': 0.447, 'document': 0.447}
{'this': 0.333, 'document': 0.667, 'is': 0.333, 'the': 0.333, 'second': 0.469}
{'and': 0.497, 'this': 0.293, 'is': 0.293, 'the': 0.293, 'third': 0.497, 'one': 0.497}
{'is': 0.384, 'this': 0.384, 'the': 0.384, 'first': 0.580, 'document': 0.469}
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update with a set of features `x`.

    A lot of transformers don't actually have to do anything during the `learn_one` step because they are stateless. For this reason the default behavior of this function is to do nothing. Transformers that however do something during the `learn_one` can override this method.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *Transformer*:     self
    
???- note "process_text"

???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *dict*:     The transformed values.
    

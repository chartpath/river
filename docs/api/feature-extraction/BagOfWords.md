# BagOfWords

Counts tokens in sentences.

This transformer can be used to counts tokens in a given piece of text. It takes care of normalizing the text before tokenizing it. 

Note that the parameters are identical to those of `feature_extraction.TFIDF`.

## Parameters

- **on** (*str*) – defaults to `None`

    The name of the feature that contains the text to vectorize. If `None`, then each `learn_one` and `transform_one` will assume that each `x` that is provided is a `str`, andnot a `dict`.

- **strip_accents** – defaults to `True`

    Whether or not to strip accent characters.

- **lowercase** – defaults to `True`

    Whether or not to convert all characters to lowercase.

- **preprocessor** (*Callable*) – defaults to `None`

    Override the preprocessing step while preserving the tokenizing and n-grams generation steps.

- **tokenizer** (*Callable*) – defaults to `None`

    A function used to convert preprocessed text into a `dict` of tokens. By default, a regex formula that works well in most cases is used.

- **ngram_range** – defaults to `(1, 1)`

    The lower and upper boundary of the range n-grams to be extracted. All values of n such that `min_n <= n <= max_n` will be used. For example an `ngram_range` of `(1, 1)` means only unigrams, `(1, 2)` means unigrams and bigrams, and `(2, 2)` means only bigrams.



## Examples

By default, `BagOfWords` will take as input a sentence, preprocess it, tokenize the
preprocessed text, and then return a `collections.Counter` containing the number of
occurrences of each token.

```python
>>> from river import feature_extraction as fx

>>> corpus = [
...     'This is the first document.',
...     'This document is the second document.',
...     'And this is the third one.',
...     'Is this the first document?',
... ]

>>> bow = fx.BagOfWords()

>>> for sentence in corpus:
...     print(bow.transform_one(sentence))
Counter({'this': 1, 'is': 1, 'the': 1, 'first': 1, 'document': 1})
Counter({'document': 2, 'this': 1, 'is': 1, 'the': 1, 'second': 1})
Counter({'and': 1, 'this': 1, 'is': 1, 'the': 1, 'third': 1, 'one': 1})
Counter({'is': 1, 'this': 1, 'the': 1, 'first': 1, 'document': 1})

```

Note that `learn_one` does not have to be called because `BagOfWords` is stateless. You can
call it but it won't do anything.

In the above example, a string is passed to `transform_one`. You can also indicate which
field to access if the string is stored in a dictionary:

```python
>>> bow = fx.BagOfWords(on='sentence')

>>> for sentence in corpus:
...     x = {'sentence': sentence}
...     print(bow.transform_one(x))
Counter({'this': 1, 'is': 1, 'the': 1, 'first': 1, 'document': 1})
Counter({'document': 2, 'this': 1, 'is': 1, 'the': 1, 'second': 1})
Counter({'and': 1, 'this': 1, 'is': 1, 'the': 1, 'third': 1, 'one': 1})
Counter({'is': 1, 'this': 1, 'the': 1, 'first': 1, 'document': 1})

```

The `ngram_range` parameter can be used to extract n-grams (including unigrams):

```python
>>> ngrammer = fx.BagOfWords(ngram_range=(1, 2))

>>> ngrams = ngrammer.transform_one('I love the smell of napalm in the morning')
>>> for ngram, count in ngrams.items():
...     print(ngram, count)
love 1
the 2
smell 1
of 1
napalm 1
in 1
morning 1
('love', 'the') 1
('the', 'smell') 1
('smell', 'of') 1
('of', 'napalm') 1
('napalm', 'in') 1
('in', 'the') 1
('the', 'morning') 1
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
    - **kwargs**    
    
    **Returns**

    *Transformer*:     self
    
???- note "process_text"

???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *dict*:     The transformed values.
    

# Pipeline

A pipeline of estimators.

Pipelines allow you to chain different steps into a sequence. Typically, when doing supervised learning, a pipeline contains one ore more transformation steps, whilst it's is a regressor or a classifier. It is highly recommended to use pipelines with `river`. Indeed, in an online learning setting, it is very practical to have a model defined as a single object. Take a look at the [user guide](/user-guide/the-art-of-using-pipelines) for further information and practical examples. 

One special thing to take notice to is the way transformers are handled. In a typical scenario, it is usual to predict something for a sample and wait for the ground truth to arrive. In such a case, the features are seen before the ground truth arrives. Therefore, the unsupervised parts of the pipeline are updated when `predict_one` and `predict_proba_one` are called. Usually the unsupervised parts of the pipeline are all the steps that precede the final step, which is a supervised model. However, some transformers are supervised and are therefore obtained during calls to `learn_one`.

## Parameters

- **steps**

    Ideally, a list of (name, estimator) tuples. A name is automatically inferred if none is provided.



## Examples

The recommended way to declare a pipeline is to use the `|` operator. The latter allows you
to chain estimators in a very terse manner:

```python
>>> from river import linear_model
>>> from river import preprocessing

>>> scaler = preprocessing.StandardScaler()
>>> log_reg = linear_model.LinearRegression()
>>> model = scaler | log_reg

```

This results in a pipeline that stores each step inside a dictionary.

```python
>>> model
Pipeline (
  StandardScaler (),
  LinearRegression (
    optimizer=SGD (
      lr=Constant (
        learning_rate=0.01
      )
    )
    loss=Squared ()
    l2=0.
    intercept_init=0.
    intercept_lr=Constant (
      learning_rate=0.01
    )
    clip_gradient=1e+12
    initializer=Zeros ()
  )
)

```

You can access parts of a pipeline in the same manner as a dictionary:

```python
>>> model['LinearRegression']
LinearRegression (
  optimizer=SGD (
    lr=Constant (
      learning_rate=0.01
    )
  )
  loss=Squared ()
  l2=0.
  intercept_init=0.
  intercept_lr=Constant (
    learning_rate=0.01
  )
  clip_gradient=1e+12
  initializer=Zeros ()
)

```

Note that you can also declare a pipeline by using the `compose.Pipeline` constructor
method, which is slightly more verbose:

```python
>>> from river import compose

>>> model = compose.Pipeline(scaler, log_reg)

```

By using a `compose.TransformerUnion`, you can define complex pipelines that apply
different steps to different parts of the data. For instance, we can extract word counts
from text data, and extract polynomial features from numeric data.

```python
>>> from river import feature_extraction as fx

>>> tfidf = fx.TFIDF('text')
>>> counts = fx.BagOfWords('text')
>>> text_part = compose.Select('text') | (tfidf + counts)

>>> num_part = compose.Select('a', 'b') | fx.PolynomialExtender()

>>> model = text_part + num_part
>>> model |= preprocessing.StandardScaler()
>>> model |= linear_model.LinearRegression()

```

You can obtain a visual representation of the pipeline by calling it's `draw` method.

```python
>>> dot = model.draw()

```

![pipeline_example](/img/pipeline_docstring.svg)

The following shows an example of using `debug_one` to visualize how the information
flows and changes throughout the pipeline.

```python
>>> from river import compose
>>> from river import naive_bayes

>>> dataset = [
...     ('A positive comment', True),
...     ('A negative comment', False),
...     ('A happy comment', True),
...     ('A lovely comment', True),
...     ('A harsh comment', False)
... ]

>>> tfidf = fx.TFIDF() | compose.Renamer(prefix='tfidf_')
>>> counts = fx.BagOfWords() | compose.Renamer(prefix='count_')
>>> mnb = naive_bayes.MultinomialNB()
>>> model = (tfidf + counts) | mnb

>>> for x, y in dataset:
...     model = model.learn_one(x, y)

>>> x = dataset[0][0]
>>> report = model.debug_one(dataset[0][0])
>>> print(report)
0. Input
--------
A positive comment
<BLANKLINE>
1. Transformer union
--------------------
    1.0 TFIDF | Renamer
    -------------------
    tfidf_comment: 0.47606 (float)
    tfidf_positive: 0.87942 (float)
<BLANKLINE>
    1.1 BagOfWords | Renamer
    ------------------------
    count_comment: 1 (int)
    count_positive: 1 (int)
<BLANKLINE>
count_comment: 1 (int)
count_positive: 1 (int)
tfidf_comment: 0.50854 (float)
tfidf_positive: 0.86104 (float)
<BLANKLINE>
2. MultinomialNB
----------------
False: 0.19313
True: 0.80687
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "debug_one"

    Displays the state of a set of features as it goes through the pipeline.

    **Parameters**

    - **x**     (*dict*)    
    - **show_types**     – defaults to `True`    
    - **n_decimals**     – defaults to `5`    
    
???- note "draw"

    Draws the pipeline using the `graphviz` library.

    
???- note "forecast"

    Return a forecast.

    Only works if each estimator has a `transform_one` method and the final estimator has a `forecast` method. This is the case of time series models from the `time_series` module.

    **Parameters**

    - **horizon**     (*int*)    
    - **xs**     (*List[dict]*)     – defaults to `None`    
    
???- note "learn_many"

    Fit to a mini-batch.

    **Parameters**

    - **X**     (*pandas.core.frame.DataFrame*)    
    - **y**     (*pandas.core.series.Series*)     – defaults to `None`    
    - **params**    
    
???- note "learn_one"

    Fit to a single instance.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     – defaults to `None`    
    - **params**    
    
???- note "predict_many"

???- note "predict_one"

???- note "predict_proba_many"

???- note "predict_proba_one"

???- note "score_one"

???- note "transform_many"

    Apply each transformer in the pipeline to some features.

    The final step in the pipeline will be applied if it is a transformer. If not, then it will be ignored and the output from the penultimate step will be returned. Note that the steps that precede the final step are assumed to all be transformers.

    **Parameters**

    - **X**     (*pandas.core.frame.DataFrame*)    
    
???- note "transform_one"

    Apply each transformer in the pipeline to some features.

    The final step in the pipeline will be applied if it is a transformer. If not, then it will be ignored and the output from the penultimate step will be returned. Note that the steps that precede the final step are assumed to all be transformers.

    **Parameters**

    - **x**     (*dict*)    
    

# TransformerUnion

Packs multiple transformers into a single one.

Pipelines allow you to apply steps sequentially. Therefore, the output of a step becomes the input of the next one. In many cases, you may want to pass the output of a step to multiple steps. This simple transformer allows you to do so. In other words, it enables you to apply particular steps to different parts of an input. A typical example is when you want to scale numeric features and one-hot encode categorical features. 

This transformer is essentially a list of transformers. Whenever it is updated, it loops through each transformer and updates them. Meanwhile, calling `transform_one` collects the output of each transformer and merges them into a single dictionary.

## Parameters

- **transformers**

    Ideally, a list of (name, estimator) tuples. A name is automatically inferred if none is provided.



## Examples

Take the following dataset:

```python
>>> X = [
...     {'place': 'Taco Bell', 'revenue': 42},
...     {'place': 'Burger King', 'revenue': 16},
...     {'place': 'Burger King', 'revenue': 24},
...     {'place': 'Taco Bell', 'revenue': 58},
...     {'place': 'Burger King', 'revenue': 20},
...     {'place': 'Taco Bell', 'revenue': 50}
... ]

```

As an example, let's assume we want to compute two aggregates of a dataset. We therefore
define two `feature_extraction.Agg`s and initialize a `TransformerUnion` with them:

```python
>>> from river import compose
>>> from river import feature_extraction
>>> from river import stats

>>> mean = feature_extraction.Agg(
...     on='revenue', by='place',
...     how=stats.Mean()
... )
>>> count = feature_extraction.Agg(
...     on='revenue', by='place',
...     how=stats.Count()
... )
>>> agg = compose.TransformerUnion(mean, count)

```

We can now update each transformer and obtain their output with a single function call:

```python
>>> from pprint import pprint
>>> for x in X:
...     agg = agg.learn_one(x)
...     pprint(agg.transform_one(x))
{'revenue_count_by_place': 1, 'revenue_mean_by_place': 42.0}
{'revenue_count_by_place': 1, 'revenue_mean_by_place': 16.0}
{'revenue_count_by_place': 2, 'revenue_mean_by_place': 20.0}
{'revenue_count_by_place': 2, 'revenue_mean_by_place': 50.0}
{'revenue_count_by_place': 3, 'revenue_mean_by_place': 20.0}
{'revenue_count_by_place': 3, 'revenue_mean_by_place': 50.0}

```

Note that you can use the `+` operator as a shorthand notation:

agg = mean + count

This allows you to build complex pipelines in a very terse manner. For instance, we can
create a pipeline that scales each feature and fits a logistic regression as so:

```python
>>> from river import linear_model as lm
>>> from river import preprocessing as pp

>>> model = (
...     (mean + count) |
...     pp.StandardScaler() |
...     lm.LogisticRegression()
... )

```

Whice is equivalent to the following code:

```python
>>> model = compose.Pipeline(
...     compose.TransformerUnion(mean, count),
...     pp.StandardScaler(),
...     lm.LogisticRegression()
... )

```

Note that you access any part of a `TransformerUnion` by name:

```python
>>> model['TransformerUnion']['Agg']
Agg (
    on="revenue"
    by=['place']
    how=Mean ()
)

>>> model['TransformerUnion']['Agg1']
Agg (
    on="revenue"
    by=['place']
    how=Count ()
)

```

You can also manually provide a name for each step:

```python
>>> agg = compose.TransformerUnion(
...     ('Mean revenue by place', mean),
...     ('# by place', count)
... )
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update each transformer.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     – defaults to `None`    
    
???- note "transform_one"

    Passes the data through each transformer and packs the results together.

    **Parameters**

    - **x**     (*dict*)    
    

# Agg

Computes a streaming aggregate.

This transformer allows to compute an aggregate statistic, very much like the groupby method from `pandas`, but on a streaming dataset. This makes use of the streaming statistics from the `stats` module. 

When `learn_one` is called, the running statistic `how` of group `by` is updated with the value of `on`. Meanwhile, the output of `transform_one` is a single-element dictionary, where the key is the name of the aggregate and the value is the current value of the statistic for the relevant group. The key is automatically inferred from the parameters. 

Note that you can use a `compose.TransformerUnion` to extract many aggregate statistics in a concise manner.

## Parameters

- **on** (*str*)

    The feature on which to compute the aggregate statistic.

- **by** (*Union[str, List[str]]*)

    The feature by which to group the data.

- **how** (*river.stats.base.Univariate*)

    The statistic to compute.


## Attributes

- **groups** (*collections.defaultdict*)

    Maps group keys to univariate statistics.

- **feature_name** (*str*)

    The name of the feature used in the output.


## Examples

Consider the following dataset:

```python
>>> X = [
...     {'country': 'France', 'place': 'Taco Bell', 'revenue': 42},
...     {'country': 'Sweden', 'place': 'Burger King', 'revenue': 16},
...     {'country': 'France', 'place': 'Burger King', 'revenue': 24},
...     {'country': 'Sweden', 'place': 'Taco Bell', 'revenue': 58},
...     {'country': 'Sweden', 'place': 'Burger King', 'revenue': 20},
...     {'country': 'France', 'place': 'Taco Bell', 'revenue': 50},
...     {'country': 'France', 'place': 'Burger King', 'revenue': 10},
...     {'country': 'Sweden', 'place': 'Taco Bell', 'revenue': 80}
... ]

```

As an example, we can calculate the average (how) revenue (on) for each place (by):

```python
>>> from river import feature_extraction as fx
>>> from river import stats

>>> agg = fx.Agg(
...     on='revenue',
...     by='place',
...     how=stats.Mean()
... )

>>> for x in X:
...     agg = agg.learn_one(x)
...     print(agg.transform_one(x))
{'revenue_mean_by_place': 42.0}
{'revenue_mean_by_place': 16.0}
{'revenue_mean_by_place': 20.0}
{'revenue_mean_by_place': 50.0}
{'revenue_mean_by_place': 20.0}
{'revenue_mean_by_place': 50.0}
{'revenue_mean_by_place': 17.5}
{'revenue_mean_by_place': 57.5}

```

You can compute an aggregate over multiple keys by passing a tuple to the `by` argument.
For instance, we can compute the maximum (how) revenue (on) per place as well as per
day (by):

```python
>>> agg = fx.Agg(
...     on='revenue',
...     by=['place', 'country'],
...     how=stats.Max()
... )

>>> for x in X:
...     agg = agg.learn_one(x)
...     print(agg.transform_one(x))
{'revenue_max_by_place_and_country': 42}
{'revenue_max_by_place_and_country': 16}
{'revenue_max_by_place_and_country': 24}
{'revenue_max_by_place_and_country': 58}
{'revenue_max_by_place_and_country': 20}
{'revenue_max_by_place_and_country': 50}
{'revenue_max_by_place_and_country': 24}
{'revenue_max_by_place_and_country': 80}

```

You can use a `compose.TransformerUnion` in order to calculate multiple aggregates in one
go. The latter can be constructed by using the `+` operator:

```python
>>> agg = (
...     fx.Agg(on='revenue', by='place', how=stats.Mean()) +
...     fx.Agg(on='revenue', by=['place', 'country'], how=stats.Max())
... )

>>> import pprint
>>> for x in X:
...     agg = agg.learn_one(x)
...     pprint.pprint(agg.transform_one(x))
{'revenue_max_by_place_and_country': 42, 'revenue_mean_by_place': 42.0}
{'revenue_max_by_place_and_country': 16, 'revenue_mean_by_place': 16.0}
{'revenue_max_by_place_and_country': 24, 'revenue_mean_by_place': 20.0}
{'revenue_max_by_place_and_country': 58, 'revenue_mean_by_place': 50.0}
{'revenue_max_by_place_and_country': 20, 'revenue_mean_by_place': 20.0}
{'revenue_max_by_place_and_country': 50, 'revenue_mean_by_place': 50.0}
{'revenue_max_by_place_and_country': 24, 'revenue_mean_by_place': 17.5}
{'revenue_max_by_place_and_country': 80, 'revenue_mean_by_place': 57.5}
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
    
???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *dict*:     The transformed values.
    
## References

[^1]: [Streaming groupbys in pandas for big datasets](https://maxhalford.github.io/blog/streaming-groupbys-in-pandas-for-big-datasets/)


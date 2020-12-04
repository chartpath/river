# TargetAgg

Computes a streaming aggregate of the target values.

This transformer is identical to `feature_extraction.Agg`, the only difference is that it operates on the target rather than on a feature. At each step, the running statistic `how` of target values in group `by` is updated with the target. It is therefore a supervised transformer.

## Parameters

- **by** (*Union[str, List[str]]*)

    The feature by which to group the target values.

- **how** (*river.stats.base.Univariate*)

    The statistic to compute.

- **target_name** – defaults to `target`

    The target name which is used in the result.


## Attributes

- **groups**

    Maps group keys to univariate statistics.

- **feature_name**

    The name of the feature in the output.


## Examples

Consider the following dataset, where the second value of each value is the target:

```python
>>> dataset = [
...     ({'country': 'France', 'place': 'Taco Bell'}, 42),
...     ({'country': 'Sweden', 'place': 'Burger King'}, 16),
...     ({'country': 'France', 'place': 'Burger King'}, 24),
...     ({'country': 'Sweden', 'place': 'Taco Bell'}, 58),
...     ({'country': 'Sweden', 'place': 'Burger King'}, 20),
...     ({'country': 'France', 'place': 'Taco Bell'}, 50),
...     ({'country': 'France', 'place': 'Burger King'}, 10),
...     ({'country': 'Sweden', 'place': 'Taco Bell'}, 80)
... ]

```

As an example, let's perform a target encoding of the `place` feature. Instead of simply
updating a running average, we use a `stats.BayesianMean` which allows us to incorporate
some prior knowledge. This makes subsequent models less prone to overfitting. Indeed, it
dampens the fact that too few samples might have been seen within a group.

```python
>>> from river import feature_extraction
>>> from river import stats

>>> agg = feature_extraction.TargetAgg(
...     by='place',
...     how=stats.BayesianMean(
...         prior=3,
...         prior_weight=1
...     )
... )

>>> for x, y in dataset:
...     print(agg.transform_one(x))
...     agg = agg.learn_one(x, y)
{'target_bayes_mean_by_place': 3.0}
{'target_bayes_mean_by_place': 3.0}
{'target_bayes_mean_by_place': 9.5}
{'target_bayes_mean_by_place': 22.5}
{'target_bayes_mean_by_place': 14.333}
{'target_bayes_mean_by_place': 34.333}
{'target_bayes_mean_by_place': 15.75}
{'target_bayes_mean_by_place': 38.25}

```

Just like with `feature_extraction.Agg`, we can specify multiple features on which to
group the data:

```python
>>> agg = feature_extraction.TargetAgg(
...     by=['place', 'country'],
...     how=stats.BayesianMean(
...         prior=3,
...         prior_weight=1
...     )
... )

>>> for x, y in dataset:
...     print(agg.transform_one(x))
...     agg = agg.learn_one(x, y)
{'target_bayes_mean_by_place_and_country': 3.0}
{'target_bayes_mean_by_place_and_country': 3.0}
{'target_bayes_mean_by_place_and_country': 3.0}
{'target_bayes_mean_by_place_and_country': 3.0}
{'target_bayes_mean_by_place_and_country': 9.5}
{'target_bayes_mean_by_place_and_country': 22.5}
{'target_bayes_mean_by_place_and_country': 13.5}
{'target_bayes_mean_by_place_and_country': 30.5}
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update with a set of features `x` and a target `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*Union[bool, str, int, numbers.Number]*)    
    
    **Returns**

    *SupervisedTransformer*:     self
    
???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *dict*:     The transformed values.
    
## References

1. [Streaming groupbys in pandas for big datasets](https://maxhalford.github.io/blog/streaming-groupbys-in-pandas-for-big-datasets/)


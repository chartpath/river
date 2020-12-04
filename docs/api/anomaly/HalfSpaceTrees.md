# HalfSpaceTrees

Half-Space Trees (HST).

Half-space trees are an online variant of isolation forests. They work well when anomalies are spread out. However, they do not work well if anomalies are packed together in windows. 

By default, this implementation assumes that each feature has values that are comprised between 0 and 1. If this isn't the case, then you can manually specify the limits via the `limits` argument. If you do not know the limits in advance, then you can use a `preprocessing.MinMaxScaler` as an initial preprocessing step. 

The current implementation builds the trees the first time the `learn_one` method is called. Therefore, the first `learn_one` call might be slow, whereas subsequent calls will be very fast in comparison. In general, the computation time of both `learn_one` and `score_one` scales linearly with the number of trees, and exponentially with the height of each tree. 

Note that high scores indicate anomalies, whereas low scores indicate normal observations.

## Parameters

- **n_trees** – defaults to `10`

    Number of trees to use.

- **height** – defaults to `8`

    Height of each tree. Note that a tree of height `h` is made up of `h + 1` levels and therefore contains `2 ** (h + 1) - 1` nodes.

- **window_size** – defaults to `250`

    Number of observations to use for calculating the mass at each node in each tree.

- **limits** (*Dict[Hashable, Tuple[float, float]]*) – defaults to `None`

    Specifies the range of each feature. By default each feature is assumed to be in range `[0, 1]`.

- **seed** (*int*) – defaults to `None`

    Random number seed.


## Attributes

- **size_limit**

    This is the threshold under which the node search stops during the scoring phase.  The value .1 is a magic constant indicated in the original paper.


## Examples

```python
>>> from river import anomaly

>>> X = [0.5, 0.45, 0.43, 0.44, 0.445, 0.45, 0.0]
>>> hst = anomaly.HalfSpaceTrees(
...     n_trees=5,
...     height=3,
...     window_size=3,
...     seed=42
... )

>>> for x in X[:3]:
...     hst = hst.learn_one({'x': x})  # Warming up

>>> for x in X:
...     features = {'x': x}
...     hst = hst.learn_one(features)
...     print(f'Anomaly score for x={x:.3f}: {hst.score_one(features):.3f}')
Anomaly score for x=0.500: 0.107
Anomaly score for x=0.450: 0.071
Anomaly score for x=0.430: 0.107
Anomaly score for x=0.440: 0.107
Anomaly score for x=0.445: 0.107
Anomaly score for x=0.450: 0.071
Anomaly score for x=0.000: 0.853

```

The feature values are all comprised between 0 and 1. This is what is assumed by the model
by default. In the following example, we construct a pipeline that scales the data online
and ensures that the values of each feature are comprised between 0 and 1.

```python
>>> from river import compose
>>> from river import datasets
>>> from river import metrics
>>> from river import preprocessing

>>> model = compose.Pipeline(
...     preprocessing.MinMaxScaler(),
...     anomaly.HalfSpaceTrees(seed=42)
... )

>>> auc = metrics.ROCAUC()

>>> for x, y in datasets.CreditCard().take(8000):
...     score = model.score_one(x)
...     model = model.learn_one(x, y)
...     auc = auc.update(y, score)

>>> auc
ROCAUC: 0.940431
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update the model.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *AnomalyDetector*:     self
    
???- note "score_one"

    Return an outlier score.

    A high score is indicative of an anomaly. A low score corresponds a normal observation.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *float*:     An anomaly score. A high score is indicative of an anomaly. A low score corresponds a
    
## References

[^1]: [Tan, S.C., Ting, K.M. and Liu, T.F., 2011, June. Fast anomaly detection for streaming data. In Twenty-Second International Joint Conference on Artificial Intelligence.](https://www.ijcai.org/Proceedings/11/Papers/254.pdf)


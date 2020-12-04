# KNNRegressor

k-Nearest Neighbors regressor.

This non-parametric regression method keeps track of the last `window_size` training samples. Predictions are obtained by aggregating the values of the closest n_neighbors stored-samples with respect to a query sample.

## Parameters

- **n_neighbors** (*int*) – defaults to `5`

    The number of nearest neighbors to search for.

- **window_size** (*int*) – defaults to `1000`

    The maximum size of the window storing the last observed samples.

- **leaf_size** (*int*) – defaults to `30`

    scipy.spatial.cKDTree parameter. The maximum number of samples that can be stored in one leaf node, which determines from which point the algorithm will switch for a brute-force approach. The bigger this number the faster the tree construction time, but the slower the query time will be.

- **p** (*float*) – defaults to `2`

    p-norm value for the Minkowski metric. When `p=1`, this corresponds to the Manhattan distance, while `p=2` corresponds to the Euclidean distance. Valid values are in the interval $[1, +\infty)$

- **aggregation_method** (*str*) – defaults to `mean`

    The method to aggregate the target values of neighbors.     | 'mean'     | 'median'     | 'weighted_mean'

- **kwargs**

    Other parameters passed to scipy.spatial.cKDTree.



## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import metrics
>>> from river import neighbors
>>> from river import preprocessing

>>> dataset = datasets.TrumpApproval()

>>> model = (
...     preprocessing.StandardScaler() |
...     neighbors.KNNRegressor(window_size=50)
... )

>>> metric = metrics.MAE()

>>> evaluate.progressive_val_score(dataset, model, metric)
MAE: 0.441308
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update the model with a set of features `x` and a real target value `y`.

    **Parameters**

    - **x**    
    - **y**    
    
    **Returns**

    self
    
???- note "predict_one"

    Predict the target value of a set of features `x`.

    Search the KDTree for the `n_neighbors` nearest neighbors.

    **Parameters**

    - **x**    
    
    **Returns**

    The prediction.
    
???- note "reset"

    Reset estimator. 

    
## Notes

This estimator is not optimal for a mixture of categorical and numerical
features. This implementation treats all features from a given stream as
numerical.


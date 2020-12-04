# KNNClassifier

k-Nearest Neighbors classifier.

This non-parametric classification method keeps track of the last `window_size` training samples. The predicted class-label for a given query sample is obtained in two steps: 

1. Find the closest `n_neighbors` to the query sample in the data window. 2. Aggregate the class-labels of the `n_neighbors` to define the predicted    class for the query sample.

## Parameters

- **n_neighbors** (*int*) – defaults to `5`

    The number of nearest neighbors to search for.

- **window_size** (*int*) – defaults to `1000`

    The maximum size of the window storing the last observed samples.

- **leaf_size** (*int*) – defaults to `30`

    scipy.spatial.cKDTree parameter. The maximum number of samples that can be stored in one leaf node, which determines from which point the algorithm will switch for a brute-force approach. The bigger this number the faster the tree construction time, but the slower the query time will be.

- **p** (*float*) – defaults to `2`

    p-norm value for the Minkowski metric. When `p=1`, this corresponds to the Manhattan distance, while `p=2` corresponds to the Euclidean distance. Valid values are in the interval $[1, +\infty)$

- **weighted** (*bool*) – defaults to `True`

    Whether to weight the contribution of each neighbor by it's inverse distance or not.

- **kwargs**

    Other parameters passed to `scipy.spatial.cKDTree`.



## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import metrics
>>> from river import neighbors
>>> from river import preprocessing

>>> dataset = datasets.Phishing()

>>> model = (
...     preprocessing.StandardScaler() |
...     neighbors.KNNClassifier()
... )

>>> metric = metrics.Accuracy()

>>> evaluate.progressive_val_score(dataset, model, metric)
Accuracy: 88.07%
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update the model with a set of features `x` and a label `y`.

    **Parameters**

    - **x**    
    - **y**    
    
    **Returns**

    self
    
???- note "predict_one"

    Predict the label of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Union[bool, str, int]*:     The predicted label.
    
???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    proba
    
???- note "reset"

    Reset estimator. 

    
## Notes

This estimator is not optimal for a mixture of categorical and numerical
features. This implementation treats all features from a given stream as
numerical.


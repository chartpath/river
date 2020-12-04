# AdaptiveRandomForestRegressor

Adaptive Random Forest regressor.

The 3 most important aspects of Adaptive Random Forest [^1] are: 

1. inducing diversity through re-sampling 

2. inducing diversity through randomly selecting subsets of features for    node splits 

3. drift detectors per base tree, which cause selective resets in response    to drifts 

Notice that this implementation is slightly different from the original algorithm proposed in [^2]. The `HoeffdingTreeRegressor` is used as base learner, instead of `FIMT-DD`. It also adds a new strategy to monitor the predictions and check for concept drifts. The deviations of the predictions to the target are monitored and normalized in the [0, 1] range to fulfill ADWIN's requirements. We assume that the data subjected to the normalization follows a normal distribution, and thus, lies within the interval of the mean $\pm3\sigma$.

## Parameters

- **n_models** (*int*) – defaults to `10`

    Number of trees in the ensemble.

- **max_features** – defaults to `sqrt`

    Max number of attributes for each node split.<br/> - If `int`, then consider `max_features` at each split.<br/> - If `float`, then `max_features` is a percentage and   `int(max_features * n_features)` features are considered per split.<br/> - If "sqrt", then `max_features=sqrt(n_features)`.<br/> - If "log2", then `max_features=log2(n_features)`.<br/> - If None, then ``max_features=n_features``.

- **aggregation_method** (*str*) – defaults to `median`

    The method to use to aggregate predictions in the ensemble.<br/> - 'mean'<br/> - 'median' - If selected will disable the weighted vote.

- **lambda_value** (*int*) – defaults to `6`

    The lambda value for bagging (lambda=6 corresponds to Leveraging Bagging).

- **metric** (*river.metrics.base.RegressionMetric*) – defaults to `MSE: 0.`

    Metric used to track trees performance within the ensemble. Depending, on the configuration, this metric is also used to weight predictions from the members of the ensemble.

- **disable_weighted_vote** – defaults to `False`

    If `True`, disables the weighted vote prediction, i.e. does not assign weights to individual tree's predictions and uses the arithmetic mean instead. Otherwise will use the `metric` value to weight predictions.

- **drift_detector** (*[base.DriftDetector](../../base/DriftDetector)*) – defaults to `ADWIN`

    Drift Detection method. Set to None to disable Drift detection.

- **warning_detector** (*[base.DriftDetector](../../base/DriftDetector)*) – defaults to `ADWIN`

    Warning Detection method. Set to None to disable warning detection.

- **max_size** (*int*) – defaults to `100`

    [*Tree parameter*] Maximum memory (MB) consumed by the tree.

- **memory_estimate_period** (*int*) – defaults to `2000000`

    [*Tree parameter*] Number of instances between memory consumption checks.

- **grace_period** (*int*) – defaults to `50`

    [*Tree parameter*] Number of instances a leaf should observe between split attempts.

- **split_confidence** (*float*) – defaults to `0.01`

    [*Tree parameter*] Allowed error in split decision, a value closer to 0 takes longer to decide.

- **tie_threshold** (*float*) – defaults to `0.05`

    [*Tree parameter*] Threshold below which a split will be forced to break ties.

- **binary_split** (*bool*) – defaults to `False`

    [*Tree parameter*] If True, only allow binary splits.

- **stop_mem_management** (*bool*) – defaults to `False`

    [*Tree parameter*] If True, stop growing as soon as memory limit is hit.

- **remove_poor_attrs** (*bool*) – defaults to `False`

    [*Tree parameter*] If True, disable poor attributes.

- **merit_preprune** (*bool*) – defaults to `True`

    [*Tree parameter*] If True, disable pre-pruning.

- **leaf_prediction** (*str*) – defaults to `model`

    [*Tree parameter*] Prediction mechanism used at leaves.</br> - 'mean' - Target mean</br> - 'model' - Uses the model defined in `leaf_model`</br> - 'adaptive' - Chooses between 'mean' and 'model' dynamically</br>

- **leaf_model** (*[base.Regressor](../../base/Regressor)*) – defaults to `None`

    [*Tree parameter*] The regression model used to provide responses if `leaf_prediction='model'`. If not provided, an instance of `river.linear_model.LinearRegression` with the default hyperparameters  is used.

- **model_selector_decay** (*float*) – defaults to `0.95`

    The exponential decaying factor applied to the learning models' squared errors, that are monitored if `leaf_prediction='adaptive'`. Must be between `0` and `1`. The closer to `1`, the more importance is going to be given to past observations. On the other hand, if its value approaches `0`, the recent observed errors are going to have more influence on the final decision.

- **nominal_attributes** (*list*) – defaults to `None`

    [*Tree parameter*] List of Nominal attributes. If empty, then assume that all attributes are numerical.

- **attr_obs** (*str*) – defaults to `e-bst`

    [*Tree parameter*] The attribute observer (AO) used to monitor the target statistics of numeric features and perform splits. Parameters can be passed to the AOs (when supported) by using `attr_obs_params`. Valid options are:</br> - `'e-bst'`: Extended Binary Search Tree (E-BST). This AO has no parameters.</br> See notes for more information about the supported AOs.

- **attr_obs_params** (*dict*) – defaults to `None`

    [*Tree parameter*] Parameters passed to the numeric AOs. See `attr_obs` for more information.

- **min_samples_split** (*int*) – defaults to `5`

    [*Tree parameter*] The minimum number of samples every branch resulting from a split candidate must have to be considered valid.

- **max_depth** (*int*) – defaults to `None`

    [*Tree parameter*] The maximum depth a tree can reach. If `None`, the tree will grow indefinitely.

- **seed** – defaults to `None`

    If `int`, `seed` is used to seed the random number generator; If `RandomState`, `seed` is the random number generator; If `None`, the random number generator is the `RandomState` instance used by `np.random`.


## Attributes

- **valid_aggregation_method**

    Valid aggregation_method values.


## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import metrics
>>> from river import ensemble
>>> from river import preprocessing

>>> dataset = datasets.TrumpApproval()

>>> model = (
...     preprocessing.StandardScaler() |
...     ensemble.AdaptiveRandomForestRegressor(n_models=3, seed=42)
... )

>>> metric = metrics.MAE()

>>> evaluate.progressive_val_score(dataset, model, metric)
MAE: 23.320694
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

???- note "predict_one"

    Predicts the target value of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *Number*:     The prediction.
    
???- note "reset"

    Reset the forest.

    
## Notes

Hoeffding trees rely on Attribute Observer (AO) algorithms to monitor input features
and perform splits. Nominal features can be easily dealt with, since the partitions
are well-defined. Numerical features, however, require more sophisticated solutions.
Currently, only one AO is supported in `river` for regression trees:

- The Extended Binary Search Tree (E-BST) uses an exhaustive algorithm to find split
candidates, similarly to batch decision tree algorithms. It ends up storing all
observations between split attempts. However, E-BST automatically removes bad split
points periodically from its structure and, thus, alleviates the memory and time
costs involved in its usage.

## References

[^1]: Gomes, H.M., Bifet, A., Read, J., Barddal, J.P., Enembreck, F.,
      Pfharinger, B., Holmes, G. and Abdessalem, T., 2017. Adaptive random
      forests for evolving data stream classification. Machine Learning,
      106(9-10), pp.1469-1495.

[^2]: Gomes, H.M., Barddal, J.P., Boiko, L.E., Bifet, A., 2018.
      Adaptive random forests for data stream regression. ESANN 2018.


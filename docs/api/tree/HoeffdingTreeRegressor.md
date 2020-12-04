# HoeffdingTreeRegressor

Hoeffding Tree regressor.



## Parameters

- **grace_period** (*int*) – defaults to `200`

    Number of instances a leaf should observe between split attempts.

- **max_depth** (*int*) – defaults to `None`

    The maximum depth a tree can reach. If `None`, the tree will grow indefinitely.

- **split_confidence** (*float*) – defaults to `1e-07`

    Allowed error in split decision, a value closer to 0 takes longer to decide.

- **tie_threshold** (*float*) – defaults to `0.05`

    Threshold below which a split will be forced to break ties.

- **leaf_prediction** (*str*) – defaults to `model`

    Prediction mechanism used at leafs.</br> - 'mean' - Target mean</br> - 'model' - Uses the model defined in `leaf_model`</br> - 'adaptive' - Chooses between 'mean' and 'model' dynamically</br>

- **leaf_model** (*[base.Regressor](../../base/Regressor)*) – defaults to `None`

    The regression model used to provide responses if `leaf_prediction='model'`. If not provided an instance of `river.linear_model.LinearRegression` with the default hyperparameters is used.

- **model_selector_decay** (*float*) – defaults to `0.95`

    The exponential decaying factor applied to the learning models' squared errors, that are monitored if `leaf_prediction='adaptive'`. Must be between `0` and `1`. The closer to `1`, the more importance is going to be given to past observations. On the other hand, if its value approaches `0`, the recent observed errors are going to have more influence on the final decision.

- **nominal_attributes** (*list*) – defaults to `None`

    List of Nominal attributes identifiers. If empty, then assume that all numeric attributes should be treated as continuous.

- **attr_obs** (*str*) – defaults to `e-bst`

    The attribute observer (AO) used to monitor the target statistics of numeric features and perform splits. Parameters can be passed to the AOs (when supported) by using `attr_obs_params`. Valid options are:</br> - `'e-bst'`: Extended Binary Search Tree (E-BST). This AO has no parameters.</br> See notes for more information about the supported AOs.

- **attr_obs_params** (*dict*) – defaults to `None`

    Parameters passed to the numeric AOs. See `attr_obs` for more information.

- **min_samples_split** (*int*) – defaults to `5`

    The minimum number of samples every branch resulting from a split candidate must have to be considered valid.

- **kwargs**

    Other parameters passed to `river.tree.BaseHoeffdingTree`.


## Attributes

- **depth**

    The depth of the tree.

- **leaf_prediction**

    Return the prediction strategy used by the tree at its leaves.

- **max_size**

    Max allowed size tree can reach (in MB).

- **model_measurements**

    Collect metrics corresponding to the current status of the tree in a string buffer.

- **split_criterion**

    Return a string with the name of the split criterion being used by the tree.


## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import metrics
>>> from river import tree
>>> from river import preprocessing

>>> dataset = datasets.TrumpApproval()

>>> model = (
...     preprocessing.StandardScaler() |
...     tree.HoeffdingTreeRegressor(
...         grace_period=100,
...         leaf_prediction='adaptive',
...         model_selector_decay=0.9
...     )
... )

>>> metric = metrics.MAE()

>>> evaluate.progressive_val_score(dataset, model, metric)
MAE: 0.852902
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "debug_one"

    Print an explanation of how `x` is predicted.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Union[str, NoneType]*:     A representation of the path followed by the tree to predict `x`; `None` if
    
???- note "draw"

    Draw the tree using the `graphviz` library.

    Since the tree is drawn without passing incoming samples, classification trees will show the majority class in their leaves, whereas regression trees will use the target mean.

    **Parameters**

    - **max_depth**     (*int*)     – defaults to `None`    
        The maximum depth a tree can reach. If `None`, the tree will grow indefinitely.
    
???- note "learn_one"

    Train the tree model on sample x and corresponding target y.

    **Parameters**

    - **x**    
    - **y**    
    - **sample_weight**     – defaults to `1.0`    
    
    **Returns**

    self
    
???- note "model_description"

    Walk the tree and return its structure in a buffer.

    
    **Returns**

    The description of the model.
    
???- note "predict_one"

    Predict the target value using one of the leaf prediction strategies.

    **Parameters**

    - **x**    
    
    **Returns**

    Predicted target value.
    
## Notes

The Hoeffding Tree Regressor (HTR) is an adaptation of the incremental tree algorithm of the
same name for classification. Similarly to its classification counterpart, HTR uses the
Hoeffding bound to control its split decisions. Differently from the classification algorithm,
HTR relies on calculating the reduction of variance in the target space to decide among the
split candidates. The smallest the variance at its leaf nodes, the more homogeneous the
partitions are. At its leaf nodes, HTR fits either linear models or uses the target
average as the predictor.

Hoeffding trees rely on Attribute Observer (AO) algorithms to monitor input features
and perform splits. Nominal features can be easily dealt with, since the partitions
are well-defined. Numerical features, however, require more sophisticated solutions.
Currently, only one AO is supported in `river` for regression trees:

- The Extended Binary Search Tree (E-BST) uses an exhaustive algorithm to find split
candidates, similarly to batch decision tree algorithms. It ends up storing all
observations between split attempts. However, E-BST automatically removes bad split
points periodically from its structure and, thus, alleviates the memory and time
costs involved in its usage.


# iSOUPTreeRegressor

Incremental Structured Output Prediction Tree (iSOUP-Tree) for multi-target regression.

This is an implementation of the iSOUP-Tree proposed by A. Osojnik, P. Panov, and S. Džeroski [^1].

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

- **leaf_model** (*Union[[base.Regressor](../../base/Regressor), Dict]*) – defaults to `None`

    The regression model(s) used to provide responses if `leaf_prediction='model'`. It can be either a regressor (in which case it is going to be replicated to all the targets) or a dictionary whose keys are target identifiers, and the values are instances of `river.base.Regressor.` If not provided, instances of `river.linear_model.LinearRegression` with the default hyperparameters are used for all the targets. If a dictionary is passed and not all target models are specified, copies from the first model match in the dictionary will be used to the remaining targets.

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
>>> import numbers
>>> from river import compose
>>> from river import datasets
>>> from river import evaluate
>>> from river import linear_model
>>> from river import metrics
>>> from river import preprocessing
>>> from river import tree

>>> dataset = datasets.SolarFlare()

>>> num = compose.SelectType(numbers.Number) | preprocessing.MinMaxScaler()
>>> cat = compose.SelectType(str) | preprocessing.OneHotEncoder(sparse=False)

>>> model = tree.iSOUPTreeRegressor(
...     grace_period=100,
...     leaf_prediction='model',
...     leaf_model={
...         'c-class-flares': linear_model.LinearRegression(l2=0.02),
...         'm-class-flares': linear_model.PARegressor(),
...         'x-class-flares': linear_model.LinearRegression(l2=0.1)
...     }
... )

>>> pipeline = (num + cat) | model
>>> metric = metrics.RegressionMultiOutput(metrics.MAE())

>>> evaluate.progressive_val_score(dataset, pipeline, metric)
MAE: 0.425929
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

    Incrementally train the model with one sample.

    Training tasks:  * If the tree is empty, create a leaf node as the root. * If the tree is already initialized, find the corresponding leaf for   the instance and update the leaf node statistics. * If growth is allowed and the number of instances that the leaf has   observed between split attempts exceed the grace period then attempt   to split.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*Dict[Hashable, numbers.Number]*)    
    - **sample_weight**     (*float*)     – defaults to `1.0`    
    
???- note "model_description"

    Walk the tree and return its structure in a buffer.

    
    **Returns**

    The description of the model.
    
???- note "predict_one"

    Predict the target values for a given instance.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Dict[typing.Hashable, numbers.Number]*:     dict
    
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

[^1]: Aljaž Osojnik, Panče Panov, and Sašo Džeroski. "Tree-based methods for online
    multi-target regression." Journal of Intelligent Information Systems 50.2 (2018): 315-339.


# HoeffdingAdaptiveTreeClassifier

Hoeffding Adaptive Tree classifier.



## Parameters

- **grace_period** (*int*) – defaults to `200`

    Number of instances a leaf should observe between split attempts.

- **max_depth** (*int*) – defaults to `None`

    The maximum depth a tree can reach. If `None`, the tree will grow indefinitely.

- **split_criterion** (*str*) – defaults to `info_gain`

    Split criterion to use.</br> - 'gini' - Gini</br> - 'info_gain' - Information Gain</br> - 'hellinger' - Helinger Distance</br>

- **split_confidence** (*float*) – defaults to `1e-07`

    Allowed error in split decision, a value closer to 0 takes longer to decide.

- **tie_threshold** (*float*) – defaults to `0.05`

    Threshold below which a split will be forced to break ties.

- **leaf_prediction** (*str*) – defaults to `nba`

    Prediction mechanism used at leafs.</br> - 'mc' - Majority Class</br> - 'nb' - Naive Bayes</br> - 'nba' - Naive Bayes Adaptive</br>

- **nb_threshold** (*int*) – defaults to `0`

    Number of instances a leaf should observe before allowing Naive Bayes.

- **nominal_attributes** (*list*) – defaults to `None`

    List of Nominal attributes. If empty, then assume that all numeric attributes should be treated as continuous.

- **attr_obs** (*str*) – defaults to `gaussian`

    The Attribute Observer (AO) used to monitor the class statistics of numeric features and perform splits. Parameters can be passed to the AOs (when supported) by using `attr_obs_params`. Valid options are:</br> - `'bst'`: Binary Search Tree.</br> - `'gaussian'`: Gaussian observer. The `n_splits` used to query  for split candidates can be adjusted (defaults to `10`).</br> - `'histogram'`: Histogram-based class frequency estimation.  The number of histogram bins (`n_bins` -- defaults to `256`) and the number of split point candidates to evaluate (`n_splits` -- defaults to `32`) can be adjusted.</br> See 'Notes' for more information about the AOs.

- **attr_obs_params** (*dict*) – defaults to `None`

    Parameters passed to the numeric AOs. See `attr_obs` for more information.

- **bootstrap_sampling** (*bool*) – defaults to `True`

    If True, perform bootstrap sampling in the leaf nodes.

- **drift_window_threshold** (*int*) – defaults to `300`

    Minimum number of examples an alternate tree must observe before being considered as a potential replacement to the current one.

- **adwin_confidence** (*float*) – defaults to `0.002`

    The delta parameter used in the nodes' ADWIN drift detectors.

- **seed** – defaults to `None`

    If int, `seed` is the seed used by the random number generator;</br> If RandomState instance, `seed` is the random number generator;</br> If None, the random number generator is the RandomState instance used by `np.random`. Only used when `bootstrap_sampling=True` to direct the bootstrap sampling.</br>

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
>>> from river import synth
>>> from river import evaluate
>>> from river import metrics
>>> from river import tree

>>> gen = synth.ConceptDriftStream(stream=synth.SEA(seed=42, variant=0),
...                                drift_stream=synth.SEA(seed=42, variant=1),
...                                seed=1, position=500, width=50)
>>> # Take 1000 instances from the infinite data generator
>>> dataset = iter(gen.take(1000))

>>> model = tree.HoeffdingAdaptiveTreeClassifier(
...     grace_period=100,
...     split_confidence=1e-5,
...     leaf_prediction='nb',
...     nb_threshold=10,
...     seed=0
... )

>>> metric = metrics.Accuracy()

>>> evaluate.progressive_val_score(dataset, model, metric)
Accuracy: 91.09%
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

    Train the model on instance x and corresponding target y.

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

    A dictionary that associates a probability which each label.
    
## Notes

The Hoeffding Adaptive Tree [^1] uses ADWIN [^2] to monitor performance of branches on the tree
and to replace them with new branches when their accuracy decreases if the new branches are
more accurate.

The bootstrap sampling strategy is an improvement over the original Hoeffding Adaptive Tree
algorithm. It is enabled by default since, in general, it results in better performance.

Hoeffding trees rely on Attribute Observer (AO) algorithms to monitor input features
and perform splits. Nominal features can be easily dealt with, since the partitions
are well-defined. Numerical features, however, require more sophisticated solutions.
Currently, three AOs are supported in `river` for classification trees:

- *Binary Search Tree (BST)*: uses an exhaustive algorithm to find split candidates,
similarly to batch decision trees. It ends up storing all observations between split
attempts. This AO is the most costly one in terms of memory and processing
time; however, it tends to yield the most accurate results when using `leaf_prediction=mc`.
It cannot be used to calculate the Probability Density Function (PDF) of the monitored
feature due to its binary tree nature. Hence, leaf prediction strategies other than
the majority class will end up effectively mimicing the majority class classifier.
This AO has no parameters.</br>
- *Gaussian Estimator*: Approximates the numeric feature distribution by using
a Gaussian distribution per class. The Cumulative Distribution Function (CDF) necessary to
calculate the entropy (and, consequently, the information gain), the gini index, and
other split criteria is then calculated using the fit feature's distribution.</br>
- *Histogram*: approximates the numeric feature distribution using an incrementally
maintained histogram per class. It represents a compromise between the intensive
resource usage of BST and the strong assumptions about the feature's distribution
used in the Gaussian Estimator. Besides that, this AO sits in the middle between the
previous two in terms of memory usage and running time. Note that the number of
bins affects the probability density approximation required to use leaves with
(adaptive) naive bayes models. Hence, Histogram tends to be less accurate than the
Gaussian estimator when adaptive or naive bayes leaves are used.

## References

[^1]: Bifet, Albert, and Ricard Gavaldà. "Adaptive learning from evolving data streams."
   In International Symposium on Intelligent Data Analysis, pp. 249-260. Springer, Berlin,
   Heidelberg, 2009.
[^2]: Bifet, Albert, and Ricard Gavaldà. "Learning from time-changing data with adaptive
   windowing." In Proceedings of the 2007 SIAM international conference on data mining,
   pp. 443-448. Society for Industrial and Applied Mathematics, 2007.


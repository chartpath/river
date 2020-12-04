# KNNADWINClassifier

K-Nearest Neighbors classifier with ADWIN change detector.

This classifier is an improvement from the regular kNN method, as it is resistant to concept drift. It uses the `ADWIN` change detector to decide which samples to keep and which ones to forget, and by doing so it regulates the sample window size.

## Parameters

- **n_neighbors** – defaults to `5`

    The number of nearest neighbors to search for.

- **window_size** – defaults to `1000`

    The maximum size of the window storing the last viewed samples.

- **leaf_size** – defaults to `30`

    The maximum number of samples that can be stored in one leaf node, which determines from which point the algorithm will switch for a brute-force approach. The bigger this number the faster the tree construction time, but the slower the query time will be.

- **p** – defaults to `2`

    p-norm value for the Minkowski metric. When `p=1`, this corresponds to the Manhattan distance, while `p=2` corresponds to the Euclidean distance. Valid values are in the interval $[1, +\infty)$



## Examples

```python
>>> from river import synth
>>> from river import evaluate
>>> from river import metrics
>>> from river import neighbors

>>> dataset = synth.ConceptDriftStream(position=500, width=20, seed=1).take(1000)

>>> model = neighbors.KNNADWINClassifier(window_size=100)

>>> metric = metrics.Accuracy()

>>> evaluate.progressive_val_score(dataset, model, metric)
Accuracy: 57.36%
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

- This estimator is not optimal for a mixture of categorical and numerical
features. This implementation treats all features from a given stream as
numerical.
- This implementation is extended from the KNNClassifier, with the main
difference that it keeps a dynamic window whose size changes in agreement
with the amount of change detected by the ADWIN drift detector.


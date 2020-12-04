# SAMKNNClassifier

Self Adjusting Memory coupled with the kNN classifier.

The Self Adjusting Memory (SAM) [^1] model builds an ensemble with models targeting current or former concepts. SAM is built using two memories: STM for the current concept, and the LTM to retain information about past concepts. A cleaning process is in charge of controlling the size of the STM while keeping the information in the LTM consistent with the STM.

## Parameters

- **n_neighbors** (*int*) – defaults to `5`

    number of evaluated nearest neighbors.

- **distance_weighting** – defaults to `True`

    Type of weighting of the nearest neighbors. It `True`  will use 'distance'. Otherwise, will use 'uniform' (majority voting).

- **window_size** (*int*) – defaults to `5000`

    Maximum number of overall stored data points.

- **ltm_size** (*float*) – defaults to `0.4`

    Proportion of the overall instances that may be used for the LTM. This is  only relevant when the maximum number(maxSize) of stored instances is reached.

- **min_stm_size** (*int*) – defaults to `50`

    Minimum STM size which is evaluated during the STM size adaption.

- **stm_aprox_adaption** – defaults to `True`

    Type of STM size adaption.<br/>     - If `True` approximates the interleaved test-train error and is        significantly faster than the exact version.<br/>     - If `False` calculates the interleaved test-train error exactly for each of the       evaluated window sizes, which often has to be recalculated from the scratch.<br/>     - If `None`, the STM is not  adapted at all. If additionally `use_ltm=False`, then       this algorithm is simply a kNN with fixed sliding window size.

- **use_ltm** – defaults to `True`

    Specifies whether the LTM should be used at all.


## Attributes

- **LTMLabels**

    Class labels in the LTM.

- **LTMSamples**

    Samples in the LTM.

- **STMLabels**

    Class labels in the STM.

- **STMSamples**

    Samples in the STM.


## Examples

```python
>>> from river import synth
>>> from river import evaluate
>>> from river import metrics
>>> from river import neighbors

>>> dataset = synth.ConceptDriftStream(position=500, width=20, seed=1).take(1000)

>>> model = neighbors.SAMKNNClassifier(window_size=100)

>>> metric = metrics.Accuracy()

>>> evaluate.progressive_val_score(dataset, model, metric)
Accuracy: 59.90%
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update the model with a set of features `x` and a label `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*Union[bool, str, int]*)    
    
    **Returns**

    *Classifier*:     self
    
???- note "predict_one"

    Predict the label of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Union[bool, str, int]*:     The predicted label.
    
???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Dict[typing.Union[bool, str, int], float]*:     A dictionary that associates a probability which each label.
    
## Notes

This modules uses libNearestNeighbor, a C++ library used to speed up some of
the algorithm's computations. When invoking the library's functions it's important 
to pass the right argument type. Although most of this framework's functionality
will work with python standard types, the C++ library will work with 8-bit labels, 
which is already done by the SAMKNN class, but may be absent in custom classes that
use SAMKNN static methods, or other custom functions that use the C++ library.

## References

[^1]: Losing, Viktor, Barbara Hammer, and Heiko Wersing.
      "Knn classifier with self adjusting memory for heterogeneous concept drift."
      In Data Mining (ICDM), 2016 IEEE 16th International Conference on,
      pp. 291-300. IEEE, 2016.


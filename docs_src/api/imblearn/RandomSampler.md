# RandomSampler

Random sampling by mixing under-sampling and over-sampling.

This is a wrapper for classifiers. It will train the provided classifier by both under-sampling and over-sampling the stream of given observations so that the class distribution seen by the classifier follows a given desired distribution.

## Parameters

- **classifier** (*[base.Classifier](../../base/Classifier)*)

- **desired_dist** (*dict*)

    The desired class distribution. The keys are the classes whilst the values are the desired class percentages. The values must sum up to 1. If set to `None`, then the observations will be sampled uniformly at random, which is stricly equivalent to using `ensemble.BaggingClassifier`.

- **sampling_rate** – defaults to `1.0`

    The desired ratio of data to sample.

- **seed** (*int*) – defaults to `None`

    Random seed for reproducibility.




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

    - **x**    
    
    **Returns**

    The predicted label.
    
???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    A dictionary that associates a probability which each label.
    

# RandomOverSampler

Random over-sampling.

This is a wrapper for classifiers. It will train the provided classifier by over-sampling the stream of given observations so that the class distribution seen by the classifier follows a given desired distribution. The implementation is a discrete version of reverse rejection sampling.

## Parameters

- **classifier** (*[base.Classifier](../../base/Classifier)*)

- **desired_dist** (*dict*)

    The desired class distribution. The keys are the classes whilst the values are the desired class percentages. The values must sum up to 1.

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
    

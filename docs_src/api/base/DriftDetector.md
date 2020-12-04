# DriftDetector

A drift detector.




## Attributes

- **change_detected**

    Concept drift alarm.  True if concept drift is detected.

- **warning_detected**

    Warning zone alarm.  Indicates if the drift detector is in the warning zone. Applicability depends on each drift detector implementation. True if the change detector is in the warning zone.



## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "reset"

    Reset the change detector.

    
???- note "update"

    Update the change detector with a single data point.

    **Parameters**

    - **value**     (*numbers.Number*)    
    
    **Returns**

    *typing.Tuple[bool, bool]*:     A tuple (drift, warning) where its elements indicate if a drift or a warning is detected.
    

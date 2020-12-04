# PageHinkley

Page-Hinkley method for concept drift detection.

This change detection method works by computing the observed values and their mean up to the current moment. Page-Hinkley does not signal warning zones, only change detections. The method works by means of the Page-Hinkley test. In general lines it will detect a concept drift if the observed mean at some instant is greater then a threshold value lambda.

## Parameters

- **min_instances** – defaults to `30`

    The minimum number of instances before detecting change.

- **delta** – defaults to `0.005`

    The delta factor for the Page Hinkley test.

- **threshold** – defaults to `50`

    The change detection threshold (lambda).

- **alpha** – defaults to `0.9999`

    The forgetting factor, used to weight the observed value and the mean.


## Attributes

- **change_detected**

    Concept drift alarm.  True if concept drift is detected.

- **warning_detected**

    Warning zone alarm.  Indicates if the drift detector is in the warning zone. Applicability depends on each drift detector implementation. True if the change detector is in the warning zone.


## Examples

```python
>>> import numpy as np
>>> from river.drift import PageHinkley
>>> np.random.seed(12345)

>>> ph = PageHinkley()

>>> # Simulate a data stream composed by two data distributions
>>> data_stream = np.concatenate((np.random.randint(2, size=1000),
...                               np.random.randint(4, high=8, size=1000)))

>>> # Update drift detector and verify if change is detected
>>> for i, val in enumerate(data_stream):
...     in_drift, in_warning = ph.update(val)
...     if in_drift:
...         print(f"Change detected at index {i}, input value: {val}")
Change detected at index 1009, input value: 5
```

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

    *tuple*:     A tuple (drift, warning) where its elements indicate if a drift or a warning is detected.
    
## References

[^1]: E. S. Page. 1954. Continuous Inspection Schemes. Biometrika 41, 1/2 (1954), 100–115.


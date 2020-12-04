# HDDM_A

Drift Detection Method based on Hoeffding’s bounds with moving average-test.

HDDM_A is a drift detection method based on the Hoeffding’s inequality. HDDM_A uses the average as estimator. It receives as input a stream of real values and returns the estimated status of the stream: STABLE, WARNING or DRIFT. 

**Input:** `value` must be a binary signal, where 0 indicates error. For example, if a classifier's prediction $y'$ is right or wrong w.r.t the true target label $y$: 

- 0: Correct, $y=y'$ 

- 1: Error, $y \neq y'$ 

*Implementation based on MOA.*

## Parameters

- **drift_confidence** – defaults to `0.001`

    Confidence to the drift

- **warning_confidence** – defaults to `0.005`

    Confidence to the warning

- **two_sided_test** – defaults to `False`

    If `True`, will monitor error increments and decrements (two-sided). By default will only monitor increments (one-sided).


## Attributes

- **change_detected**

    Concept drift alarm.  True if concept drift is detected.

- **warning_detected**

    Warning zone alarm.  Indicates if the drift detector is in the warning zone. Applicability depends on each drift detector implementation. True if the change detector is in the warning zone.


## Examples

```python
>>> import numpy as np
>>> from river.drift import HDDM_A
>>> np.random.seed(12345)

>>> hddm_a = HDDM_A()

>>> # Simulate a data stream as a normal distribution of 1's and 0's
>>> data_stream = np.random.randint(2, size=2000)
>>> # Change the data distribution from index 999 to 1500, simulating an
>>> # increase in error rate (1 indicates error)
>>> data_stream[999:1500] = 1

>>> # Update drift detector and verify if change is detected
>>> for i, val in enumerate(data_stream):
...     in_drift, in_warning = hddm_a.update(val)
...     if in_drift:
...         print(f"Change detected at index {i}, input value: {val}")
Change detected at index 1013, input value: 1
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

[^1]: Frías-Blanco I, del Campo-Ávila J, Ramos-Jimenez G, et al. Online and non-parametric drift detection methods based on Hoeffding’s bounds. IEEE Transactions on Knowledge and Data Engineering, 2014, 27(3): 810-823.
[^2]: Albert Bifet, Geoff Holmes, Richard Kirkby, Bernhard Pfahringer. MOA: Massive Online Analysis; Journal of Machine Learning Research 11: 1601-1604, 2010.


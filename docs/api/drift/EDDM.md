# EDDM

Early Drift Detection Method.

EDDM (Early Drift Detection Method) aims to improve the detection rate of gradual concept drift in DDM, while keeping a good performance against abrupt concept drift. 

This method works by keeping track of the average distance between two errors instead of only the error rate. For this, it is necessary to keep track of the running average distance and the running standard deviation, as well as the maximum distance and the maximum standard deviation. 

The algorithm works similarly to the DDM algorithm, by keeping track of statistics only. It works with the running average distance ($p_i'$) and the running standard deviation ($s_i'$), as well as $p'_{max}$ and $s'_{max}$, which are the values of $p_i'$ and $s_i'$ when $(p_i' + 2 * s_i')$ reaches its maximum. 

Like DDM, there are two threshold values that define the borderline between no change, warning zone, and drift detected. These are as follows: 

* if $(p_i' + 2 * s_i')/(p'_{max} + 2 * s'_{max}) < \alpha$ -> Warning zone 

* if $(p_i' + 2 * s_i')/(p'_{max} + 2 * s'_{max}) < \beta$ -> Change detected 

$\alpha$ and $\beta$ are set to 0.95 and 0.9, respectively. 

**Input:** `value` must be a binary signal, where 0 indicates error. For example, if a classifier's prediction $y'$ is right or wrong w.r.t the true target label $y$: 

- 0: Correct, $y=y'$ 

- 1: Error, $y \neq y'$


## Attributes

- **change_detected**

    Concept drift alarm.  True if concept drift is detected.

- **warning_detected**

    Warning zone alarm.  Indicates if the drift detector is in the warning zone. Applicability depends on each drift detector implementation. True if the change detector is in the warning zone.


## Examples

```python
>>> import numpy as np
>>> from river.drift import EDDM
>>> np.random.seed(12345)

>>> eddm = EDDM()

>>> # Simulate a data stream as a normal distribution of 1's and 0's
>>> data_stream = np.random.randint(2, size=2000)
>>> # Change the data distribution from index 999 to 1500, simulating an
>>> # increase in error rate (1 indicates error)
>>> data_stream[999:1500] = 1

>>> # Update drift detector and verify if change is detected
>>> for i, val in enumerate(data_stream):
...     in_drift, in_warning = eddm.update(val)
...     if in_drift:
...         print(f"Change detected at index {i}, input value: {val}")
Change detected at index 53, input value: 1
Change detected at index 121, input value: 1
Change detected at index 185, input value: 1
Change detected at index 272, input value: 1
Change detected at index 336, input value: 1
Change detected at index 391, input value: 1
Change detected at index 571, input value: 1
Change detected at index 627, input value: 1
Change detected at index 686, input value: 1
Change detected at index 754, input value: 1
Change detected at index 1033, input value: 1
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

[^1]: Early Drift Detection Method. Manuel Baena-Garcia, Jose Del Campo-Avila, Raúl Fidalgo, Albert Bifet, Ricard Gavalda, Rafael Morales-Bueno. In Fourth International Workshop on Knowledge Discovery from Data Streams, 2006.


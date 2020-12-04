# ADWIN

Adaptive Windowing method for concept drift detection.

ADWIN (ADaptive WINdowing) is a popular drift detection method with mathematical guarantees. ADWIN efficiently keeps a variable-length window of recent items; such that it holds that there has no been change in the data distribution. This window is further divided into two sub-windows $(W_0, W_1)$ used to determine if a change has happened. ADWIN compares the average of $W_0$ and $W_1$ to confirm that they correspond to the same distribution. Concept drift is detected if the distribution equality no longer holds. Upon detecting a drift, $W_0$ is replaced by $W_1$ and a new $W_1$ is initialized. ADWIN uses a confidence value $\delta=\in(0,1)$ to determine if the two sub-windows correspond to the same distribution. 

**Input**: `value` can be any numeric value related to the definition of concept change for the data analyzed. For example, using 0's or 1's to track drift in a classifier's performance as follows: 

- 0: Means the learners prediction was wrong 

- 1: Means the learners prediction was correct

## Parameters

- **delta** – defaults to `0.002`

    Confidence value.


## Attributes

- **change_detected**

    Concept drift alarm.  True if concept drift is detected.

- **estimation**

    Error estimation

- **n_detections**

- **variance**

- **warning_detected**

    Warning zone alarm.  Indicates if the drift detector is in the warning zone. Applicability depends on each drift detector implementation. True if the change detector is in the warning zone.

- **width**

    Window size


## Examples

```python
>>> import numpy as np
>>> from river.drift import ADWIN
>>> np.random.seed(12345)

>>> adwin = ADWIN()

>>> # Simulate a data stream composed by two data distributions
>>> data_stream = np.concatenate((np.random.randint(2, size=1000),
...                               np.random.randint(4, high=8, size=1000)))

>>> # Update drift detector and verify if change is detected
>>> for i, val in enumerate(data_stream):
...     in_drift, in_warning = adwin.update(val)
...     if in_drift:
...         print(f"Change detected at index {i}, input value: {val}")
Change detected at index 1023, input value: 5
Change detected at index 1055, input value: 7
Change detected at index 1087, input value: 5
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "reset"

    Reset the change detector.

    
???- note "update"

    Update the change detector with a single data point.

    Apart from adding the element value to the window, by inserting it in the correct bucket, it will also update the relevant statistics, in this case the total sum of all values, the window width and the total variance.

    **Parameters**

    - **value**     (*numbers.Number*)    
    
    **Returns**

    *typing.Tuple[bool, bool]*:     tuple
    
## References

[^1]: Bifet, Albert, and Ricard Gavalda. "Learning from time-changing data with adaptive windowing." In Proceedings of the 2007 SIAM international conference on data mining, pp. 443-448. Society for Industrial and Applied Mathematics, 2007.


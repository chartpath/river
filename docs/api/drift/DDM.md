# DDM

Drift Detection Method.

DDM (Drift Detection Method) is a concept change detection method based on the PAC learning model premise, that the learner's error rate will decrease as the number of analysed samples increase, as long as the data distribution is stationary. 

If the algorithm detects an increase in the error rate, that surpasses a calculated threshold, either change is detected or the algorithm will warn the user that change may occur in the near future, which is called the warning zone. 

The detection threshold is calculated in function of two statistics, obtained when $(p_i + s_i)$ is minimum: 

* $p_{min}$: The minimum recorded error rate. 

* $s_{min}$: The minimum recorded standard deviation. 

At instant $i$, the detection algorithm uses: 

* $p_i$: The error rate at instant $i$. 

* $s_i$: The standard deviation at instant $i$. 

The conditions for entering the warning zone and detecting change are as follows: 

* if $p_i + s_i \geq p_{min} + 2 * s_{min}$ -> Warning zone 

* if $p_i + s_i \geq p_{min} + 3 * s_{min}$ -> Change detected 

**Input:** `value` must be a binary signal, where 0 indicates error. For example, if a classifier's prediction $y'$ is right or wrong w.r.t the true target label $y$: 

- 0: Correct, $y=y'$ 

- 1: Error, $y \neq y'$

## Parameters

- **min_num_instances** – defaults to `30`

    The minimum required number of analyzed samples so change can be detected. This is used to avoid false detections during the early moments of the detector, when the weight of one sample is important.

- **warning_level** – defaults to `2.0`

    Warning level.

- **out_control_level** – defaults to `3.0`

    Out-control level.


## Attributes

- **change_detected**

    Concept drift alarm.  True if concept drift is detected.

- **warning_detected**

    Warning zone alarm.  Indicates if the drift detector is in the warning zone. Applicability depends on each drift detector implementation. True if the change detector is in the warning zone.


## Examples

```python
>>> import numpy as np
>>> from river.drift import DDM
>>> np.random.seed(12345)

>>> ddm = DDM()

>>> # Simulate a data stream as a normal distribution of 1's and 0's
>>> data_stream = np.random.randint(2, size=2000)
>>> # Change the data distribution from index 999 to 1500, simulating an
>>> # increase in error rate (1 indicates error)
>>> data_stream[999:1500] = 1

>>> # Update drift detector and verify if change is detected
>>> for i, val in enumerate(data_stream):
...     in_drift, in_warning = ddm.update(val)
...     if in_drift:
...         print(f"Change detected at index {i}, input value: {val}")
Change detected at index 1077, input value: 1
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
    
## References

[^1]: João Gama, Pedro Medas, Gladys Castillo, Pedro Pereira Rodrigues: Learning with Drift Detection. SBIA 2004: 286-295


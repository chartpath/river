# KSWIN

Kolmogorov-Smirnov Windowing method for concept drift detection.



## Parameters

- **alpha** – defaults to `0.005`

    Probability for the test statistic of the Kolmogorov-Smirnov-Test. The alpha parameter is very sensitive, therefore should be set below 0.01.

- **window_size** – defaults to `100`

    Size of the sliding window.

- **stat_size** – defaults to `30`

    Size of the statistic window.

- **window** – defaults to `None`

    Already collected data to avoid cold start.


## Attributes

- **change_detected**

    Concept drift alarm.  True if concept drift is detected.

- **warning_detected**

    Warning zone alarm.  Indicates if the drift detector is in the warning zone. Applicability depends on each drift detector implementation. True if the change detector is in the warning zone.


## Examples

```python
>>> import numpy as np
>>> from river.drift import KSWIN
>>> np.random.seed(12345)

>>> kswin = KSWIN()

>>> # Simulate a data stream composed by two data distributions
>>> data_stream = np.concatenate((np.random.randint(2, size=1000),
...                               np.random.randint(4, high=8, size=1000)))

>>> # Update drift detector and verify if change is detected
>>> for i, val in enumerate(data_stream):
...     in_drift, in_warning = kswin.update(val)
...     if in_drift:
...         print(f"Change detected at index {i}, input value: {val}")
Change detected at index 1014, input value: 5
Change detected at index 1828, input value: 6
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "reset"

    Reset the change detector.

    
???- note "update"

    Update the change detector with a single data point.

    Adds an element on top of the sliding window and removes the oldest one from the window. Afterwards, the KS-test is performed.

    **Parameters**

    - **value**     (*numbers.Number*)    
    
    **Returns**

    *tuple*:     A tuple (drift, warning) where its elements indicate if a drift or a warning is detected.
    
## Notes

KSWIN (Kolmogorov-Smirnov Windowing) is a concept change detection method based
on the Kolmogorov-Smirnov (KS) statistical test. KS-test is a statistical test with
no assumption of underlying data distribution. KSWIN can monitor data or performance
distributions. Note that the detector accepts one dimensional input as array.

KSWIN maintains a sliding window $\Psi$ of fixed size $n$ (window_size). The
last $r$ (stat_size) samples of $\Psi$ are assumed to represent the last
concept considered as $R$. From the first $n-r$ samples of $\Psi$,
$r$ samples are uniformly drawn, representing an approximated last concept $W$.

The KS-test is performed on the windows $R$ and $W$ of the same size. KS
-test compares the distance of the empirical cumulative data distribution $dist(R,W)$.

A concept drift is detected by KSWIN if:

$$
dist(R,W) > \sqrt{-rac{lnlpha}{r}}
$$

The difference in empirical data distributions between the windows $R$ and $W$ is too large
since $R$ and $W$ come from the same distribution.

## References

[^1]: Christoph Raab, Moritz Heusinger, Frank-Michael Schleif, Reactive Soft Prototype Computing for Concept Drift Streams, Neurocomputing, 2020,


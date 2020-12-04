# Hyperplane

Hyperplane stream generator.

Generates a problem of prediction class of a rotation hyperplane. It was used as testbed for CVFDT and VFDT in [^1]. 

A hyperplane in d-dimensional space is the set of points $x$ that satisfy 

$$\sum^{d}_{i=1} w_i x_i = w_0 = \sum^{d}_{i=1} w_i$$ 

where $x_i$ is the i-th coordinate of $x$. 

- Examples for which $\sum^{d}_{i=1} w_i x_i > w_0$, are labeled positive. 

- Examples for which $\sum^{d}_{i=1} w_i x_i \leq w_0$, are labeled negative. 

Hyperplanes are useful for simulating time-changing concepts because we can change the orientation and position of the hyperplane in a smooth manner by changing the relative size of the weights. We introduce change to this dataset by adding drift to each weighted feature $w_i = w_i + d \sigma$, where $\sigma$ is the probability that the direction of change is reversed and $d$ is the change applied to each example.

## Parameters

- **seed** (*int*) – defaults to `None`

    If int, `seed` is used to seed the random number generator; If RandomState instance, `seed` is the random number generator; If None, the random number generator is the `RandomState` instance used by `np.random`.

- **n_features** (*int*) – defaults to `10`

    The number of attributes to generate. Higher than 2.

- **n_drift_features** (*int*) – defaults to `2`

    The number of attributes with drift. Higher than 2.

- **mag_change** (*float*) – defaults to `0.0`

    Magnitude of the change for every example. From 0.0 to 1.0.

- **noise_percentage** (*float*) – defaults to `0.05`

    Percentage of noise to add to the data. From 0.0 to 1.0.

- **sigma** (*float*) – defaults to `0.1`

    Probability that the direction of change is reversed. From 0.0 to 1.0.


## Attributes

- **desc**

    Return the description from the docstring.


## Examples

```python
>>> from river import synth

>>> dataset = synth.Hyperplane(seed=42, n_features=2)

>>> for x, y in dataset.take(5):
...     print(x, y)
{0: 0.7319, 1: 0.5986} 1
{0: 0.8661, 1: 0.6011} 1
{0: 0.8324, 1: 0.2123} 0
{0: 0.5247, 1: 0.4319} 0
{0: 0.2921, 1: 0.3663} 0
```

## Methods

???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    
## Notes

The sample generation works as follows: The features are generated
with the random number generator, initialized with the seed passed by
the user. Then the classification function decides, as a function of
the sum of the weighted features and the sum of the weights, whether
the instance belongs to class 0 or class 1. The last step is to add
noise and generate drift.

## References

[^1]: G. Hulten, L. Spencer, and P. Domingos. Mining time-changing data streams.
      In KDD’01, pages 97–106, San Francisco, CA, 2001. ACM Press.


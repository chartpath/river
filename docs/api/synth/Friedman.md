# Friedman

Friedman synthetic dataset.

Each observation is composed of 10 features. Each feature value is sampled uniformly in [0, 1]. The target is defined by the following function: 

$$y = 10 sin(\pi x_0 x_1) + 20 (x_2 - .5)^2 + 10 x_3 + 5 x_4$$ 

Therefore, only the first 5 features are relevant.

## Parameters

- **seed** (*int*) – defaults to `None`

    Random seed number used for reproducibility.


## Attributes

- **desc**

    Return the description from the docstring.


## Examples

```python
>>> from river import synth

>>> dataset = synth.Friedman(seed=42)

>>> for x, y in dataset.take(5):
...     print(list(x.values()), y)
[0.63, 0.02, 0.27, 0.22, 0.73, 0.67, 0.89, 0.08, 0.42, 0.02] 7.42
[0.21, 0.50, 0.02, 0.19, 0.64, 0.54, 0.22, 0.58, 0.80, 0.00] 13.12
[0.80, 0.69, 0.34, 0.15, 0.95, 0.33, 0.09, 0.09, 0.84, 0.60] 16.65
[0.80, 0.72, 0.53, 0.97, 0.37, 0.55, 0.82, 0.61, 0.86, 0.57] 21.26
[0.70, 0.04, 0.22, 0.28, 0.07, 0.23, 0.10, 0.27, 0.63, 0.36] 5.78
```

## Methods

???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    
## References

[^1]: [Friedman, J.H., 1991. Multivariate adaptive regression splines. The annals of statistics, pp.1-67.](https://projecteuclid.org/euclid.aos/1176347963)


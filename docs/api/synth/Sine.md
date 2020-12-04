# Sine

Sine generator.

This generator is an implementation of the dara stream with abrupt concept drift, as described in Gama, Joao, et al. [^1]. 

It generates up to 4 relevant numerical features, that vary from 0 to 1, where only 2 of them are relevant to the classification task and the other 2 are optionally added by as noise. A classification function is chosen among four options: 

0. `SINE1`. Abrupt concept drift, noise-free examples. It has two relevant    attributes. Each attributes has values uniformly distributed in [0, 1].    In the first context all points below the curve $y = sin(x)$ are    classified as positive. 

1. `Reversed SINE1`. The reversed classification of `SINE1`. 

2. `SINE2`. The same two relevant attributes. The classification function    is $y < 0.5 + 0.3 sin(3 \pi  x)$. 

3. `Reversed SINE2`. The reversed classification of `SINE2`. 

Concept drift can be introduced by changing the classification function. This can be done manually or using `ConceptDriftStream`. 

Two important features are the possibility to balance classes, which means the class distribution will tend to a uniform one, and the possibility to add noise, which will, add two non relevant attributes.

## Parameters

- **classification_function** (*int*) – defaults to `0`

    Classification functions to use. From 0 to 3.

- **seed** (*int*) – defaults to `None`

    If int, `seed` is used to seed the random number generator; If RandomState instance, `seed` is the random number generator; If None, the random number generator is the `RandomState` instance used by `np.random`.

- **balance_classes** (*bool*) – defaults to `False`

    Whether to balance classes or not. If balanced, the class distribution will converge to an uniform distribution.

- **has_noise** (*bool*) – defaults to `False`

    Adds 2 non relevant features to the stream.


## Attributes

- **desc**

    Return the description from the docstring.


## Examples

```python
>>> from river import synth

>>> dataset = synth.Sine(classification_function = 2, seed = 112,
...                      balance_classes = False, has_noise = True)

>>> for x, y in dataset.take(5):
...     print(x, y)
{0: 0.3750, 1: 0.6403, 2: 0.9500, 3: 0.0756} 1
{0: 0.7769, 1: 0.8327, 2: 0.0548, 3: 0.8176} 1
{0: 0.8853, 1: 0.7223, 2: 0.0025, 3: 0.9811} 0
{0: 0.3434, 1: 0.0947, 2: 0.3946, 3: 0.0049} 1
{0: 0.7367, 1: 0.9558, 2: 0.8206, 3: 0.3449} 0
```

## Methods

???- note "generate_drift"

    Generate drift by switching the classification function at random.

    
???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    
## Notes

The sample generation works as follows: The two attributes are
generated with the random number generator. The classification function
defines whether to classify the instance as class 0 or class 1. Finally,
data is balanced and noise is added, if these options are set by the user.

The generated sample will have 2 relevant features, and an additional
two noise features if `has_noise` is set.

## References

[^1]: Gama, Joao, et al.'s 'Learning with drift detection.'
      Advances in artificial intelligence–SBIA 2004.
      Springer Berlin Heidelberg, 2004. 286-295."


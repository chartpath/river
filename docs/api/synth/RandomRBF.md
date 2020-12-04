# RandomRBF

Random Radial Basis Function generator.

Produces a radial basis function stream. A number of centroids, having a random central position, a standard deviation, a class label and weight are generated. A new sample is created by choosing one of the centroids at random, taking into account their weights, and offsetting the attributes in a random direction from the centroid's center. The offset length is drawn from a Gaussian distribution. 

This process will create a normally distributed hypersphere of samples on the surrounds of each centroid.

## Parameters

- **seed_model** (*int*) – defaults to `None`

    Model's seed to generate centroids If int, `seed` is used to seed the random number generator; If RandomState instance, `seed` is the random number generator; If None, the random number generator is the `RandomState` instance used by `np.random`.

- **seed_sample** (*int*) – defaults to `None`

    Sample's seed If int, `seed` is used to seed the random number generator; If RandomState instance, `seed` is the random number generator; If None, the random number generator is the `RandomState` instance used by `np.random`.

- **n_classes** (*int*) – defaults to `2`

    The number of class labels to generate.

- **n_features** (*int*) – defaults to `10`

    The number of numerical features to generate.

- **n_centroids** (*int*) – defaults to `50`

    The number of centroids to generate.


## Attributes

- **desc**

    Return the description from the docstring.


## Examples

```python
>>> from river import synth
>>>
>>> dataset = synth.RandomRBF(seed_model=42, seed_sample=42,
...                           n_classes=4, n_features=4, n_centroids=20)
>>>
>>> for x, y in dataset.take(5):
...     print(x, y)
{0: 0.9518, 1: 0.5263, 2: 0.2509, 3: 0.4177} 0
{0: 0.3383, 1: 0.8072, 2: 0.8051, 3: 0.4140} 3
{0: -0.2640, 1: 0.2275, 2: 0.6286, 3: -0.0532} 2
{0: 0.9050, 1: 0.6443, 2: 0.1270, 3: 0.4520} 2
{0: 0.1874, 1: 0.4348, 2: 0.9819, 3: -0.0459} 2
```

## Methods

???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    

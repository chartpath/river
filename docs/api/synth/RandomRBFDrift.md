# RandomRBFDrift

Random Radial Basis Function generator with concept drift.

This class is an extension from the `RandomRBF` generator. Concept drift can be introduced in instances of this class. 

The drift is created by adding a "speed" to certain centroids. As the samples are generated each of the moving centroids' centers is changed by an amount determined by its speed.

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

- **change_speed** (*float*) – defaults to `0.0`

    The concept drift speed.

- **n_drift_centroids** (*int*) – defaults to `50`

    The number of centroids that will drift.


## Attributes

- **desc**

    Return the description from the docstring.


## Examples

```python
>>> from river import synth
>>>
>>> dataset = synth.RandomRBFDrift(seed_model=42, seed_sample=42,
...                                n_classes=4, n_features=4, n_centroids=20,
...                                change_speed=0.87, n_drift_centroids=10)
>>>
>>> for x, y in dataset.take(5):
...     print(x, y)
{0: 1.1965, 1: 0.5729, 2: 0.8607, 3: 0.5888} 0
{0: 0.3383, 1: 0.8072, 2: 0.8051, 3: 0.4140} 3
{0: 0.5362, 1: -0.2867, 2: 0.0962, 3: 0.8974} 2
{0: 1.1875, 1: 1.0385, 2: 0.8323, 3: -0.0553} 2
{0: 0.3256, 1: 0.9206, 2: 0.8595, 3: 0.5907} 2
```

## Methods

???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    

# LEDDrift

LED stream generator with concept drift.

This class is an extension of the `LED` generator whose purpose is to add concept drift to the stream.

## Parameters

- **seed** (*int*) – defaults to `None`

    If int, `seed` is used to seed the random number generator; If RandomState instance, `seed` is the random number generator; If None, the random number generator is the `RandomState` instance used by `np.random`.

- **noise_percentage** (*float*) – defaults to `0.0`

    The probability that noise will happen in the generation. At each new sample generated, a random number is generated, and if it is equal or less than the noise_percentage, the led value  will be switched

- **irrelevant_features** (*bool*) – defaults to `False`

    Adds 17 non-relevant attributes to the stream.

- **n_drift_features** (*int*) – defaults to `0`

    The number of attributes that have drift.


## Attributes

- **desc**

    Return the description from the docstring.


## Examples

```python
>>> from river import synth

>>> dataset = synth.LEDDrift(seed = 112, noise_percentage = 0.28,
...                          irrelevant_features= True, n_drift_features=4)

>>> for x, y in dataset.take(5):
...     print(list(x.values()), y)
[1, 1, 1, 1, 1, 0, 1, 0, 0, 0, 1, 0, 1, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1] 8
[0, 1, 1, 1, 0, 1, 1, 1, 1, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 0, 1, 1, 1, 1] 5
[1, 1, 1, 1, 0, 1, 0, 1, 0, 0, 0, 1, 1, 1, 1, 0, 0, 1, 0, 0, 1, 1, 0, 1] 8
[0, 0, 1, 1, 1, 1, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 1, 0, 1, 0, 1, 1, 0] 3
[0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 1, 1, 0, 0, 1, 1, 1, 0, 0, 1, 1, 1, 1, 0] 5
```

## Methods

???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    
## Notes

An instance is generated based on the parameters passed. If `has_noise`
is set then the total number of attributes will be 24, otherwise there will
be 7 attributes.


# AnomalySine

Simulate a stream with anomalies in sine waves

The data generated corresponds to sine (`attribute 1`) and cosine (`attribute 2`) functions. Anomalies are induced by replacing values from `attribute 2` with values from a sine function different to the one used in `attribute 1`. The `contextual` flag can be used to introduce contextual anomalies which are values in the normal global range, but abnormal compared to the seasonal pattern. Contextual attributes are introduced by replacing values in `attribute 2` with values from `attribute 1`.

## Parameters

- **n_samples** (*int*) – defaults to `10000`

    Number of samples

- **n_anomalies** (*int*) – defaults to `2500`

    Number of anomalies. Can't be larger than `n_samples`.

- **contextual** (*bool*) – defaults to `False`

    If True, will add contextual anomalies

- **n_contextual** (*int*) – defaults to `2500`

    Number of contextual anomalies. Can't be larger than `n_samples`.

- **shift** (*int*) – defaults to `4`

    Shift in number of samples applied when retrieving contextual anomalies

- **noise** (*float*) – defaults to `0.5`

    Amount of noise

- **replace** (*bool*) – defaults to `True`

    If True, anomalies are randomly sampled with replacement

- **seed** (*int*) – defaults to `None`

    If int, `seed` is used to seed the random number generator; If RandomState instance, `seed` is the random number generator; If None, the random number generator is the `RandomState` instance used by `np.random`.


## Attributes

- **desc**

    Return the description from the docstring.


## Examples

```python
>>> from river import synth

>>> dataset = synth.AnomalySine(seed=12345,
...                             n_samples=100,
...                             n_anomalies=25,
...                             contextual=True,
...                             n_contextual=10)

>>> for x, y in dataset.take(5):
...     print(x, y)
{'sine': -0.1023, 'cosine': 0.2171} 0.0
{'sine': 0.4868, 'cosine': 0.6876} 0.0
{'sine': 0.2197, 'cosine': 0.8612} 0.0
{'sine': 0.4037, 'cosine': 0.2671} 0.0
{'sine': 1.8243, 'cosine': 1.8268} 1.0
```

## Methods

???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    

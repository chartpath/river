# Waveform

Waveform stream generator.

Generates samples with 21 numeric features and 3 classes, based on a random differentiation of some base waveforms. Supports noise addition, in this case the samples will have 40 features.

## Parameters

- **seed** (*int*) – defaults to `None`

    If int, `seed` is used to seed the random number generator; If RandomState instance, `seed` is the random number generator; If None, the random number generator is the `RandomState` instance used by `np.random`.

- **has_noise** (*bool*) – defaults to `False`

    Adds 19 unrelated features to the stream.


## Attributes

- **desc**

    Return the description from the docstring.


## Examples

```python
>>> from river import synth

>>> dataset = synth.Waveform(seed=42, has_noise=True)

>>> for x, y in dataset.take(5):
...     print(list(x.values()), y)
[0.5437, -0.6154, -1.1978, 2.1417, -0.0946, -0.7254, -0.4783, 0.1982, 0.3312, 1.9780,     3.0469, 3.5249, 5.4624, 6.1318, 2.7471, 4.7896, 2.9351, 2.2258, 0.1168, 2.2835, -0.0245,     0.3556, 0.4170, 0.8325, -0.2934, -0.0298, 0.0951, 0.6647, -0.1402, -0.0332, -0.7491,     -0.7784, 0.9488, 1.5809, -0.3682, 0.3756, -1.1932, -0.4091, -0.4467, 1.5242] 2
[0.2186, 1.4285, 0.0843, 0.0568, 2.9605, 2.6487, 2.8402, 3.2128, 2.8694, 4.0410,     4.3953, 3.7009, 2.7075, 2.1149, 0.6994, -0.1702, -1.5082, 1.0996, -0.1777, -0.4104,     1.1797, -0.8982, 0.8348, 0.2966, -1.0378, -0.0758, 0.9730, 0.7956, 1.4954, 0.3382,     3.3723, -0.9204, -0.3986, -0.0609, -1.4188, 1.0425, 0.9035, 0.0190, -0.5344, -1.4951] 1
[0.1358, 0.6081, 0.7050, 0.3609, -1.4670, 1.6896, 1.4886, 1.4355, 2.7730, 2.7890,     4.8437, 5.3447, 3.6724, 2.5445, 2.5541, 2.2732, -0.5371, -0.4099, 0.5331, -1.0464,     1.9451, -0.1533, -0.9070, -0.8174, -0.4831, -0.5698, -2.0916, 1.2637, -0.0155, -0.0274,     0.8179, -1.0546, -0.7583, 0.4574, -0.0644, 0.3449, -0.0801, -0.2414, 1.4335, 1.0658] 2
[1.1428, 1.2414, 1.7699, 0.5590, 3.3606, 1.0454, 3.5236, 4.6377, 0.9673, 1.4126,     2.0997, 1.5176, 0.4915, 2.6213, 2.0010, 3.0263, 1.1228, 3.0816, 0.2378, 0.1885,     0.8135, -1.2309, 0.2275, 1.3071, -1.6075, 0.1846, 0.2599, 0.7818, -1.2370, -1.3205,     0.5219, 0.2970, 0.2505, 0.3464, -0.6800, 0.2323, 0.2931, -0.7144, 1.8658, 0.4738] 0
[-0.9747, 1.0114, 1.6071, -0.1479, 1.8605, 1.5341, 2.1677, 3.0181, 0.6517, 0.6948,     1.1105, 1.7357, 3.0258, 4.2198, 4.9311, 4.7058, 3.1159, 3.7807, 1.2868, 3.4959,     0.6257, -0.8572, -1.0709, 0.4825, -0.2235, 0.7140, 0.4732, -0.0728, -0.8468, -1.5148,     -0.4465, 0.8564, 0.2141, -1.2457, 0.1732, 0.3853, -0.8839, 0.1537, 0.0582, -1.1430] 0
```

## Methods

???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    
## Notes

An instance is generated based on the parameters passed.
The generator will randomly choose one of the hard coded waveforms, as
well as random multipliers. For each feature, the actual value generated
will be a a combination of the hard coded functions, with the multipliers
and a random value.

If noise is added then the features 21 to 40 will be replaced with a
random normal value.


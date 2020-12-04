# SDFT

Sliding Discrete Fourier Transform (SDFT).

Initially, the coefficients are all equal to 0, up until enough values have been seen. A call to `numpy.fft.fft` is triggered once `window_size` values have been seen. Subsequent values will update the coefficients online. This is much faster than recomputing an FFT from scratch for every new value.

## Parameters

- **window_size**

    The size of the window.


## Attributes

- **window** (*utils.Window*)

    The window of values.


## Examples

```python
>>> from river import utils

>>> X = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

>>> window_size = 5
>>> sdft = utils.SDFT(window_size)

>>> for i, x in enumerate(X):
...     sdft = sdft.update(x)
...
...     if i + 1 >= window_size:
...         assert np.allclose(sdft, np.fft.fft(X[i+1 - window_size:i+1]))
```

## Methods

???- note "append"

???- note "extend"

???- note "popleft"

???- note "update"

## References

[^1]: `Jacobsen, E. and Lyons, R., 2003. The sliding DFT. IEEE Signal Processing Magazine, 20(2), pp.74-80. <https://www.comm.utoronto.ca/~dimitris/ece431/slidingdft.pdf>`_
[^2]: `Understanding and Implementing the Sliding DFT <https://www.dsprelated.com/showarticle/776.php>`_


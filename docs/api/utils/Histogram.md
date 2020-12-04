# Histogram

Streaming histogram.



## Parameters

- **max_bins** – defaults to `256`

    Maximal number of bins.


## Attributes

- **n**

    Total number of seen values.


## Examples

```python
>>> from river import utils
>>> import matplotlib.pyplot as plt
>>> import numpy as np

>>> np.random.seed(42)

>>> values = np.hstack((
...     np.random.normal(-3, 1, 1000),
...     np.random.normal(3, 1, 1000),
... ))

>>> hist = utils.Histogram(max_bins=60)

>>> for x in values:
...     hist = hist.update(x)

>>> ax = plt.bar(
...     x=[(b.left + b.right) / 2 for b in hist],
...     height=[b.count for b in hist],
...     width=[(b.right - b.left) / 2 for b in hist]
... )

```

.. image:: ../../docs/img/histogram_docstring.svg
    :align: center

## Methods

???- note "append"

    S.append(value) -- append value to the end of the sequence

    **Parameters**

    - **item**    
    
???- note "cdf"

    Cumulative distribution function.

    Example:      >>> from river import utils      >>> hist = utils.Histogram()     >>> for x in range(4):     ...     hist = hist.update(x)      >>> print(hist)     [0.00000, 0.00000]: 1     [1.00000, 1.00000]: 1     [2.00000, 2.00000]: 1     [3.00000, 3.00000]: 1      >>> hist.cdf(-1)     0.0      >>> hist.cdf(0)     0.25      >>> hist.cdf(.5)     0.25      >>> hist.cdf(1)     0.5      >>> hist.cdf(2.5)     0.75      >>> hist.cdf(3.5)     1.0

    **Parameters**

    - **x**    
    
???- note "clear"

    S.clear() -> None -- remove all items from S

    
???- note "copy"

???- note "count"

    S.count(value) -> integer -- return number of occurrences of value

    **Parameters**

    - **item**    
    
???- note "extend"

    S.extend(iterable) -- extend sequence by appending elements from the iterable

    **Parameters**

    - **other**    
    
???- note "index"

    S.index(value, [start, [stop]]) -> integer -- return first index of value. Raises ValueError if the value is not present.

    Supporting start and stop arguments is optional, but recommended.

    **Parameters**

    - **item**    
    - **args**    
    
???- note "insert"

    S.insert(index, value) -- insert value before index

    **Parameters**

    - **i**    
    - **item**    
    
???- note "iter_cdf"

    Yields CDF values for a sorted iterable of values.

    This is faster than calling `cdf` with many values.  Example:      >>> from river import utils      >>> hist = utils.Histogram()     >>> for x in range(4):     ...     hist = hist.update(x)      >>> print(hist)     [0.00000, 0.00000]: 1     [1.00000, 1.00000]: 1     [2.00000, 2.00000]: 1     [3.00000, 3.00000]: 1      >>> X = [-1, 0, .5, 1, 2.5, 3.5]     >>> for x, cdf in zip(X, hist.iter_cdf(X)):     ...     print(x, cdf)     -1 0.0     0 0.25     0.5 0.25     1 0.5     2.5 0.75     3.5 1.0

    **Parameters**

    - **X**    
    - **verbose**     – defaults to `False`    
    
???- note "pop"

    S.pop([index]) -> item -- remove and return item at index (default last). Raise IndexError if list is empty or index is out of range.

    **Parameters**

    - **i**     – defaults to `-1`    
    
???- note "remove"

    S.remove(value) -- remove first occurrence of value. Raise ValueError if the value is not present.

    **Parameters**

    - **item**    
    
???- note "reverse"

    S.reverse() -- reverse *IN PLACE*

    
???- note "sort"

???- note "update"

## References

[^1]: [Ben-Haim, Y. and Tom-Tov, E., 2010. A streaming parallel decision tree algorithm. Journal of Machine Learning Research, 11(Feb), pp.849-872.](http://jmlr.org/papers/volume11/ben-haim10a/ben-haim10a.pdf)
[^2]: [Go implementation](https://github.com/VividCortex/gohistogram)


# NUnique

Approximate number of unique values counter.

This is basically an implementation of the HyperLogLog algorithm. Adapted from [`hypy`](https://github.com/clarkduvall/hypy). The code is a bit too terse but it will do for now.

## Parameters

- **error_rate** – defaults to `0.01`

    Desired error rate. Memory usage is inversely proportional to this value.

- **seed** (*int*) – defaults to `None`

    Set the seed to produce identical results.


## Attributes

- **n_bits** (*int*)

- **n_buckets** (*int*)

- **buckets** (*list*)


## Examples

```python
>>> import string
>>> from river import stats

>>> alphabet = string.ascii_lowercase
>>> n_unique = stats.NUnique(error_rate=0.2, seed=42)

>>> n_unique.update('a').get()
1

>>> n_unique.update('b').get()
2

>>> for letter in alphabet:
...     n_unique = n_unique.update(letter)
>>> n_unique.get()
31

```

Lowering the `error_rate` parameter will increase the precision.

```python
>>> n_unique = stats.NUnique(error_rate=0.01, seed=42)
>>> for letter in alphabet:
...     n_unique = n_unique.update(letter)
>>> n_unique.get()
26
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "get"

???- note "revert"

    Revert and return the called instance.

    **Parameters**

    - **x**    
    
???- note "update"

    Update and return the called instance.

    **Parameters**

    - **x**    
    
## References

[^1]: [My favorite algorithm (and data structure): HyperLogLog](https://odino.org/my-favorite-data-structure-hyperloglog/)
[^2]: [Flajolet, P., Fusy, É., Gandouet, O. and Meunier, F., 2007, June. Hyperloglog: the analysis of a near-optimal cardinality estimation algorithm.](http://algo.inria.fr/flajolet/Publications/FlFuGaMe07.pdf)


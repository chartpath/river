# Link

A link joins two univariate statistics as a sequence.

This can be used to pipe the output of one statistic to the input of another. This can be used, for instance, to calculate the mean of the variance of a variable. It can also be used to compute shifted statistics by piping statistics with an instance of `stats.Shift`. 

Note that a link is not meant to be instantiated via this class definition. Instead, users can link statistics together via the `|` operator.

## Parameters

- **left** (*river.stats.base.Univariate*)

- **right** (*river.stats.base.Univariate*)

    The output from `left`'s `get` method is passed to `right`'s `update` method if `left`'s `get` method doesn't produce `None.`


## Attributes

- **name**


## Examples

```python
>>> from river import stats
>>> stat = stats.Shift(1) | stats.Mean()

```

No values have been seen, therefore `get` defaults to the initial value of `stats.Mean`,
which is 0.

```python
>>> stat.get()
0.

```

Let us now call `update`.

```python
>>> stat = stat.update(1)

```

The output from `get` will still be 0. The reason is that `stats.Shift` has not enough
values, and therefore outputs it's default value, which is `None`. The `stats.Mean`
instance is therefore not updated.

```python
>>> stat.get()
0.0

```

On the next call to `update`, the `stats.Shift` instance has seen enough values, and
therefore the mean can be updated. The mean is therefore equal to 1, because that's the
only value from the past.

```python
>>> stat = stat.update(3)
>>> stat.get()
1.0

```

On the subsequent call to update, the mean will be updated with the value 3.

```python
>>> stat = stat.update(4)
>>> stat.get()
2.0

```

Note that composing statistics returns a new statistic with it's own name.

```python
>>> stat.name
'mean_of_shift_1'
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
    

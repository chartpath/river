# RollingQuantile

Running quantile over a window.



## Parameters

- **q**

    Determines which quantile to compute, must be comprised between 0 and 1.

- **window_size**

    Size of the window.


## Attributes

- **name**

- **size**

- **window_size**


## Examples

```python
>>> from river import stats

>>> rolling_quantile = stats.RollingQuantile(
...     q=.5,
...     window_size=100,
... )

>>> for i in range(0, 1001):
...     rolling_quantile = rolling_quantile.update(i)
...     if i % 100 == 0:
...         print(rolling_quantile.get())
0
50
150
250
350
450
550
650
750
850
950
```

## Methods

???- note "append"

    S.append(value) -- append value to the end of the sequence

    **Parameters**

    - **x**    
    
???- note "clear"

    S.clear() -> None -- remove all items from S

    
???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "copy"

???- note "count"

    S.count(value) -> integer -- return number of occurrences of value

    **Parameters**

    - **item**    
    
???- note "extend"

    S.extend(iterable) -- extend sequence by appending elements from the iterable

    **Parameters**

    - **other**    
    
???- note "get"

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

    
???- note "revert"

    Revert and return the called instance.

    **Parameters**

    - **x**    
    
???- note "sort"

???- note "update"

    Update and return the called instance.

    **Parameters**

    - **x**    
    
## References

[^1]: [Left sorted](https://stackoverflow.com/questions/8024571/insert-an-item-into-sorted-list-in-python)


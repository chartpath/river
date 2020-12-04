# SortedWindow

Sorted running window data structure.



## Parameters

- **size** (*int*)

    Size of the window to compute the rolling quantile.


## Attributes

- **size**


## Examples

```python
>>> from river import utils

>>> window = utils.SortedWindow(size=3)

>>> for i in reversed(range(9)):
...     print(window.append(i))
[8]
[7, 8]
[6, 7, 8]
[5, 6, 7]
[4, 5, 6]
[3, 4, 5]
[2, 3, 4]
[1, 2, 3]
[0, 1, 2]
```

## Methods

???- note "append"

    S.append(value) -- append value to the end of the sequence

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

## References

[^1]: [Left sorted inserts in Python](https://stackoverflow.com/questions/8024571/insert-an-item-into-sorted-list-in-python)


# Cache

Utility for caching iterables.

This can be used to save a stream of data to the disk in order to iterate over it faster the following time. This can save time depending on the nature of stream. The more processing happens in a stream, the more time will be saved. Even in the case where no processing is done apart from reading the data, the cache will save some time because it is using the pickle binary protocol. It can thus improve the speed in common cases such as reading from a CSV file.

## Parameters

- **directory** – defaults to `None`

    The path where to store the pickled data streams. If not provided, then it will be automatically inferred whenever possible, if not an exception will be raised.


## Attributes

- **keys** (*set*)

    The set of keys that are being cached.


## Examples

```python
>>> import time
>>> from river import datasets
>>> from river import stream

>>> dataset = datasets.Phishing()
>>> cache = stream.Cache()

```

The cache can be used by wrapping it around an iterable. Because this is the first time
are iterating over the data, nothing is cached.

```python
>>> tic = time.time()
>>> for x, y in cache(dataset, key='phishing'):
...     pass
>>> toc = time.time()
>>> print(toc - tic)  # doctest: +SKIP
0.012813

```

If we do the same thing again, we can see the loop is now faster.

```python
>>> tic = time.time()
>>> for x, y in cache(dataset, key='phishing'):
...     pass
>>> toc = time.time()
>>> print(toc - tic)  # doctest: +SKIP
0.001927

```

We can see an overview of the cache. The first line indicates the location of the
cache.

```python
>>> cache  # doctest: +SKIP
/tmp
phishing - 125.2KiB

```

Finally, we can clear the stream from the cache.

```python
>>> cache.clear('phishing')
>>> cache
/tmp

```

There is also a `clear_all` method to remove all the items in the cache.

```python
>>> cache.clear_all()
```

## Methods

???- note "__call__"

    Call self as a function.

    **Parameters**

    - **stream**    
    - **key**     – defaults to `None`    
    
???- note "clear"

    Delete the cached stream associated with the given key.

    **Parameters**

    - **key**     (*str*)    
    
???- note "clear_all"

    Delete all the cached streams.

    

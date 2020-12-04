# iter_csv

Iterates over rows from a CSV file.

Reading CSV files can be quite slow. If, for whatever reason, you're going to loop through the same file multiple times, then we recommend that you to use the [`stream.Cache`](../../stream/Cache) utility.

## Parameters

- **filepath_or_buffer**

    Either a string indicating the location of a CSV file, or a buffer object that has a `read` method.

- **target** (*Union[str, List[str]]*) – defaults to `None`

    A single target column is assumed if a string is passed. A multiple output scenario is assumed if a list of strings is passed. A `None` value will be assigned to each `y` if this parameter is omitted.

- **converters** (*dict*) – defaults to `None`

    A `dict` mapping feature names to callables used to parse their associated values.

- **parse_dates** (*dict*) – defaults to `None`

    A `dict` mapping feature names to a format passed to the `datetime.datetime.strptime` method.

- **drop** (*List[str]*) – defaults to `None`

    Fields to ignore.

- **fraction** – defaults to `1.0`

    Sampling fraction.

- **compression** – defaults to `infer`

    For on-the-fly decompression of on-disk data. If this is set to 'infer' and `filepath_or_buffer` is a path, then the decompression method is inferred for the following extensions: '.gz', '.zip'.

- **seed** (*int*) – defaults to `None`

    If specified, the sampling will be deterministic.

- **field_size_limit** (*int*) – defaults to `None`

    If not `None`, this will be passed to the `csv.field_size_limit` function.

- **kwargs**

    All other keyword arguments are passed to the underlying `csv.DictReader`.



## Examples

Although this function is designed to handle different kinds of inputs, the most common
use case is to read a file on the disk. We'll first create a little CSV file to illustrate.

```python
>>> tv_shows = '''name,year,rating
... Planet Earth II,2016,9.5
... Planet Earth,2006,9.4
... Band of Brothers,2001,9.4
... Breaking Bad,2008,9.4
... Chernobyl,2019,9.4
... '''
>>> with open('tv_shows.csv', mode='w') as f:
...     _ = f.write(tv_shows)

```

We can now go through the rows one by one. We can use the `converters` parameter to cast
the `rating` field value as a `float`. We can also convert the `year` to a `datetime` via
the `parse_dates` parameter.

```python
>>> from river import stream

>>> params = {
...     'converters': {'rating': float},
...     'parse_dates': {'year': '%Y'}
... }
>>> for x, y in stream.iter_csv('tv_shows.csv', **params):
...     print(x, y)
{'name': 'Planet Earth II', 'year': datetime.datetime(2016, 1, 1, 0, 0), 'rating': 9.5} None
{'name': 'Planet Earth', 'year': datetime.datetime(2006, 1, 1, 0, 0), 'rating': 9.4} None
{'name': 'Band of Brothers', 'year': datetime.datetime(2001, 1, 1, 0, 0), 'rating': 9.4} None
{'name': 'Breaking Bad', 'year': datetime.datetime(2008, 1, 1, 0, 0), 'rating': 9.4} None
{'name': 'Chernobyl', 'year': datetime.datetime(2019, 1, 1, 0, 0), 'rating': 9.4} None

```

The value of `y` is always `None` because we haven't provided a value for the `target`
parameter. Here is an example where a `target` is provided:

```python
>>> dataset = stream.iter_csv('tv_shows.csv', target='rating', **params)
>>> for x, y in dataset:
...     print(x, y)
{'name': 'Planet Earth II', 'year': datetime.datetime(2016, 1, 1, 0, 0)} 9.5
{'name': 'Planet Earth', 'year': datetime.datetime(2006, 1, 1, 0, 0)} 9.4
{'name': 'Band of Brothers', 'year': datetime.datetime(2001, 1, 1, 0, 0)} 9.4
{'name': 'Breaking Bad', 'year': datetime.datetime(2008, 1, 1, 0, 0)} 9.4
{'name': 'Chernobyl', 'year': datetime.datetime(2019, 1, 1, 0, 0)} 9.4

```

Finally, let's delete the example file.

```python
>>> import os; os.remove('tv_shows.csv')
```


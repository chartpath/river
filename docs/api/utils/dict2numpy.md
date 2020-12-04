# dict2numpy

Convert a dictionary containing data to a numpy array.

There is not restriction to the type of keys in `data`, but values must be strictly numeric. To make sure random permutations of the features do not impact on the learning algorithms, keys are first converted to strings and then sorted prior to the conversion.

## Parameters

- **data**

    A dictionary whose keys represent input attributes and the values represent their observed contents.



## Examples

```python
>>> from river.utils import dict2numpy
>>> dict2numpy({'a': 1, 'b': 2, 3: 3})
array([3, 1, 2])
```


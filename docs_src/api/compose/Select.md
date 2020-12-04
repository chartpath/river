# Select

Selects features according to a whitelist.

This can be used in a pipeline when you want to remove certain features. The `transform_one` method is pure, and therefore returns a fresh new dictionary instead of removing the specified keys from the input.

## Parameters

- **whitelist** (*Tuple[Hashable]*)

    Key(s) to keep.



## Examples

```python
>>> from river import compose

>>> x = {'a': 42, 'b': 12, 'c': 13}
>>> compose.Select('c').transform_one(x)
{'c': 13}

```

You can chain a selector with any estimator in order to apply said estimator to the
desired features.

```python
>>> from river import feature_extraction as fx

>>> x = {'sales': 10, 'shop': 'Ikea', 'country': 'Sweden'}

>>> pipeline = (
...     compose.Select('sales') |
...     fx.PolynomialExtender()
... )
>>> pipeline.transform_one(x)
{'sales': 10, 'sales*sales': 100}
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update with a set of features `x`.

    A lot of transformers don't actually have to do anything during the `learn_one` step because they are stateless. For this reason the default behavior of this function is to do nothing. Transformers that however do something during the `learn_one` can override this method.

    **Parameters**

    - **x**     (*dict*)    
    - **kwargs**    
    
    **Returns**

    *Transformer*:     self
    
???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *dict*:     The transformed values.
    

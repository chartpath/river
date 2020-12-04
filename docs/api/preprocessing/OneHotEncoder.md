# OneHotEncoder

One-hot encoding.

This transformer will encode every feature it is provided it with. You can apply it to a subset of features by composing it with `compose.Select` or `compose.SelectType`.

## Parameters

- **sparse** – defaults to `False`

    Whether or not 0s should be made explicit or not.



## Examples

Let us first create an example dataset.

```python
>>> from pprint import pprint
>>> import random
>>> import string

>>> random.seed(42)
>>> alphabet = list(string.ascii_lowercase)
>>> X = [
...     {
...         'c1': random.choice(alphabet),
...         'c2': random.choice(alphabet),
...     }
...     for _ in range(4)
... ]
>>> pprint(X)
[{'c1': 'u', 'c2': 'd'},
    {'c1': 'a', 'c2': 'x'},
    {'c1': 'i', 'c2': 'h'},
    {'c1': 'h', 'c2': 'e'}]

```

We can now apply one-hot encoding. All the provided are one-hot encoded, there is therefore
no need to specify which features to encode.

```python
>>> import river.preprocessing

>>> oh = river.preprocessing.OneHotEncoder(sparse=True)
>>> for x in X:
...     oh = oh.learn_one(x)
...     pprint(oh.transform_one(x))
{'c1_u': 1, 'c2_d': 1}
{'c1_a': 1, 'c2_x': 1}
{'c1_i': 1, 'c2_h': 1}
{'c1_h': 1, 'c2_e': 1}

```

The `sparse` parameter can be set to `False` in order to include the values that are not
present in the output.

```python
>>> oh = river.preprocessing.OneHotEncoder(sparse=False)
>>> for x in X[:2]:
...     oh = oh.learn_one(x)
...     pprint(oh.transform_one(x))
{'c1_u': 1, 'c2_d': 1}
{'c1_a': 1, 'c1_u': 0, 'c2_d': 0, 'c2_x': 1}

```

A subset of the features can be one-hot encoded by using an instance of `compose.Select`.

```python
>>> from river import compose

>>> pp = compose.Select('c1') | river.preprocessing.OneHotEncoder()

>>> for x in X:
...     pp = pp.learn_one(x)
...     pprint(pp.transform_one(x))
{'c1_u': 1}
{'c1_a': 1, 'c1_u': 0}
{'c1_a': 0, 'c1_i': 1, 'c1_u': 0}
{'c1_a': 0, 'c1_h': 1, 'c1_i': 0, 'c1_u': 0}

```

You can preserve the `c2` feature by using a union:

```python
>>> pp = compose.Select('c1') | river.preprocessing.OneHotEncoder()
>>> pp += compose.Select('c2')

>>> for x in X:
...     pp = pp.learn_one(x)
...     pprint(pp.transform_one(x))
{'c1_u': 1, 'c2': 'd'}
{'c1_a': 1, 'c1_u': 0, 'c2': 'x'}
{'c1_a': 0, 'c1_i': 1, 'c1_u': 0, 'c2': 'h'}
{'c1_a': 0, 'c1_h': 1, 'c1_i': 0, 'c1_u': 0, 'c2': 'e'}
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
    
    **Returns**

    *Transformer*:     self
    
???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     – defaults to `None`    
    
    **Returns**

    *dict*:     The transformed values.
    

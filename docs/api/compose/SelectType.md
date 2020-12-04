# SelectType

Selects features based on their type.

This is practical when you want to apply different preprocessing steps to different kinds of features. For instance, a common usecase is to apply a `preprocessing.StandardScaler` to numeric features and a `preprocessing.OneHotEncoder` to categorical features.

## Parameters

- **types** (*Tuple[type]*)

    Python types which you want to select. Under the hood, the `isinstance` method will be used to check if a value is of a given type.



## Examples

```python
>>> import numbers
>>> from river import compose
>>> from river import linear_model
>>> from river import preprocessing

>>> num = compose.SelectType(numbers.Number) | preprocessing.StandardScaler()
>>> cat = compose.SelectType(str) | preprocessing.OneHotEncoder()
>>> model = (num + cat) | linear_model.LogisticRegression()
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
    

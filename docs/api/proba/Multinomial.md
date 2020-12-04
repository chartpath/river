# Multinomial

Multinomial distribution for categorical data.



## Parameters

- **events** (*Union[dict, list]*) – defaults to `None`

    An optional list of events that already occurred.


## Attributes

- **mode**

- **n_samples**

    The number of observed samples.


## Examples

```python
>>> from river import proba

>>> p = proba.Multinomial(['green'] * 3)
>>> p = p.update('red')

>>> p.pmf('red')
0.25

>>> p.update('red').update('red').pmf('green')
0.5
```

## Methods

???- note "pmf"

    Probability mass function.

    **Parameters**

    - **x**    
    
???- note "update"

    Updates the parameters of the distribution given a new observation.

    **Parameters**

    - **x**    
    

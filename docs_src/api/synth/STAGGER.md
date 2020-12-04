# STAGGER

STAGGER concepts stream generator.

This generator is an implementation of the dara stream with abrupt concept drift, as described in [^1]. 

The STAGGER concepts are boolean functions `f` with three features describing objects: size (small, medium and large), shape (circle, square and triangle) and colour (red, blue and green). 

`f` options: 

0. `True` if the size is small and the color is red. 

1. `True` if the color is green or the shape is a circle. 

2. `True` if the size is medium or large 

Concept drift can be introduced by changing the classification function. This can be done manually or using `ConceptDriftStream`. 

One important feature is the possibility to balance classes, which means the class distribution will tend to a uniform one.

## Parameters

- **classification_function** (*int*) – defaults to `0`

    Classification functions to use. From 0 to 2.

- **seed** (*int*) – defaults to `None`

    If int, `seed` is used to seed the random number generator; If RandomState instance, `seed` is the random number generator; If None, the random number generator is the `RandomState` instance used by `np.random`.

- **balance_classes** (*bool*) – defaults to `False`

    Whether to balance classes or not. If balanced, the class distribution will converge to an uniform distribution.


## Attributes

- **desc**

    Return the description from the docstring.


## Examples

```python
>>> from river import synth

>>> dataset = synth.STAGGER(classification_function = 2, seed = 112,
...                      balance_classes = False)

>>> for x, y in dataset.take(5):
...     print(x, y)
{'size': 0, 'color': 0, 'shape': 2} 0
{'size': 1, 'color': 0, 'shape': 1} 1
{'size': 0, 'color': 0, 'shape': 0} 0
{'size': 1, 'color': 2, 'shape': 0} 1
{'size': 1, 'color': 0, 'shape': 2} 1
```

## Methods

???- note "generate_drift"

    Generate drift by switching the classification function at random.

    
???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    
## Notes

The sample generation works as follows: The 3 attributes are
generated with the random number generator. The classification function
defines whether to classify the instance as class 0 or class 1. Finally,
data is balanced, if this option is set by the user.

## References

[^1]: Schlimmer, J. C., & Granger, R. H. (1986). Incremental learning
      from noisy data. Machine learning, 1(3), 317-354.


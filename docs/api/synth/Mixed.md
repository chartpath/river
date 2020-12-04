# Mixed

Mixed data stream generator.

This generator is an implementation of a data stream with abrupt concept drift and boolean noise-free examples as described in [^1]. 

It has four relevant attributes, two boolean attributes $v, w$ and two numeric attributes $x, y$ uniformly distributed from 0 to 1. The examples are labeled depending on the classification function chosen from below. 

* `function 0`:   if $v$ and $w$ are true or $v$ and $z$ are true or $w$ and $z$ are true   then 0 else 1, where $z$ is $y < 0.5 + 0.3 sin(3 \pi  x)$ 

* `function 1`:    The opposite of `function 0`. 

Concept drift can be introduced by changing the classification function. This can be done manually or using `ConceptDriftStream`.

## Parameters

- **classification_function** (*int*) – defaults to `0`

    Which of the two classification functions to use for the generation. Valid options are 0 or 1.

- **seed** (*int*) – defaults to `None`

    If int, `seed` is used to seed the random number generator; If RandomState instance, `seed` is the random number generator; If None, the random number generator is the `RandomState` instance used by `np.random`.

- **balance_classes** (*bool*) – defaults to `False`

    Whether to balance classes or not. If balanced, the class distribution will converge to a uniform distribution.


## Attributes

- **desc**

    Return the description from the docstring.


## Examples

```python
>>> from river import synth
>>>
>>> dataset = synth.Mixed(seed = 42, classification_function=1, balance_classes = True)
>>>
>>> for x, y in dataset.take(5):
...     print(x, y)
{0: False, 1: True, 2: 0.7319, 3: 0.5986} 1
{0: False, 1: False, 2: 0.0580, 3: 0.8661} 0
{0: True, 1: True, 2: 0.0205, 3: 0.9699} 1
{0: False, 1: True, 2: 0.4319, 3: 0.2912} 0
{0: True, 1: False, 2: 0.2921, 3: 0.3663} 1
```

## Methods

???- note "generate_drift"

    Generate drift by switching the classification function.

    
???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    
## Notes

The sample generation works as follows: The two numeric attributes are
generated with the random  generator initialized with the seed passed by
the user (optional). The boolean attributes are either 0 or 1
based on the comparison of the random number generator and 0.5 ,
the classification function decides whether to classify the instance
as class 0 or class 1. The next step is to verify if the classes should
be balanced, and if so, balance the classes.

The generated sample will have 4 relevant features and 1 label (it is a
binary-classification task).

## References

[^1]: Gama, Joao, et al. "Learning with drift detection." Advances in
      artificial intelligence–SBIA 2004. Springer Berlin Heidelberg,
      2004. 286-295"


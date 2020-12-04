# Agrawal

Agrawal stream generator.

The generator was introduced by Agrawal et al. [^1], and was a common source of data for early work on scaling up decision tree learners. The generator produces a stream containing nine features, six numeric and three categorical. There are 10 functions defined for generating binary class labels from the features. Presumably these determine whether the loan should be approved. Classification functions are listed in the original paper [^1]. 

**Feature** | **Description** | **Values** 

* `salary` | salary | uniformly distributed from 20k to 150k 

* `commission` | commission | 0 if `salary` < 75k else uniformly distributed from 10k to 75k 

* `age` | age | uniformly distributed from 20 to 80 

* `elevel` | education level | uniformly chosen from 0 to 4 

* `car` | car maker | uniformly chosen from 1 to 20 

* `zipcode` | zip code of the town | uniformly chosen from 0 to 8 

* `hvalue` | house value | uniformly distributed from 50k x zipcode to 100k x zipcode 

* `hyears` | years house owned | uniformly distributed from 1 to 30 

* `loan` | total loan amount | uniformly distributed from 0 to 500k

## Parameters

- **classification_function** (*int*) – defaults to `0`

    The classification function to use for the generation. Valid values are from 0 to 9.

- **seed** (*int*) – defaults to `None`

    If int, `seed` is used to seed the random number generator; If RandomState instance, `seed` is the random number generator; If None, the random number generator is the `RandomState` instance used by `np.random`.

- **balance_classes** (*bool*) – defaults to `False`

    If True, the class distribution will converge to a uniform distribution.

- **perturbation** (*float*) – defaults to `0.0`

    The probability that noise will happen in the generation. Each new sample will be perturbed by the magnitude of `perturbation`. Valid values are in the range [0.0 to 1.0].


## Attributes

- **desc**

    Return the description from the docstring.


## Examples

```python
>>> from river import synth

>>> dataset = synth.Agrawal(classification_function=0,
...                         seed=42)

>>> for x, y in dataset.take(5):
...     print(list(x.values()), y)
[68690.2154, 81303.5729, 62, 4, 6, 2, 419982.4410, 11, 433088.0728] 1
[98144.9515, 0, 43, 2, 1, 7, 266488.5281, 6, 389.3829] 0
[148987.502, 0, 52, 3, 11, 8, 79122.9140, 27, 199930.4858] 0
[26066.5362, 83031.6639, 34, 2, 11, 6, 444969.2657, 25, 23225.2063] 1
[98980.8307, 0, 40, 0, 6, 1, 1159108.4298, 28, 281644.1089] 0
```

## Methods

???- note "generate_drift"

    Generate drift by switching the classification function randomly.

    
???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    
## Notes

The sample generation works as follows: The 9 features are generated
with the random generator, initialized with the seed passed by the
user. Then, the classification function decides, as a function of all
the attributes, whether to classify the instance as class 0 or class
1. The next step is to verify if the classes should be balanced, and
if so, balance the classes. Finally, add noise if `perturbation` > 0.0.

## References

[^1]: Rakesh Agrawal, Tomasz Imielinksi, and Arun Swami. "Database Mining:
      A Performance Perspective", IEEE Transactions on Knowledge and
      Data Engineering, 5(6), December 1993.


# Entropy

Running entropy.



## Parameters

- **alpha** – defaults to `1`

    Fading factor.

- **eps** – defaults to `1e-08`

    Small value that will be added to the denominator to avoid division by zero.


## Attributes

- **entropy** (*float*)

    The running entropy.

- **n** (*int*)

    The current number of observations.

- **counter** (*collections.Counter*)

    Count the number of times the values have occurred


## Examples

```python
>>> import math
>>> import random
>>> import numpy as np
>>> from scipy.stats import entropy
>>> from river import stats

>>> def entropy_list(labels, base=None):
...   value,counts = np.unique(labels, return_counts=True)
...   return entropy(counts, base=base)

>>> SEED = 42 * 1337
>>> random.seed(SEED)

>>> entro = stats.Entropy(alpha=1)

>>> list_animal = []
>>> for animal, num_val in zip(['cat', 'dog', 'bird'],[301, 401, 601]):
...     list_animal += [animal for i in range(num_val)]
>>> random.shuffle(list_animal)

>>> for animal in list_animal:
...     _ = entro.update(animal)

>>> print(f'{entro.get():.6f}')
1.058093
>>> print(f'{entropy_list(list_animal):.6f}')
1.058093
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "get"

???- note "revert"

    Revert and return the called instance.

    **Parameters**

    - **x**    
    
???- note "update"

    Update and return the called instance.

    **Parameters**

    - **x**    
    
## References

[^1]: [Sovdat, B., 2014. Updating Formulas and Algorithms for Computing Entropy and Gini Index from Time-Changing Data Streams. arXiv preprint arXiv:1403.6348.](https://arxiv.org/pdf/1403.6348.pdf)


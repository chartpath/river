# RandomTree

Random Tree generator.

This generator is based on [^1]. The generator creates a random tree by splitting features at random and setting labels at its leaves. 

The tree structure is composed of node objects, which can be either inner nodes or leaf nodes. The choice comes as a function of the parameters passed to its initializer. 

Since the concepts are generated and classified according to a tree structure, in theory, it should favor decision tree learners.

## Parameters

- **seed_tree** (*int*) – defaults to `None`

    Seed for random generation of tree.

- **seed_sample** (*int*) – defaults to `None`

    Seed for random generation of instances.

- **n_classes** (*int*) – defaults to `2`

    The number of classes to generate.

- **n_num_features** (*int*) – defaults to `5`

    The number of numerical features to generate.

- **n_cat_features** (*int*) – defaults to `5`

    The number of categorical features to generate.

- **n_categories_per_feature** (*int*) – defaults to `5`

    The number of values to generate per categorical feature.

- **max_tree_depth** (*int*) – defaults to `5`

    The maximum depth of the tree concept.

- **first_leaf_level** (*int*) – defaults to `3`

    The first level of the tree above `max_tree_depth` that can have leaves.

- **fraction_leaves_per_level** (*float*) – defaults to `0.15`

    The fraction of leaves per level from `first_leaf_level` onwards.


## Attributes

- **desc**

    Return the description from the docstring.


## Examples

```python
>>> from river import synth

>>> dataset = synth.RandomTree(seed_tree=42, seed_sample=42, n_classes=2,
...                            n_num_features=2, n_cat_features=2,
...                            n_categories_per_feature=2, max_tree_depth=6,
...                            first_leaf_level=3, fraction_leaves_per_level=0.15)

>>> for x, y in dataset.take(5):
...     print(x, y)
{'x_num_0': 0.3745, 'x_num_1': 0.9507, 'x_cat_0': 0, 'x_cat_1': 1} 1
{'x_num_0': 0.5986, 'x_num_1': 0.1560, 'x_cat_0': 0, 'x_cat_1': 0} 1
{'x_num_0': 0.0580, 'x_num_1': 0.8661, 'x_cat_0': 1, 'x_cat_1': 1} 0
{'x_num_0': 0.7080, 'x_num_1': 0.0205, 'x_cat_0': 1, 'x_cat_1': 1} 0
{'x_num_0': 0.8324, 'x_num_1': 0.2123, 'x_cat_0': 1, 'x_cat_1': 1} 0
```

## Methods

???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    
## References

[^1]: Domingos, Pedro, and Geoff Hulten. "Mining high-speed data streams."
      In Proceedings of the sixth ACM SIGKDD international conference on
      Knowledge discovery and data mining, pp. 71-80. 2000.


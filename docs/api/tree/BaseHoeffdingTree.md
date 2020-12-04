# BaseHoeffdingTree

Base class for Hoeffding Decision Trees.

This is an **abstract class**, so it cannot be used directly. It defines base operations and properties that all the decision trees must inherit or implement according to their own design. 

All the extended classes inherit the following functionality: 

* Set the maximum tree depth allowed (`max_depth`). 

* Handle *Active* and *Inactive* nodes: Active learning nodes update their own internal state to improve predictions and monitor input features to perform split attempts. Inactive learning nodes do not update their internal state and only keep the predictors; they are used to save memory in the tree (`max_size`). 

*  Enable/disable memory management. 

* Define strategies to sort leaves according to how likely they are going to be split. This enables deactivating non-promising leaves to save memory. 

* Disabling ‘poor’ attributes to save memory and speed up tree construction. A poor attribute is an input feature whose split merit is much smaller than the current best candidate. Once a feature is disabled, the tree stops saving statistics necessary to split such a feature. 

* Define properties to access leaf prediction strategies, split criteria, and other relevant characteristics.

## Parameters

- **max_depth** (*int*) – defaults to `None`

    The maximum depth a tree can reach. If `None`, the tree will grow indefinitely.

- **binary_split** (*bool*) – defaults to `False`

    If True, only allow binary splits.

- **max_size** (*int*) – defaults to `100`

    The max size of the tree, in Megabytes (MB).

- **memory_estimate_period** (*int*) – defaults to `1000000`

    Interval (number of processed instances) between memory consumption checks.

- **stop_mem_management** (*bool*) – defaults to `False`

    If True, stop growing as soon as memory limit is hit.

- **remove_poor_attrs** (*bool*) – defaults to `False`

    If True, disable poor attributes to reduce memory usage.

- **merit_preprune** (*bool*) – defaults to `True`

    If True, enable merit-based tree pre-pruning.


## Attributes

- **depth**

    The depth of the tree.

- **leaf_prediction**

    Return the prediction strategy used by the tree at its leaves.

- **max_size**

    Max allowed size tree can reach (in MB).

- **model_measurements**

    Collect metrics corresponding to the current status of the tree in a string buffer.

- **split_criterion**

    Return a string with the name of the split criterion being used by the tree.



## Methods

???- note "debug_one"

    Print an explanation of how `x` is predicted.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Union[str, NoneType]*:     A representation of the path followed by the tree to predict `x`; `None` if
    
???- note "draw"

    Draw the tree using the `graphviz` library.

    Since the tree is drawn without passing incoming samples, classification trees will show the majority class in their leaves, whereas regression trees will use the target mean.

    **Parameters**

    - **max_depth**     (*int*)     – defaults to `None`    
        The maximum depth a tree can reach. If `None`, the tree will grow indefinitely.
    
???- note "model_description"

    Walk the tree and return its structure in a buffer.

    
    **Returns**

    The description of the model.
    
## Notes

Hoeffding trees might face situations where an input feature previously used to make
a split decision is missing in an incoming sample. In this case, the trees follow the
conventions:

- *Learning:* choose the subtree branch most traversed so far to pass the instance on.</br>
- *Predicting:* Use the last "reachable" decision node to provide responses.


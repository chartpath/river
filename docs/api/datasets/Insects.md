# Insects

Insects dataset.

This dataset has different variants, which are: 

- abrupt_balanced - abrupt_imbalanced - gradual_balanced - gradual_imbalanced - incremental-abrupt_balanced - incremental-abrupt_imbalanced - incremental-reoccurring_balanced - incremental-reoccurring_imbalanced - incremental_balanced - incremental_imbalanced - out-of-control 

The number of samples and the difficulty change from one variant to another. The number of classes is always the same (6), except for the last variant (24).

## Parameters

- **variant** – defaults to `abrupt_balanced`

    Indicates which variant of the dataset to load.


## Attributes

- **desc**

    Return the description from the docstring.

- **is_downloaded**

    Indicate whether or the data has been correctly downloaded.

- **path**



## Methods

???- note "download"

???- note "take"

    Iterate over the k samples.

    **Parameters**

    - **k**     (*int*)    
    
## References

[^1]: [USP DS repository](https://sites.google.com/view/uspdsrepository)
[^2]: [Souza, V., Reis, D.M.D., Maletzke, A.G. and Batista, G.E., 2020. Challenges in Benchmarking Stream Learning Algorithms with Real-world Data. arXiv preprint arXiv:2005.00113.](https://arxiv.org/abs/2005.00113)


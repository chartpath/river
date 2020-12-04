# LDA

Online Latent Dirichlet Allocation with Infinite Vocabulary.

Latent Dirichlet allocation (LDA) is a probabilistic approach for exploring topics in document collections. The key advantage of this variant is that it assumes an infinite vocabulary, meaning that the set of tokens does not have to known in advance, as opposed to the [implementation from sklearn](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.LatentDirichletAllocation.html) The results produced by this implementation are identical to those from [the original implementation](https://github.com/kzhai/PyInfVoc) proposed by the method's authors. 

This class takes as input token counts. Therefore, it requires you to tokenize beforehand. You can do so by using a `feature_extraction.BagOfWords` instance, as shown in the example below.

## Parameters

- **n_components** – defaults to `10`

    Number of topics of the latent Drichlet allocation.

- **number_of_documents** – defaults to `1000000.0`

    Estimated number of documents.

- **alpha_theta** – defaults to `0.5`

    Hyper-parameter of the Dirichlet distribution of topics.

- **alpha_beta** – defaults to `100.0`

    Hyper-parameter of the Dirichlet process of distribution over words.

- **tau** – defaults to `64.0`

    Learning inertia to prevent premature convergence.

- **kappa** – defaults to `0.75`

    The learning rate kappa controls how quickly new parameters estimates replace the old ones. kappa ∈ (0.5, 1] is required for convergence.

- **vocab_prune_interval** – defaults to `10`

    Interval at which to refresh the words topics distribution.

- **number_of_samples** – defaults to `10`

    Number of iteration to computes documents topics distribution.

- **ranking_smooth_factor** – defaults to `1e-12`

- **burn_in_sweeps** – defaults to `5`

    Number of iteration necessaries while analyzing a document before updating document topics distribution.

- **maximum_size_vocabulary** – defaults to `4000`

    Maximum size of the stored vocabulary.

- **seed** (*int*) – defaults to `None`

    Random number seed used for reproducibility.


## Attributes

- **counter** (*int*)

    The current number of observed documents.

- **truncation_size_prime** (*int*)

    Number of distincts words stored in the vocabulary. Updated before processing a document.

- **truncation_size** (*int*)

    Number of distincts words stored in the vocabulary. Updated after processing a document.

- **word_to_index** (*dict*)

    Words as keys and indexes as values.

- **index_to_word** (*dict*)

    Indexes as keys and words as values.

- **nu_1** (*dict*)

    Weights of the words. Component of the variational inference.

- **nu_2** (*dict*)

    Weights of the words. Component of the variational inference.


## Examples

```python
>>> from river import compose
>>> from river import feature_extraction
>>> from river import preprocessing

>>> X = [
...    'weather cold',
...    'weather hot dry',
...    'weather cold rainy',
...    'weather hot',
...    'weather cold humid',
... ]

>>> lda = compose.Pipeline(
...     feature_extraction.BagOfWords(),
...     preprocessing.LDA(
...         n_components=2,
...         number_of_documents=60,
...         seed=42
...     )
... )

>>> for x in X:
...     lda = lda.learn_one(x)
...     topics = lda.transform_one(x)
...     print(topics)
{0: 2.5, 1: 0.5}
{0: 2.5, 1: 1.5}
{0: 1.5, 1: 2.5}
{0: 1.5, 1: 1.5}
{0: 0.5, 1: 3.5}
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
    
???- note "learn_transform_one"

    Equivalent to `lda.learn_one(x).transform_one(x)`s, but faster.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *dict*:     Component attributions for the input document.
    
???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *dict*:     The transformed values.
    
## References

[^1]: [Zhai, K. and Boyd-Graber, J., 2013, February. Online latent Dirichlet allocation with infinite vocabulary. In International Conference on Machine Learning (pp. 561-569).](http://proceedings.mlr.press/v28/zhai13.pdf)
[^2]: [PyInfVoc on GitHub](https://github.com/kzhai/PyInfVoc)


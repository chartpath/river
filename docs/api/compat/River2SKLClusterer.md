# River2SKLClusterer

Compatibility layer from River to scikit-learn for clustering.



## Parameters

- **estimator** (*[base.Clusterer](../../base/Clusterer)*)




## Methods

???- note "fit"

    Fits to an entire dataset contained in memory.

    **Parameters**

    - **X**    
    - **y**     – defaults to `None`    
    
    **Returns**

    self
    
???- note "fit_predict"

    Perform clustering on X and returns cluster labels.

    **Parameters**

    - **X**    
    - **y**     – defaults to `None`    
    
    **Returns**

    ndarray of shape (n_samples,)
    
???- note "get_params"

    Get parameters for this estimator.

    **Parameters**

    - **deep**     – defaults to `True`    
    
    **Returns**

    mapping of string to any
    
???- note "partial_fit"

    Fits incrementally on a portion of a dataset.

    **Parameters**

    - **X**    
    - **y**    
    
    **Returns**

    self
    
???- note "predict"

    Predicts the target of an entire dataset contained in memory.

    **Parameters**

    - **X**    
    
    **Returns**

    Transformed output.
    
???- note "set_params"

    Set the parameters of this estimator.

    The method works on simple estimators as well as on nested objects (such as pipelines). The latter have parameters of the form ``<component>__<parameter>`` so that it's possible to update each component of a nested object.

    **Parameters**

    - **params**    
    
    **Returns**

    object
    

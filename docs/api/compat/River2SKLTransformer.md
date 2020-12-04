# River2SKLTransformer

Compatibility layer from River to scikit-learn for transformation.



## Parameters

- **estimator** (*[base.Transformer](../../base/Transformer)*)




## Methods

???- note "fit"

    Fits to an entire dataset contained in memory.

    **Parameters**

    - **X**    
    - **y**     – defaults to `None`    
    
    **Returns**

    self
    
???- note "fit_transform"

    Fit to data, then transform it.

    Fits transformer to X and y with optional parameters fit_params and returns a transformed version of X.

    **Parameters**

    - **X**    
    - **y**     – defaults to `None`    
    - **fit_params**    
    
    **Returns**

    ndarray array of shape (n_samples, n_features_new)
    
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
    - **y**     – defaults to `None`    
    
    **Returns**

    self
    
???- note "set_params"

    Set the parameters of this estimator.

    The method works on simple estimators as well as on nested objects (such as pipelines). The latter have parameters of the form ``<component>__<parameter>`` so that it's possible to update each component of a nested object.

    **Parameters**

    - **params**    
    
    **Returns**

    object
    
???- note "transform"

    Predicts the target of an entire dataset contained in memory.

    **Parameters**

    - **X**    
    
    **Returns**

    Transformed output.
    

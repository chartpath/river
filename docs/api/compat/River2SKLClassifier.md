# River2SKLClassifier

Compatibility layer from River to scikit-learn for classification.



## Parameters

- **estimator** (*[base.Classifier](../../base/Classifier)*)




## Methods

???- note "fit"

    Fits to an entire dataset contained in memory.

    **Parameters**

    - **X**    
    - **y**    
    
    **Returns**

    self
    
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
    - **classes**     – defaults to `None`    
    
    **Returns**

    self
    
???- note "predict"

    Predicts the target of an entire dataset contained in memory.

    **Parameters**

    - **X**    
    
    **Returns**

    Predicted target values for each row of `X`.
    
???- note "predict_proba"

    Predicts the target probability of an entire dataset contained in memory.

    **Parameters**

    - **X**    
    
    **Returns**

    Predicted target values for each row of `X`.
    
???- note "score"

    Return the mean accuracy on the given test data and labels.

    In multi-label classification, this is the subset accuracy which is a harsh metric since you require for each sample that each label set be correctly predicted.

    **Parameters**

    - **X**    
    - **y**    
    - **sample_weight**     – defaults to `None`    
    
    **Returns**

    float
    
???- note "set_params"

    Set the parameters of this estimator.

    The method works on simple estimators as well as on nested objects (such as pipelines). The latter have parameters of the form ``<component>__<parameter>`` so that it's possible to update each component of a nested object.

    **Parameters**

    - **params**    
    
    **Returns**

    object
    

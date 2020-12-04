# River2SKLRegressor

Compatibility layer from River to scikit-learn for regression.



## Parameters

- **estimator** (*[base.Regressor](../../base/Regressor)*)




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
    
    **Returns**

    self
    
???- note "predict"

    Predicts the target of an entire dataset contained in memory.

    **Parameters**

    - **X**    
    
    **Returns**

    *ndarray*:     Predicted target values for each row of `X`.
    
???- note "score"

    Return the coefficient of determination R^2 of the prediction.

    The coefficient R^2 is defined as (1 - u/v), where u is the residual sum of squares ((y_true - y_pred) ** 2).sum() and v is the total sum of squares ((y_true - y_true.mean()) ** 2).sum(). The best possible score is 1.0 and it can be negative (because the model can be arbitrarily worse). A constant model that always predicts the expected value of y, disregarding the input features, would get a R^2 score of 0.0.

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
    

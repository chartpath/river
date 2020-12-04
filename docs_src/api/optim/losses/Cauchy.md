# Cauchy

Cauchy loss function.



## Parameters

- **C** – defaults to `80`




## Methods

???- note "__call__"

    Returns the loss.

    **Parameters**

    - **y_true**    
    - **y_pred**    
    
    **Returns**

    The loss(es).
    
???- note "gradient"

    Return the gradient with respect to y_pred.

    **Parameters**

    - **y_true**    
    - **y_pred**    
    
    **Returns**

    The gradient(s).
    
???- note "mean_func"

    Mean function.

    This is the inverse of the link function. Typically, a loss function takes as input the raw output of a model. In the case of classification, the raw output would be logits. The mean function can be used to convert the raw output into a value that makes sense to the user, such as a probability.

    **Parameters**

    - **y_pred**    
    
    **Returns**

    The adjusted prediction(s).
    
## References

[^1]: ["Effect of MAE" Kaggle discussion](https://www.kaggle.com/c/allstate-claims-severity/discussion/24520#140163)
[^2]: [Paris Madness Kaggle kernel](https://www.kaggle.com/raddar/paris-madness)


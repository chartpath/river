# Poisson

Poisson loss.

The Poisson loss is usually more suited for regression with count data than the squared loss. 

Mathematically, it is defined as 

$$L = exp(p_i) - y_i \times p_i$$ 

It's gradient w.r.t. to $p_i$ is 

$$\frac{\partial L}{\partial p_i} = exp(p_i) - y_i$$




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
    

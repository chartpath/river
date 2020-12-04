# Absolute

Absolute loss, also known as the mean absolute error or L1 loss.

Mathematically, it is defined as 

$$L = |p_i - y_i|$$ 

It's gradient w.r.t. to $p_i$ is 

$$\frac{\partial L}{\partial p_i} = sgn(p_i - y_i)$$



## Examples

```python
>>> from river import optim

>>> loss = optim.losses.Absolute()
>>> loss(-42, 42)
84
>>> loss.gradient(1, 2)
1
>>> loss.gradient(2, 1)
-1
```

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
    

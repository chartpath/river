# Squared

Squared loss, also known as the L2 loss.

Mathematically, it is defined as 

$$L = (p_i - y_i) ^ 2$$ 

It's gradient w.r.t. to $p_i$ is 

$$\frac{\partial L}{\partial p_i} = 2       imes (p_i - y_i)$$ 

One thing to note is that this convention is consistent with Vowpal Wabbit and PyTorch, but not with scikit-learn. Indeed, scikit-learn divides the loss by 2, making the 2 disappear in the gradient.



## Examples

```python
>>> from river import optim

>>> loss = optim.losses.Squared()
>>> loss(-4, 5)
81
>>> loss.gradient(-4, 5)
18
>>> loss.gradient(5, -4)
-18
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
    

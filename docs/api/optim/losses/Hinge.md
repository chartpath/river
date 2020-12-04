# Hinge

Computes the hinge loss.

Mathematically, it is defined as 

$$L = max(0, 1 - p_i * y_i)$$ 

It's gradient w.r.t. to $p_i$ is 

$$ \frac{\partial L}{\partial y_i} = \left\{ \begin{array}{ll}     \ 0  &   p_iy_i \geqslant 1  \\     \ - y_i & p_iy_i < 1 \end{array} \right. $$

## Parameters

- **threshold** – defaults to `1.0`

    Margin threshold. 1 yield the loss used in SVMs, whilst 0 is equivalent to the loss used in the Perceptron algorithm.



## Examples

```python
>>> from river import optim

>>> loss = optim.losses.Hinge(threshold=1)
>>> loss(1, .2)
0.8

>>> loss.gradient(1, .2)
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
    

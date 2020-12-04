# Quantile

Quantile loss.



## Parameters

- **alpha** – defaults to `0.5`

    Desired quantile to attain.



## Examples

```python
>>> from river import optim

>>> loss = optim.losses.Quantile(0.5)
>>> loss(1, 3)
1.0

>>> loss.gradient(1, 3)
0.5

>>> loss.gradient(3, 1)
-0.5
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
    
## References

[^1]: [Wikipedia article on quantile regression](https://www.wikiwand.com/en/Quantile_regression)
[^2]: [Derivative from WolframAlpha](https://www.wolframalpha.com/input/?i=derivative+(y+-+p)+*+(alpha+-+Boole(y+-+p))+wrt+p)


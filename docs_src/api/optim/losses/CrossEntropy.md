# CrossEntropy

Cross entropy loss.

This is a generalization of logistic loss to multiple classes.

## Parameters

- **class_weight** (*Dict[Union[bool, str, int], float]*) – defaults to `None`

    A dictionary that indicates what weight to associate with each class.



## Examples

```python
>>> from river import optim

>>> y_true = [0, 1, 2, 2]
>>> y_pred = [
...     {0: 0.29450637, 1: 0.34216758, 2: 0.36332605},
...     {0: 0.21290077, 1: 0.32728332, 2: 0.45981591},
...     {0: 0.42860913, 1: 0.33380113, 2: 0.23758974},
...     {0: 0.44941979, 1: 0.32962558, 2: 0.22095463}
... ]

>>> loss = optim.losses.CrossEntropy()

>>> for yt, yp in zip(y_true, y_pred):
...     print(loss(yt, yp))
1.222454
1.116929
1.437209
1.509797

>>> for yt, yp in zip(y_true, y_pred):
...     print(loss.gradient(yt, yp))
{0: -0.70549363, 1: 0.34216758, 2: 0.36332605}
{0: 0.21290077, 1: -0.67271668, 2: 0.45981591}
{0: 0.42860913, 1: 0.33380113, 2: -0.76241026}
{0: 0.44941979, 1: 0.32962558, 2: -0.77904537}
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

[^1]: [What is Softmax regression and how is it related to Logistic regression?](https://github.com/rasbt/python-machine-learning-book/blob/master/faq/softmax_regression.md)


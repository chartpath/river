# ConfusionMatrix

ConfusionMatrix(classes=None) Confusion Matrix for binary-class and multi-class classification.




## Attributes

- **classes**

- **data**

- **last_y_pred**

- **last_y_true**

- **majority_class**

- **n_classes**

- **n_samples**

- **sample_correction**

- **shape**

- **sum_col**

- **sum_diag**

- **sum_row**

- **total_weight**

- **weight_majority_classifier**

- **weight_no_change_classifier**


## Examples

```python
>>> from river import metrics

>>> y_true = ['cat', 'ant', 'cat', 'cat', 'ant', 'bird']
>>> y_pred = ['ant', 'ant', 'cat', 'cat', 'ant', 'cat']

>>> cm = metrics.ConfusionMatrix()

>>> for yt, yp in zip(y_true, y_pred):
...     cm = cm.update(yt, yp)

>>> cm
       ant  bird   cat
 ant     2     0     0
bird     0     0     1
 cat     1     0     2

>>> cm['bird']['cat']
1.0
```

## Methods

???- note "false_negatives"

    

    **Parameters**

    - **label**    
    
???- note "false_positives"

    

    **Parameters**

    - **label**    
    
???- note "reset"

    

    
???- note "revert"

    

    **Parameters**

    - **y_true**    
    - **y_pred**    
    - **sample_weight**    
    - **correction**    
    
???- note "true_negatives"

    

    **Parameters**

    - **label**    
    
???- note "true_positives"

    

    **Parameters**

    - **label**    
    
???- note "update"

    

    **Parameters**

    - **y_true**    
    - **y_pred**    
    - **sample_weight**    
    
## Notes

    This confusion matrix is a 2D matrix of shape `(n_classes, n_classes)`, corresponding
    to a single-target (binary and multi-class) classification task.

    Each row represents `true` (actual) class-labels, while each column corresponds
    to the `predicted` class-labels. For example, an entry in position `[1, 2]` means
    that the true class-label is 1, and the predicted class-label is 2 (incorrect prediction).

    This structure is used to keep updated statistics about a single-output classifier's
    performance and to compute multiple evaluation metrics.


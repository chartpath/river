# progressive_val_score

Evaluates the performance of a model on a streaming dataset.

This method is the canonical way to evaluate a model's performance. When used correctly, it allows you to exactly assess how a model would have performed in a production scenario. 

`dataset` is converted into a stream of questions and answers. At each step the model is either asked to predict an observation, or is either updated. The target is only revealed to the model after a certain amount of time, which is determined by the `delay` parameter. Note that under the hood this uses the [`stream.simulate_qa`](../../stream/simulate-qa) function to go through the data in arrival order. 

By default, there is no delay, which means that the samples are processed one after the other. When there is no delay, this function essentially performs progressive validation. When there is a delay, then we refer to it as delayed progressive validation. 

It is recommended to use this method when you want to determine a model's performance on a dataset. In particular, it is advised to use the `delay` parameter in order to get a reliable assessment. Indeed, in a production scenario, it is often the case that ground truths are made available after a certain amount of time. By using this method, you can reproduce this scenario and therefore truthfully assess what would have been the performance of a model on a given dataset.

## Parameters

- **dataset** (*Iterator[Tuple[dict, Any]]*)

    The stream of observations against which the model will be evaluated.

- **model**

    The model to evaluate.

- **metric** (*river.metrics.base.Metric*)

    The metric used to evaluate the model's predictions.

- **moment** (*Union[str, Callable]*) – defaults to `None`

    The attribute used for measuring time. If a callable is passed, then it is expected to take as input a `dict` of features. If `None`, then the observations are implicitly timestamped in the order in which they arrive.

- **delay** (*Union[str, int, datetime.timedelta, Callable]*) – defaults to `None`

    The amount to wait before revealing the target associated with each observation to the model. This value is expected to be able to sum with the `moment` value. For instance, if `moment` is a `datetime.date`, then `delay` is expected to be a `datetime.timedelta`. If a callable is passed, then it is expected to take as input a `dict` of features and the target. If a `str` is passed, then it will be used to access the relevant field from the features. If `None` is passed, then no delay will be used, which leads to doing standard online validation.

- **print_every** – defaults to `0`

    Iteration number at which to print the current metric. This only takes into account the predictions, and not the training steps.

- **show_time** – defaults to `False`

    Whether or not to display the elapsed time.

- **show_memory** – defaults to `False`

    Whether or not to display the memory usage of the model.

- **print_kwargs**

    Extra keyword arguments are passed to the `print` function. For instance, this allows providing a `file` argument, which indicates where to output progress.



## Examples

Take the following model:

```python
>>> from river import linear_model
>>> from river import preprocessing

>>> model = (
...     preprocessing.StandardScaler() |
...     linear_model.LogisticRegression()
... )

```

We can evaluate it on the `Phishing` dataset as so:

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import metrics

>>> evaluate.progressive_val_score(
...     model=model,
...     dataset=datasets.Phishing(),
...     metric=metrics.ROCAUC(),
...     print_every=200
... )
[200] ROCAUC: 0.897995
[400] ROCAUC: 0.920896
[600] ROCAUC: 0.931339
[800] ROCAUC: 0.939909
[1,000] ROCAUC: 0.947417
[1,200] ROCAUC: 0.950304
ROCAUC: 0.950363

```

We haven't specified a delay, therefore this is strictly equivalent to the following piece
of code:

```python
>>> model = (
...     preprocessing.StandardScaler() |
...     linear_model.LogisticRegression()
... )

>>> metric = metrics.ROCAUC()

>>> for x, y in datasets.Phishing():
...     y_pred = model.predict_proba_one(x)
...     metric = metric.update(y, y_pred)
...     model = model.learn_one(x, y)

>>> metric
ROCAUC: 0.950363

```

When `print_every` is specified, the current state is printed at regular intervals. Under
the hood, Python's `print` method is being used. You can pass extra keyword arguments to
modify its behavior. For instance, you may use the `file` argument if you want to log the
progress to a file of your choice.

```python
>>> with open('progress.log', 'w') as f:
...     metric = evaluate.progressive_val_score(
...         model=model,
...         dataset=datasets.Phishing(),
...         metric=metrics.ROCAUC(),
...         print_every=200,
...         file=f
...     )

>>> with open('progress.log') as f:
...     for line in f.read().splitlines():
...         print(line)
[200] ROCAUC: 0.94
[400] ROCAUC: 0.946969
[600] ROCAUC: 0.9517
[800] ROCAUC: 0.954238
[1,000] ROCAUC: 0.958207
[1,200] ROCAUC: 0.96002

```

Note that the performance is slightly better than above because we haven't used a fresh
copy of the model. Instead, we've reused the existing model which has already done a full
pass on the data.

```python
>>> import os; os.remove('progress.log')
```

## References

[^1]: [Beating the Hold-Out: Bounds for K-fold and Progressive Cross-Validation](http://hunch.net/~jl/projects/prediction_bounds/progressive_validation/coltfinal.pdf)
[^2]: [Grzenda, M., Gomes, H.M. and Bifet, A., 2019. Delayed labelling evaluation for data streams. Data Mining and Knowledge Discovery, pp.1-30](https://link.springer.com/content/pdf/10.1007%2Fs10618-019-00654-y.pdf)


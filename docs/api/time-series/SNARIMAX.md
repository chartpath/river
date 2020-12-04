# SNARIMAX

SNARIMAX model.

SNARIMAX stands for (S)easonal (N)on-linear (A)uto(R)egressive (I)ntegrated (M)oving-(A)verage with e(X)ogenous inputs model. 

This model generalizes many established time series models in a single interface that can be trained online. It assumes that the provided training data is ordered in time and is uniformly spaced. It is made up of the following components: 

- S (Seasonal) - N (Non-linear): Any online regression model can be used, not necessarily a linear regression     as is done in textbooks. - AR (Autoregressive): Lags of the target variable are used as features. - I (Integrated): The model can be fitted on a differenced version of a time series. In this     context, integration is the reverse of differencing. - MA (Moving average): Lags of the errors are used as features. - X (Exogenous): Users can provide additional features. Care has to be taken to include     features that will be available both at training and prediction time. 

Each of these components can be switched on and off by specifying the appropriate parameters. Classical time series models such as AR, MA, ARMA, and ARIMA can thus be seen as special parametrizations of the SNARIMAX model. 

This model is tailored for time series that are homoskedastic. In other words, it might not work well if the variance of the time series varies widely along time.

## Parameters

- **p** (*int*)

    Order of the autoregressive part. This is the number of past target values that will be included as features.

- **d** (*int*)

    Differencing order.

- **q** (*int*)

    Order of the moving average part. This is the number of past error terms that will be included as features.

- **m** (*int*) – defaults to `1`

    Season length used for extracting seasonal features. If you believe your data has a seasonal pattern, then set this accordingly. For instance, if the data seems to exhibit a yearly seasonality, and that your data is spaced by month, then you should set this to 12. Note that for this parameter to have any impact you should also set at least one of the `p`, `d`, and `q` parameters.

- **sp** (*int*) – defaults to `0`

    Seasonal order of the autoregressive part. This is the number of past target values that will be included as features.

- **sd** (*int*) – defaults to `0`

    Seasonal differencing order.

- **sq** (*int*) – defaults to `0`

    Seasonal order of the moving average part. This is the number of past error terms that will be included as features.

- **regressor** (*[base.Regressor](../../base/Regressor)*) – defaults to `None`

    The online regression model to use. By default, a `preprocessing.StandardScaler` piped with a `linear_model.LinearRegression` will be used.


## Attributes

- **differencer** (*Differencer*)

- **y_trues** (*collections.deque*)

    The `p` past target values.

- **errors** (*collections.deque*)

    The `q` past error values.


## Examples

```python
>>> import calendar
>>> import datetime as dt
>>> from river import compose
>>> from river import datasets
>>> from river import linear_model
>>> from river import metrics
>>> from river import optim
>>> from river import preprocessing
>>> from river import time_series

>>> def get_month_distances(x):
...     return {
...         calendar.month_name[month]: math.exp(-(x['month'].month - month) ** 2)
...         for month in range(1, 13)
...     }

>>> def get_ordinal_date(x):
...     return {'ordinal_date': x['month'].toordinal()}

>>> extract_features = compose.TransformerUnion(
...     get_ordinal_date,
...     get_month_distances
... )

>>> model = (
...     extract_features |
...     time_series.SNARIMAX(
...         p=0,
...         d=0,
...         q=0,
...         m=12,
...         sp=3,
...         sq=6,
...         regressor=(
...             preprocessing.StandardScaler() |
...             linear_model.LinearRegression(
...                 intercept_init=110,
...                 optimizer=optim.SGD(0.01),
...                 intercept_lr=0.3
...             )
...         )
...     )
... )

>>> metric = metrics.Rolling(metrics.MAE(), 12)

>>> for x, y in datasets.AirlinePassengers():
...     y_pred = model.forecast(horizon=1, xs=[x])
...     model = model.learn_one(x, y)
...     metric = metric.update(y, y_pred[0])

>>> metric
Rolling of size 12 MAE: 11.636563

>>> horizon = 12
>>> future = [
...     {'month': dt.date(year=1961, month=m, day=1)}
...     for m in range(1, horizon + 1)
... ]
>>> forecast = model.forecast(horizon=horizon, xs=future)
>>> for x, y_pred in zip(future, forecast):
...     print(x['month'], f'{y_pred:.3f}')
1961-01-01 442.554
1961-02-01 427.305
1961-03-01 471.861
1961-04-01 483.978
1961-05-01 489.995
1961-06-01 544.270
1961-07-01 632.882
1961-08-01 633.229
1961-09-01 531.349
1961-10-01 457.258
1961-11-01 405.978
1961-12-01 439.674
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "forecast"

    Makes forecast at each step of the given horizon.

    **Parameters**

    - **horizon**     (*int*)    
    - **xs**     (*list*)     – defaults to `None`    
    
???- note "learn_one"

    Updates the model.

    **Parameters**

    - **y**     (*float*)    
    - **x**     (*dict*)     – defaults to `None`    
    
## References

[^1]: [Wikipedia page on ARMA](https://www.wikiwand.com/en/Autoregressive%E2%80%93moving-average_model)
[^2]: [Wikipedia page on NARX](https://www.wikiwand.com/en/Nonlinear_autoregressive_exogenous_model)
[^3]: [ARIMA models](https://otexts.com/fpp2/arima.html)
[^4]: [Anava, O., Hazan, E., Mannor, S. and Shamir, O., 2013, June. Online learning for time series prediction. In Conference on learning theory (pp. 172-184)](https://arxiv.org/pdf/1302.6927.pdf)


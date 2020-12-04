# MiniBatchRegressor

A regressor that can operate on mini-batches.






## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_many"

    Update the model with a mini-batch of features `X` and boolean targets `y`.

    **Parameters**

    - **X**     (*pandas.core.frame.DataFrame*)    
    - **y**     (*pandas.core.series.Series*)    
    - **kwargs**    
    
    **Returns**

    *MiniBatchRegressor*:     self
    
???- note "learn_one"

    Fits to a set of features `x` and a real-valued target `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*numbers.Number*)    
    - **kwargs**    
    
    **Returns**

    *Regressor*:     self
    
???- note "predict_many"

    Predict the outcome for each given sample.

    Parameters --------- X     A dataframe of features.

    **Parameters**

    - **X**     (*pandas.core.frame.DataFrame*)    
    
    **Returns**

    *Series*:     The predicted outcomes.
    
???- note "predict_one"

    Predicts the target value of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *Number*:     The prediction.
    

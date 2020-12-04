# Gaussian

Normal distribution with parameters mu and sigma.




## Attributes

- **mode**

    Most likely value.

- **mu**

- **n_samples**

    The number of observed samples.

- **sigma**


## Examples

```python
>>> from river import proba

>>> p = proba.Gaussian().update(6).update(7)

>>> p
𝒩(μ=6.500, σ=0.707)

>>> p.pdf(6.5)
0.564189
```

## Methods

???- note "cdf"

    Cumulative density function, i.e. P(X <= x).

    **Parameters**

    - **x**    
    
???- note "pdf"

    Probability density function, i.e. P(x <= X < x+dx) / dx.

    **Parameters**

    - **x**    
    
???- note "update"

    Updates the parameters of the distribution given a new observation.

    **Parameters**

    - **x**    
    - **w**     – defaults to `1.0`    
    

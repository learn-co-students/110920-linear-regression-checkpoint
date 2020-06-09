# Linear Regression Checkpoint

In this checkpoint, you'll be using the Advertising data you encountered previously, containing amounts spent on different advertising platforms and the resulting sales.  Each observation is a different product.  

We'll import the relevant modules and load and prepare the dataset for you below.


```python
# Run this cell without changes
import pandas as pd
import statsmodels.api as sm
from statsmodels.formula.api import ols
```


```python
# Run this cell without changes
data = pd.read_csv('data/advertising.csv').drop('Unnamed: 0', axis=1)
data.describe()
```


```python
# Run this cell without changes

X = data.drop('sales', axis=1)
y = data['sales']
```

In the linear regression section of the curriculum, you analyzed how `TV`, `radio`, and `newspaper` spending individually affected figures for `sales`. Here, we'll use all three together in a multiple linear regression model!

## 1) Create a Correlation Matrix for `X`


```python
# Your code here
```

## 2) Based on this correlation matrix only, would you recommend using `TV`, `radio`, and `newspaper` in the same multiple linear regression model?


```python
# Your written answer here
```

## 3) Create a multiple linear regression model (using either `ols()` or `sm.OLS()`).  Use `TV`, `radio`, and `newspaper` as independent variables, and `sales` as the dependent variable.

### Produce the model summary table of this multiple linear regression model.


```python
# Your code here
```

## 4) For each coefficient:

### - Conclude whether it's statistically significant 

### - State how you came to that conclusion

## Interpret how these results relate to your answer for Question 2


```python
# Your written answer here
```


```python

```

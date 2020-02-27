## Linear Regression

In this section, you'll be using the Advertising data, and you'll be creating a linear model that is more complicated than a simple linear regression. We'll import the relevant modules and load and prepare the dataset for you below.


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

In the linear regression section of the curriculum, you analyzed how TV, Radio, and Newspaper spendings individually affected the Sales figures. Here, we'll use all three together in a multiple linear regression model!

## 1) Create a Correlation Matrix for `X`


```python
# Your code here
```

## 2) Based on this correlation matrix only, would you recommend to use `TV`, `radio`, and `newspaper` in the same multiple linear regression model?


```python
# Your written answer here
```

## 3) Use StatsModels' `ols` or `OLS` to create a multiple linear regression model with `TV`, `radio`, and `newspaper` as independent variables and `sales` as the dependent variable.

**Required output:** the model summary of this multiple regression model.


```python
# Your code here
```

## 4) Do we have any statistically significant coefficients? If the answer is yes, list them below.

Interpret how these results relate to your answer for Question 2


```python
# Your written answer here
```


```python

```

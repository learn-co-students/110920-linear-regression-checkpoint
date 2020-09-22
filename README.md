# Linear Regression Checkpoint

In this section, you'll be using the Advertising data to run regression models. In this dataset, each row represents a different product, and we have a sample of 200 products from a larger population of products. We have three features - `TV`, `radio`, and `newspaper` - that describe how many thousands of advertising dollars were spent promoting the product. The target, `sales`, describes how many millions of dollars in sales the product had.

We'll import the relevant modules and load and prepare the dataset for you below.


```python
# Run this cell without changes
import pandas as pd
import statsmodels
import statsmodels.api as sm
from statsmodels.formula.api import ols
```


```python
# Run this cell without changes
data = pd.read_csv('data/advertising.csv', index_col=0)
data.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>TV</th>
      <th>radio</th>
      <th>newspaper</th>
      <th>sales</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>200.000000</td>
      <td>200.000000</td>
      <td>200.000000</td>
      <td>200.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>147.042500</td>
      <td>23.264000</td>
      <td>30.554000</td>
      <td>14.022500</td>
    </tr>
    <tr>
      <th>std</th>
      <td>85.854236</td>
      <td>14.846809</td>
      <td>21.778621</td>
      <td>5.217457</td>
    </tr>
    <tr>
      <th>min</th>
      <td>0.700000</td>
      <td>0.000000</td>
      <td>0.300000</td>
      <td>1.600000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>74.375000</td>
      <td>9.975000</td>
      <td>12.750000</td>
      <td>10.375000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>149.750000</td>
      <td>22.900000</td>
      <td>25.750000</td>
      <td>12.900000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>218.825000</td>
      <td>36.525000</td>
      <td>45.100000</td>
      <td>17.400000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>296.400000</td>
      <td>49.600000</td>
      <td>114.000000</td>
      <td>27.000000</td>
    </tr>
  </tbody>
</table>
</div>



## Simple Linear Regression

### 1) Use StatsModels' `ols` function (imported above) to run a linear regression using just `TV` to predict `sales`

Produce the model summary table of this simple linear regression model.


```python
# Replace None with appropriate code
model = None
results = None
### BEGIN SOLUTION

# The Test class does not seem to be compatible with a StatsModels
# model right now.  When I save then run_test on this model, it
# throws an assert error.  It's possible that the .summary() call
# mutates the actual model object

# Therefore, for now this is a manually graded answer

formula = 'sales ~ TV'
model = ols(formula = formula, data = data)
results = model.fit()

### END SOLUTION

results.summary()
```




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>          <td>sales</td>      <th>  R-squared:         </th> <td>   0.612</td>
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th> <td>   0.610</td>
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th> <td>   312.1</td>
</tr>
<tr>
  <th>Date:</th>             <td>Tue, 22 Sep 2020</td> <th>  Prob (F-statistic):</th> <td>1.47e-42</td>
</tr>
<tr>
  <th>Time:</th>                 <td>12:33:30</td>     <th>  Log-Likelihood:    </th> <td> -519.05</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td>   200</td>      <th>  AIC:               </th> <td>   1042.</td>
</tr>
<tr>
  <th>Df Residuals:</th>          <td>   198</td>      <th>  BIC:               </th> <td>   1049.</td>
</tr>
<tr>
  <th>Df Model:</th>              <td>     1</td>      <th>                     </th>     <td> </td>   
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>     <td> </td>   
</tr>
</table>
<table class="simpletable">
<tr>
      <td></td>         <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>Intercept</th> <td>    7.0326</td> <td>    0.458</td> <td>   15.360</td> <td> 0.000</td> <td>    6.130</td> <td>    7.935</td>
</tr>
<tr>
  <th>TV</th>        <td>    0.0475</td> <td>    0.003</td> <td>   17.668</td> <td> 0.000</td> <td>    0.042</td> <td>    0.053</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td> 0.531</td> <th>  Durbin-Watson:     </th> <td>   1.935</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.767</td> <th>  Jarque-Bera (JB):  </th> <td>   0.669</td>
</tr>
<tr>
  <th>Skew:</th>          <td>-0.089</td> <th>  Prob(JB):          </th> <td>   0.716</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 2.779</td> <th>  Cond. No.          </th> <td>    338.</td>
</tr>
</table><br/><br/>Warnings:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.



### 2) Can we infer that products with higher TV advertising spend tend to have greater sales? Explain how you determined this from the model output.

This question is asking you to use your findings from the sample in your dataset to make an inference about the relationship between TV advertising spend and sales in the broader population.

Assign `ans2` to `True` if products with higher TV advertising tend to have greater sales, `False` if not.  Then explain your answer below.


```python
# Replace None with appropriate code
ans2 = None
### BEGIN SOLUTION
ans2 = True
### END SOLUTION
```


```python
# PUT ALL WORK FOR THE ABOVE QUESTION ABOVE THIS CELL
# THIS UNALTERABLE CELL CONTAINS HIDDEN TESTS

# ans2 should be True or False
assert type(ans2) == bool

### BEGIN HIDDEN TESTS

assert ans2 == True

### END HIDDEN TESTS
```

=== BEGIN MARK SCHEME ===

Yes, because the p-value for the TV predictor is very small (<0.001), that means that there is a statistically significant relationship between TV advertising spending and sales. 

Since the coefficient (0.0475) is positive, that means that more TV advertising is associated with greater sales. Every increase of 1000 dollars in TV advertising spending is associated with 0.0475x1,000,000 = 47,500 dollars of increased sales(!)

=== END MARK SCHEME ===

## Multiple Linear Regression

### 3) Create a multiple linear regression model (using either `ols()` or `sm.OLS()`).  Use `TV`, `radio`, and `newspaper` as independent variables, and `sales` as the dependent variable.

Produce the model summary table of this multiple linear regression model.

The cell below separates `X` from `y`; you can use these variables or just use `data` depending on which interface you are using.


```python
# Run this cell without changes

X = data.drop('sales', axis=1)
y = data['sales']
```


```python
# Replace None with appropriate code
model = None
results = None
### BEGIN SOLUTION

# Using ols
formula = 'sales ~ TV + radio + newspaper'
model = ols(formula = formula, data = data)
results = model.fit()

# Using OLS
X = sm.add_constant(X)
model = sm.OLS(y,X)
results = model.fit()

### END SOLUTION

results.summary()
```




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>          <td>sales</td>      <th>  R-squared:         </th> <td>   0.897</td>
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th> <td>   0.896</td>
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th> <td>   570.3</td>
</tr>
<tr>
  <th>Date:</th>             <td>Tue, 22 Sep 2020</td> <th>  Prob (F-statistic):</th> <td>1.58e-96</td>
</tr>
<tr>
  <th>Time:</th>                 <td>12:33:30</td>     <th>  Log-Likelihood:    </th> <td> -386.18</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td>   200</td>      <th>  AIC:               </th> <td>   780.4</td>
</tr>
<tr>
  <th>Df Residuals:</th>          <td>   196</td>      <th>  BIC:               </th> <td>   793.6</td>
</tr>
<tr>
  <th>Df Model:</th>              <td>     3</td>      <th>                     </th>     <td> </td>   
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>     <td> </td>   
</tr>
</table>
<table class="simpletable">
<tr>
      <td></td>         <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>const</th>     <td>    2.9389</td> <td>    0.312</td> <td>    9.422</td> <td> 0.000</td> <td>    2.324</td> <td>    3.554</td>
</tr>
<tr>
  <th>TV</th>        <td>    0.0458</td> <td>    0.001</td> <td>   32.809</td> <td> 0.000</td> <td>    0.043</td> <td>    0.049</td>
</tr>
<tr>
  <th>radio</th>     <td>    0.1885</td> <td>    0.009</td> <td>   21.893</td> <td> 0.000</td> <td>    0.172</td> <td>    0.206</td>
</tr>
<tr>
  <th>newspaper</th> <td>   -0.0010</td> <td>    0.006</td> <td>   -0.177</td> <td> 0.860</td> <td>   -0.013</td> <td>    0.011</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>60.414</td> <th>  Durbin-Watson:     </th> <td>   2.084</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th> <td> 0.000</td> <th>  Jarque-Bera (JB):  </th> <td> 151.241</td>
</tr>
<tr>
  <th>Skew:</th>          <td>-1.327</td> <th>  Prob(JB):          </th> <td>1.44e-33</td>
</tr>
<tr>
  <th>Kurtosis:</th>      <td> 6.332</td> <th>  Cond. No.          </th> <td>    454.</td>
</tr>
</table><br/><br/>Warnings:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.



### 4) The coefficient produced by this model for one of these features is not statistically significant at an alpha of 0.05.  Which feature is it, and how do you know?

Assign `ans4` to the name of the feature (you can just "hard-code" this, you don't need to extract it from the model), then explain your answer below.


```python
# Replace None with appropriate code
ans4 = None
### BEGIN SOLUTION
ans4 = "newspaper"
### END SOLUTION
```


```python
# PUT ALL WORK FOR THE ABOVE QUESTION ABOVE THIS CELL
# THIS UNALTERABLE CELL CONTAINS HIDDEN TESTS

# ans4 should be a string representing the name of a feature
assert type(ans4) == str

### BEGIN HIDDEN TESTS

assert ans4 == "newspaper"

### END HIDDEN TESTS
```

=== BEGIN MARK SCHEME ===

The `newspaper` feature has a p-value of 0.860, which is much larger than 0.05, so its coefficient is not significant

(Since the p-value is very small for TV and radio, they are statistically significant)

Alt: since the confidence interval generated at alpha=.05 does include 0 for newpapers, we can conclude it is 
not statistically significant

(Since the confidence interval generated at alpha=.05 doesn't include 0 for TV and radio, they can be considered
statistically significant)

=== END MARK SCHEME ===

### 5) The following code creates a correlation matrix for `X`

### Based on this correlation matrix only, would you recommend using `TV`, `radio`, and `newspaper` in the same multiple linear regression model?  How does this answer relate to your answer to Question 4?


```python
X.corr()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>const</th>
      <th>TV</th>
      <th>radio</th>
      <th>newspaper</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>const</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>TV</th>
      <td>NaN</td>
      <td>1.000000</td>
      <td>0.054809</td>
      <td>0.056648</td>
    </tr>
    <tr>
      <th>radio</th>
      <td>NaN</td>
      <td>0.054809</td>
      <td>1.000000</td>
      <td>0.354104</td>
    </tr>
    <tr>
      <th>newspaper</th>
      <td>NaN</td>
      <td>0.056648</td>
      <td>0.354104</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



=== BEGIN MARK SCHEME ===

The highest correlation is between radio and newspaper, about 0.35.

Multiple acceptable answers here:

a. It would probably not be a good idea to include both of these variables in a regression model because then there would be multicollinearity, and an assumption in interpreting the coefficients of a regression model is independence of the features.

b. A different rule of thumb is that 0.7 is the threshold for "high" correlation, so we should proceed with caution but go ahead and include it in the model

Going back to the answer for Question 4, it seems like there is multicollinearity between newspaper and radio. If we are interested in the "true" coefficients for newspaper and radio, we should only include one or the other in our model.

=== END MARK SCHEME ===


```python

```

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
### BEGIN SOLUTION


from test_scripts.test_class import Test
test = Test()

X.corr()

test.save()



### END SOLUTION
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>TV</th>
      <td>1.000000</td>
      <td>0.054809</td>
      <td>0.056648</td>
    </tr>
    <tr>
      <th>radio</th>
      <td>0.054809</td>
      <td>1.000000</td>
      <td>0.354104</td>
    </tr>
    <tr>
      <th>newspaper</th>
      <td>0.056648</td>
      <td>0.354104</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# PUT ALL WORK FOR THE ABOVE QUESTION ABOVE THIS CELL
# THIS UNALTERABLE CELL CONTAINS HIDDEN TESTS

### BEGIN HIDDEN TESTS

from test_scripts.test_class import Test
test = Test()

test.run_test()


### END HIDDEN TESTS
```

## 2) Based on this correlation matrix only, would you recommend using `TV`, `radio`, and `newspaper` in the same multiple linear regression model?

=== BEGIN MARK SCHEME ===

"""
The highest correlation is between radio and newspaper, about 0.35.

Multiple acceptable answers here:

a. It would probably not be a good idea to include both of these variables in a regression model 
because then there would be multicollinearity, and an assumption in interpreting the coefficients 
of a regression model is independence of the features.

b. A different rule of thumb is that 0.7 is the threshold for "high" correlation, so we should proceed with caution
but go ahead and include it in the model
"""

=== END MARK SCHEME ===

## 3) Create a multiple linear regression model (using either `ols()` or `sm.OLS()`).  Use `TV`, `radio`, and `newspaper` as independent variables, and `sales` as the dependent variable.

### Produce the model summary table of this multiple linear regression model.


```python
### BEGIN SOLUTION


from test_scripts.test_class import Test
test = Test()


# Using ols
formula = 'sales ~ TV + radio + newspaper'
model = ols(formula = formula, data = data).fit()
model.summary()

test.save()



### END SOLUTION
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
  <th>Date:</th>             <td>Thu, 27 Feb 2020</td> <th>  Prob (F-statistic):</th> <td>1.58e-96</td>
</tr>
<tr>
  <th>Time:</th>                 <td>10:41:54</td>     <th>  Log-Likelihood:    </th> <td> -386.18</td>
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
  <th>Intercept</th> <td>    2.9389</td> <td>    0.312</td> <td>    9.422</td> <td> 0.000</td> <td>    2.324</td> <td>    3.554</td>
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




```python
# PUT ALL WORK FOR THE ABOVE QUESTION ABOVE THIS CELL
# THIS UNALTERABLE CELL CONTAINS HIDDEN TESTS

### BEGIN HIDDEN TESTS

from test_scripts.test_class import Test
test = Test()

test.run_test()


### END HIDDEN TESTS
```


```python
### BEGIN SOLUTION


from test_scripts.test_class import Test
test = Test()


# Using OLS
X = sm.add_constant(X)
model = sm.OLS(y,X)
results = model.fit()
results.summary()

test.save()



### END SOLUTION
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
  <th>Date:</th>             <td>Thu, 27 Feb 2020</td> <th>  Prob (F-statistic):</th> <td>1.58e-96</td>
</tr>
<tr>
  <th>Time:</th>                 <td>10:42:08</td>     <th>  Log-Likelihood:    </th> <td> -386.18</td>
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




```python
# PUT ALL WORK FOR THE ABOVE QUESTION ABOVE THIS CELL
# THIS UNALTERABLE CELL CONTAINS HIDDEN TESTS

### BEGIN HIDDEN TESTS

from test_scripts.test_class import Test
test = Test()

test.run_test()


### END HIDDEN TESTS
```

## 4) For each coefficient:

### - Conclude whether it's statistically significant 

### - State how you came to that conclusion

## Interpret how these results relate to your answer for Question 2

=== BEGIN MARK SCHEME ===

"""
Since the p-value is very small for TV and radio, they are statistically significant at a standard alpha of 0.05.

However, newspaper has a p-value of 0.860, which is not statistically significant.

Alt: since the confidence interval generated at alpha=.05 doesn't include 0 for TV and radio, they can be considered
statistically significant 

However, since the confidence interval generated at alpha=.05 does include 0 for newpapers, we can conclude it is 
not statistically significant

Going back to the answer for Question 2, it seems like there is multicollinearity between newspaper and radio.
If we are interested in the "true" coefficients for newspaper and radio, we should only include one or the other
in our model.
"""

=== END MARK SCHEME ===

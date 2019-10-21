
## Linear Regression

Using the following FIFA soccer dataset, answer the questions below.


```python
import pandas as pd
```


```python
df = pd.read_csv('./data/fifa.csv')
df.head()
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
      <th>ID</th>
      <th>Name</th>
      <th>Age</th>
      <th>Photo</th>
      <th>Nationality</th>
      <th>Flag</th>
      <th>Overall</th>
      <th>Potential</th>
      <th>Club</th>
      <th>Club Logo</th>
      <th>...</th>
      <th>Composure</th>
      <th>Marking</th>
      <th>StandingTackle</th>
      <th>SlidingTackle</th>
      <th>GKDiving</th>
      <th>GKHandling</th>
      <th>GKKicking</th>
      <th>GKPositioning</th>
      <th>GKReflexes</th>
      <th>Release Clause</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>158023</td>
      <td>L. Messi</td>
      <td>31</td>
      <td>https://cdn.sofifa.org/players/4/19/158023.png</td>
      <td>Argentina</td>
      <td>https://cdn.sofifa.org/flags/52.png</td>
      <td>94</td>
      <td>94</td>
      <td>FC Barcelona</td>
      <td>https://cdn.sofifa.org/teams/2/light/241.png</td>
      <td>...</td>
      <td>96.0</td>
      <td>33.0</td>
      <td>28.0</td>
      <td>26.0</td>
      <td>6.0</td>
      <td>11.0</td>
      <td>15.0</td>
      <td>14.0</td>
      <td>8.0</td>
      <td>226500.0</td>
    </tr>
    <tr>
      <td>1</td>
      <td>20801</td>
      <td>Cristiano Ronaldo</td>
      <td>33</td>
      <td>https://cdn.sofifa.org/players/4/19/20801.png</td>
      <td>Portugal</td>
      <td>https://cdn.sofifa.org/flags/38.png</td>
      <td>94</td>
      <td>94</td>
      <td>Juventus</td>
      <td>https://cdn.sofifa.org/teams/2/light/45.png</td>
      <td>...</td>
      <td>95.0</td>
      <td>28.0</td>
      <td>31.0</td>
      <td>23.0</td>
      <td>7.0</td>
      <td>11.0</td>
      <td>15.0</td>
      <td>14.0</td>
      <td>11.0</td>
      <td>127100.0</td>
    </tr>
    <tr>
      <td>2</td>
      <td>190871</td>
      <td>Neymar Jr</td>
      <td>26</td>
      <td>https://cdn.sofifa.org/players/4/19/190871.png</td>
      <td>Brazil</td>
      <td>https://cdn.sofifa.org/flags/54.png</td>
      <td>92</td>
      <td>93</td>
      <td>Paris Saint-Germain</td>
      <td>https://cdn.sofifa.org/teams/2/light/73.png</td>
      <td>...</td>
      <td>94.0</td>
      <td>27.0</td>
      <td>24.0</td>
      <td>33.0</td>
      <td>9.0</td>
      <td>9.0</td>
      <td>15.0</td>
      <td>15.0</td>
      <td>11.0</td>
      <td>228100.0</td>
    </tr>
    <tr>
      <td>3</td>
      <td>193080</td>
      <td>De Gea</td>
      <td>27</td>
      <td>https://cdn.sofifa.org/players/4/19/193080.png</td>
      <td>Spain</td>
      <td>https://cdn.sofifa.org/flags/45.png</td>
      <td>91</td>
      <td>93</td>
      <td>Manchester United</td>
      <td>https://cdn.sofifa.org/teams/2/light/11.png</td>
      <td>...</td>
      <td>68.0</td>
      <td>15.0</td>
      <td>21.0</td>
      <td>13.0</td>
      <td>90.0</td>
      <td>85.0</td>
      <td>87.0</td>
      <td>88.0</td>
      <td>94.0</td>
      <td>138600.0</td>
    </tr>
    <tr>
      <td>4</td>
      <td>192985</td>
      <td>K. De Bruyne</td>
      <td>27</td>
      <td>https://cdn.sofifa.org/players/4/19/192985.png</td>
      <td>Belgium</td>
      <td>https://cdn.sofifa.org/flags/7.png</td>
      <td>91</td>
      <td>92</td>
      <td>Manchester City</td>
      <td>https://cdn.sofifa.org/teams/2/light/10.png</td>
      <td>...</td>
      <td>88.0</td>
      <td>68.0</td>
      <td>58.0</td>
      <td>51.0</td>
      <td>15.0</td>
      <td>13.0</td>
      <td>5.0</td>
      <td>10.0</td>
      <td>13.0</td>
      <td>196400.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 88 columns</p>
</div>



<b> 1) What are the covariance and correlation between "GKDiving" and "GKHandling"? </b>

a. What is the difference between covariance and correlation?  
b. What can you infer from the relationship between these variables?  
c. Would it be a good idea to include both of these in a regression model?


```python
#code here
print('Correlation:',np.corrcoef(df['GKDiving'],df['GKHandling'])[0][1])
print('Covariance:',np.cov(df['GKDiving'],df['GKHandling'])[0][1])
```

    Correlation: 0.9706399004266668
    Covariance: 294.83505727273473



```python
"""
a. Correlation is a standardized version of covariance. 
Covariance is on the scale of whatever values it is measuring, whereas correlation ranges from -1,1

b. These variables are strongly positively correlated! In general the higher better a player is at GKDiving, 
the better they are going to be at GKHandling

c. It would probably not be a good idea to include both of these variables in a regression model 
because then there would be high multicollinearity, which violates the independence assumption of linear regression.
"""
```

<b>2) Fit a linear regression using the `ols` module of statsmodels</b>

Let's see how well each players' in-game stats reflect their real-world monetary value as a player. We  will not be considering real-world factors for this model, just the variables listed below.

- y variable: Release Clause (the one in euros)
- x variables: 'Finishing', 'HeadingAccuracy', 'ShortPassing', 'Volleys', 'Dribbling', 'Curve', 'FKAccuracy', 'LongPassing', 'BallControl', 'Acceleration', 'SprintSpeed', 'Agility', 'Reactions', 'Balance', 'ShotPower', 'Jumping', 'Stamina', 'Strength', 'LongShots', 'Aggression','Interceptions', 'Positioning', 'Vision', 'Penalties', 'Composure','Marking', 'StandingTackle', 'SlidingTackle', 'GKDiving', 'GKHandling','GKKicking', 'GKPositioning', 'GKReflexes'

Once you have fit the linear regression, display the results (coefficient values, $R^2$, etc.). Displaying the results can be done with one method!


```python
# code here
import statsmodels.api as sm
from statsmodels.formula.api import ols

Y = df['Release Clause']
X = df[['Finishing', 'HeadingAccuracy', 'ShortPassing', 'Volleys', 'Dribbling', 'Curve', 'FKAccuracy', 'LongPassing', 'BallControl', 'Acceleration', 'SprintSpeed', 'Agility', 'Reactions', 'Balance', 'ShotPower', 'Jumping', 'Stamina', 'Strength', 'LongShots', 'Aggression','Interceptions', 'Positioning', 'Vision', 'Penalties', 'Composure','Marking', 'StandingTackle', 'SlidingTackle', 'GKDiving', 'GKHandling','GKKicking', 'GKPositioning', 'GKReflexes']]
X = sm.add_constant(X)
model = sm.OLS(Y,X)
results = model.fit()
results.summary()
```




<table class="simpletable">
<caption>OLS Regression Results</caption>
<tr>
  <th>Dep. Variable:</th>     <td>Release Clause</td>  <th>  R-squared:         </th>  <td>   0.141</td>  
</tr>
<tr>
  <th>Model:</th>                   <td>OLS</td>       <th>  Adj. R-squared:    </th>  <td>   0.140</td>  
</tr>
<tr>
  <th>Method:</th>             <td>Least Squares</td>  <th>  F-statistic:       </th>  <td>   82.81</td>  
</tr>
<tr>
  <th>Date:</th>             <td>Mon, 21 Oct 2019</td> <th>  Prob (F-statistic):</th>   <td>  0.00</td>   
</tr>
<tr>
  <th>Time:</th>                 <td>14:09:00</td>     <th>  Log-Likelihood:    </th> <td>-2.3220e+05</td>
</tr>
<tr>
  <th>No. Observations:</th>      <td> 16643</td>      <th>  AIC:               </th>  <td>4.645e+05</td> 
</tr>
<tr>
  <th>Df Residuals:</th>          <td> 16609</td>      <th>  BIC:               </th>  <td>4.647e+05</td> 
</tr>
<tr>
  <th>Df Model:</th>              <td>    33</td>      <th>                     </th>      <td> </td>     
</tr>
<tr>
  <th>Covariance Type:</th>      <td>nonrobust</td>    <th>                     </th>      <td> </td>     
</tr>
</table>
<table class="simpletable">
<tr>
         <td></td>            <th>coef</th>     <th>std err</th>      <th>t</th>      <th>P>|t|</th>  <th>[0.025</th>    <th>0.975]</th>  
</tr>
<tr>
  <th>const</th>           <td> 1.058e+06</td> <td> 2.92e+04</td> <td>   36.213</td> <td> 0.000</td> <td>    1e+06</td> <td> 1.12e+06</td>
</tr>
<tr>
  <th>Finishing</th>       <td> -186.6904</td> <td>  364.909</td> <td>   -0.512</td> <td> 0.609</td> <td> -901.952</td> <td>  528.571</td>
</tr>
<tr>
  <th>HeadingAccuracy</th> <td>-1721.8142</td> <td>  306.031</td> <td>   -5.626</td> <td> 0.000</td> <td>-2321.668</td> <td>-1121.960</td>
</tr>
<tr>
  <th>ShortPassing</th>    <td>-1537.6988</td> <td>  518.249</td> <td>   -2.967</td> <td> 0.003</td> <td>-2553.522</td> <td> -521.876</td>
</tr>
<tr>
  <th>Volleys</th>         <td>  524.5785</td> <td>  316.543</td> <td>    1.657</td> <td> 0.097</td> <td>  -95.879</td> <td> 1145.037</td>
</tr>
<tr>
  <th>Dribbling</th>       <td>-1816.1692</td> <td>  444.153</td> <td>   -4.089</td> <td> 0.000</td> <td>-2686.757</td> <td> -945.582</td>
</tr>
<tr>
  <th>Curve</th>           <td> -251.8955</td> <td>  302.036</td> <td>   -0.834</td> <td> 0.404</td> <td> -843.917</td> <td>  340.126</td>
</tr>
<tr>
  <th>FKAccuracy</th>      <td>   65.0183</td> <td>  275.312</td> <td>    0.236</td> <td> 0.813</td> <td> -474.624</td> <td>  604.660</td>
</tr>
<tr>
  <th>LongPassing</th>     <td>   54.3319</td> <td>  380.871</td> <td>    0.143</td> <td> 0.887</td> <td> -692.215</td> <td>  800.879</td>
</tr>
<tr>
  <th>BallControl</th>     <td>-2344.5367</td> <td>  557.525</td> <td>   -4.205</td> <td> 0.000</td> <td>-3437.345</td> <td>-1251.728</td>
</tr>
<tr>
  <th>Acceleration</th>    <td> -570.2972</td> <td>  427.689</td> <td>   -1.333</td> <td> 0.182</td> <td>-1408.614</td> <td>  268.019</td>
</tr>
<tr>
  <th>SprintSpeed</th>     <td>-1320.4425</td> <td>  395.892</td> <td>   -3.335</td> <td> 0.001</td> <td>-2096.434</td> <td> -544.451</td>
</tr>
<tr>
  <th>Agility</th>         <td> 1269.9876</td> <td>  317.384</td> <td>    4.001</td> <td> 0.000</td> <td>  647.882</td> <td> 1892.094</td>
</tr>
<tr>
  <th>Reactions</th>       <td>-6076.8710</td> <td>  420.977</td> <td>  -14.435</td> <td> 0.000</td> <td>-6902.031</td> <td>-5251.711</td>
</tr>
<tr>
  <th>Balance</th>         <td>  831.8455</td> <td>  287.459</td> <td>    2.894</td> <td> 0.004</td> <td>  268.394</td> <td> 1395.296</td>
</tr>
<tr>
  <th>ShotPower</th>       <td>-1234.1000</td> <td>  322.514</td> <td>   -3.826</td> <td> 0.000</td> <td>-1866.262</td> <td> -601.938</td>
</tr>
<tr>
  <th>Jumping</th>         <td>  -91.6105</td> <td>  225.000</td> <td>   -0.407</td> <td> 0.684</td> <td> -532.634</td> <td>  349.413</td>
</tr>
<tr>
  <th>Stamina</th>         <td>  771.8079</td> <td>  261.189</td> <td>    2.955</td> <td> 0.003</td> <td>  259.849</td> <td> 1283.767</td>
</tr>
<tr>
  <th>Strength</th>        <td> 1179.3792</td> <td>  272.289</td> <td>    4.331</td> <td> 0.000</td> <td>  645.663</td> <td> 1713.095</td>
</tr>
<tr>
  <th>LongShots</th>       <td>  662.1502</td> <td>  343.207</td> <td>    1.929</td> <td> 0.054</td> <td>  -10.572</td> <td> 1334.872</td>
</tr>
<tr>
  <th>Aggression</th>      <td> -229.7008</td> <td>  241.165</td> <td>   -0.952</td> <td> 0.341</td> <td> -702.410</td> <td>  243.008</td>
</tr>
<tr>
  <th>Interceptions</th>   <td>  189.3008</td> <td>  349.249</td> <td>    0.542</td> <td> 0.588</td> <td> -495.264</td> <td>  873.866</td>
</tr>
<tr>
  <th>Positioning</th>     <td>  753.9676</td> <td>  332.317</td> <td>    2.269</td> <td> 0.023</td> <td>  102.590</td> <td> 1405.345</td>
</tr>
<tr>
  <th>Vision</th>          <td> -512.8898</td> <td>  314.196</td> <td>   -1.632</td> <td> 0.103</td> <td>-1128.747</td> <td>  102.967</td>
</tr>
<tr>
  <th>Penalties</th>       <td>  599.0759</td> <td>  298.530</td> <td>    2.007</td> <td> 0.045</td> <td>   13.925</td> <td> 1184.227</td>
</tr>
<tr>
  <th>Composure</th>       <td>-1675.2161</td> <td>  339.233</td> <td>   -4.938</td> <td> 0.000</td> <td>-2340.149</td> <td>-1010.283</td>
</tr>
<tr>
  <th>Marking</th>         <td>   61.3220</td> <td>  280.417</td> <td>    0.219</td> <td> 0.827</td> <td> -488.325</td> <td>  610.969</td>
</tr>
<tr>
  <th>StandingTackle</th>  <td> -256.3604</td> <td>  519.643</td> <td>   -0.493</td> <td> 0.622</td> <td>-1274.915</td> <td>  762.195</td>
</tr>
<tr>
  <th>SlidingTackle</th>   <td>  278.6254</td> <td>  481.464</td> <td>    0.579</td> <td> 0.563</td> <td> -665.096</td> <td> 1222.347</td>
</tr>
<tr>
  <th>GKDiving</th>        <td>-2157.8749</td> <td>  648.490</td> <td>   -3.328</td> <td> 0.001</td> <td>-3428.984</td> <td> -886.766</td>
</tr>
<tr>
  <th>GKHandling</th>      <td> -923.1711</td> <td>  655.277</td> <td>   -1.409</td> <td> 0.159</td> <td>-2207.583</td> <td>  361.241</td>
</tr>
<tr>
  <th>GKKicking</th>       <td> -924.0726</td> <td>  603.179</td> <td>   -1.532</td> <td> 0.126</td> <td>-2106.367</td> <td>  258.222</td>
</tr>
<tr>
  <th>GKPositioning</th>   <td> -363.0774</td> <td>  641.463</td> <td>   -0.566</td> <td> 0.571</td> <td>-1620.412</td> <td>  894.258</td>
</tr>
<tr>
  <th>GKReflexes</th>      <td> -507.0585</td> <td>  644.356</td> <td>   -0.787</td> <td> 0.431</td> <td>-1770.065</td> <td>  755.948</td>
</tr>
</table>
<table class="simpletable">
<tr>
  <th>Omnibus:</th>       <td>2361.056</td> <th>  Durbin-Watson:     </th> <td>   1.535</td>
</tr>
<tr>
  <th>Prob(Omnibus):</th>  <td> 0.000</td>  <th>  Jarque-Bera (JB):  </th> <td>3512.259</td>
</tr>
<tr>
  <th>Skew:</th>           <td> 1.116</td>  <th>  Prob(JB):          </th> <td>    0.00</td>
</tr>
<tr>
  <th>Kurtosis:</th>       <td> 3.286</td>  <th>  Cond. No.          </th> <td>4.05e+03</td>
</tr>
</table><br/><br/>Warnings:<br/>[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.<br/>[2] The condition number is large, 4.05e+03. This might indicate that there are<br/>strong multicollinearity or other numerical problems.



<b> 3) Interpret the results of the regression. 

Two players have the following stats: 

1) Finishing : 1, Heading Accuracy : 10, ShortPassing : 5

2) Finishing : 1, Heading Accuracy :  8, ShortPassing : 5

Assume all the remaining stats are the same for both players. By how much can we expect the Release Clause of each player to be different? Explain how you obtained your calculation. </b>


```python
# Your written answer here
"""
Player 1's release clause will be $3442 less than Player 2's. 
This was calculated using the coefficient of for Heading Accuracy and multiplying by a change of 2 units difference.
"""
```

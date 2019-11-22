
## Linear Regression

Using the following FIFA soccer dataset, answer the questions below.


```python
import pandas as pd
```


```python
df = pd.read_csv('./data/fifa.csv')
df.head()
```

<b> 1) What are the covariance and correlation between "GKDiving" and "GKHandling"? </b>

a. What is the difference between covariance and correlation?  
b. What can you infer from the relationship between these variables?  


```python
print('Correlation:',np.corrcoef(df['GKDiving'],df['GKHandling'])[0][1])
print('Covariance:',np.cov(df['GKDiving'],df['GKHandling'])[0][1])
```


```python
"""
a. Correlation is a standardized version of covariance. 
Covariance is on the scale of whatever values it is measuring, whereas correlation ranges from -1,1

b. These variables are strongly positively correlated! In general the higher better a player is at GKDiving, 
the better they are going to be at GKHandling
"""
```

<b>2) Fit a linear regression using the `ols` module of statsmodels</b>

Let's see how well each players' in-game stats reflect their real-world monetary value as a player. We  will not be considering real-world factors for this model, just the variables listed below.

- y variable: Release Clause (the one in euros)
- x variables: 'Finishing', 'HeadingAccuracy', 'ShortPassing', 'Volleys', 'Dribbling', 'Curve', 'FKAccuracy', 'LongPassing', 'BallControl', 'Acceleration', 'SprintSpeed', 'Agility', 'Reactions', 'Balance', 'ShotPower', 'Jumping', 'Stamina', 'Strength', 'LongShots', 'Aggression','Interceptions', 'Positioning', 'Vision', 'Penalties', 'Composure','Marking', 'StandingTackle', 'SlidingTackle', 'GKDiving', 'GKHandling','GKKicking', 'GKPositioning', 'GKReflexes'

Once you have fit the linear regression, display the results (coefficient values, $R^2$, etc.). Displaying the results can be done with one method!


```python
import statsmodels.api as sm
from statsmodels.formula.api import ols

Y = df['Release Clause']
X = df[['Finishing', 'HeadingAccuracy', 'ShortPassing', 'Volleys', 'Dribbling', 'Curve', 'FKAccuracy', 'LongPassing', 'BallControl', 'Acceleration', 'SprintSpeed', 'Agility', 'Reactions', 'Balance', 'ShotPower', 'Jumping', 'Stamina', 'Strength', 'LongShots', 'Aggression','Interceptions', 'Positioning', 'Vision', 'Penalties', 'Composure','Marking', 'StandingTackle', 'SlidingTackle', 'GKDiving', 'GKHandling','GKKicking', 'GKPositioning', 'GKReflexes']]
```


```python
X = sm.add_constant(X)
model = sm.OLS(Y,X)
results = model.fit()
results.summary()
```

<b> 3) Interpret the results of the regression. 

Two players have the following stats: 

1) Finishing : 1, Heading Accuracy : 10, ShortPassing : 5

2) Finishing : 1, Heading Accuracy :  8, ShortPassing : 5

Assume all the remaining stats are the same for both players. By how much can we expect the Release Clause of each player to be different? Explain how you obtained your calculation. </b>


```python
"""
Player 1's release clause will be $3442 less than Player 2's. 
This was calculated using the coefficient of for Heading Accuracy and multiplying by a change of 2 units difference.
"""
```

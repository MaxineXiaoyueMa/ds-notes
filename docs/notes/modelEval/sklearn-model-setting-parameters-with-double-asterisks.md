Title: Machine Learning Model Parameters Setting Shortcut with Double Asterisks

# Machine Learning Model Parameters Setting Shortcut with Double Asterisks
> Quick way to pass down machine learning model parameters: `model(**params)`


```python
from sklearn.ensemble import RandomForestRegressor
```


```python
params = {'n_estimators': 100,
          'max_depth': 4}
```

## Pass down parameters with **


```python
model = RandomForestRegressor(**params)
model
```




    RandomForestRegressor(bootstrap=True, criterion='mse', max_depth=4,
               max_features='auto', max_leaf_nodes=None,
               min_impurity_decrease=0.0, min_impurity_split=None,
               min_samples_leaf=1, min_samples_split=2,
               min_weight_fraction_leaf=0.0, n_estimators=100, n_jobs=1,
               oob_score=False, random_state=None, verbose=0, warm_start=False)



## Won't work without asterisks


```python
model = RandomForestRegressor(params)
model
```




    RandomForestRegressor(bootstrap=True, criterion='mse', max_depth=None,
               max_features='auto', max_leaf_nodes=None,
               min_impurity_decrease=0.0, min_impurity_split=None,
               min_samples_leaf=1, min_samples_split=2,
               min_weight_fraction_leaf=0.0,
               n_estimators={'n_estimators': 100, 'max_depth': 4}, n_jobs=1,
               oob_score=False, random_state=None, verbose=0, warm_start=False)

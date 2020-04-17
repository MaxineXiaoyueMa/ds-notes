
# Use cPickle or pickle to Save Trained Model


```python
try:
    import cPickle as pickle
except ImportError:
    import pickle

import numpy as np
import pandas as pd
from sklearn.datasets import load_diabetes
from sklearn.svm import SVR
from sklearn.model_selection import train_test_split, GridSearchCV
from sklearn.linear_model import LinearRegression

```

## Load Data


```python
# load datatset
X, y = load_diabetes(return_X_y = True)
print X.shape, y.shape
```

    (442, 10) (442,)



```python
# train_test splie
X_train, X_test, y_train, y_test = train_test_split(X,y, shuffle = True)
print X_train.shape, y_train.shape
```

    (331, 10) (331,)


## Train model


```python
# train linear model on train set and predit on test set
model = LinearRegression()
fitted_model = model.fit(X_train, y_train)
print "The fitted model predict on the test set with RSqured: \n"
print fitted_model.score(X_test, y_test)
```

    The fitted model predict on the test set with RSqured:

    0.542043958777


## Save model with pickle.dump


```python
# use pickle to save the fitted model
with open ('fitted_model.pkl', 'wb') as f:
    pickle.dump(fitted_model, f)
```

## Load saved model with pickle.load


```python
# use pickle to load the fitted model
with open ('fitted_model.pkl', 'rb') as f:
    mdl = pickle.load(f)
```


```python
# check to see the model is indeed the one we saved
print mdl.score(X_test, y_test)
```

    0.542043958777

title: sklearn-cross-validation-methods-and-comparison
date: 2017-10-26

# Sklearn Cross Validation Methods and Comparison

## Overview

| Method     | stratified | shuffle   | n_splits | test_size | train_size |
| :------- | :----: | :---: | :---: |:---:|:---:|
| KFold | - |`shuffle = True`|**Y**|-|-|
| StratifiedKFold | **Y**   |  `shuffle = True`  | **Y**|-|-|
| ShuffleSplit     |   -|  **Y**  |**Y**|**Y**|**Y**|
| StratifiedShuffleSplit| **Y**|**Y**|**Y**|**Y**|**Y**|
| train_test_split | `stratify = None` | `shuffle = True` |-|**Y**|**Y**|

## Create Toy Dataset
> indices [0,1,2] belong to class "A"


```python
# toy X, y (class '1': 30%)
X = range(10)
y = list('A' * 3 + 'B' * 7)
print "X: ", X
print "y: ", y
```

    X:  [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    y:  ['A', 'A', 'A', 'B', 'B', 'B', 'B', 'B', 'B', 'B']



```python
# helper function to print train/test index:
def print_index_for_folds (cv, X, y = None):
    if y == None:
        for train_ix, test_ix in cv.split(X):
            print "Train_ix:", train_ix, " Test_ix:", test_ix
    else:
        for train_ix, test_ix in cv.split(X,y):
            print "Train_ix:", train_ix, " Test_ix:", test_ix
```


```python
from sklearn.model_selection import KFold, StratifiedKFold, ShuffleSplit, StratifiedShuffleSplit, train_test_split
```

## KFold


```python
# KFold
kf = KFold(n_splits=3, random_state=1)
print_index_for_folds(kf, X)
```
    Train_ix: [4 5 6 7 8 9]  Test_ix: [0 1 2 3]
    Train_ix: [0 1 2 3 7 8 9]  Test_ix: [4 5 6]
    Train_ix: [0 1 2 3 4 5 6]  Test_ix: [7 8 9]



```python
# KFold(shuffle = True)
kf = KFold(n_splits = 3, shuffle = True, random_state = 1)
print_index_for_folds(kf, X)
```
    Train_ix: [0 1 3 5 7 8]  Test_ix: [2 4 6 9]
    Train_ix: [2 4 5 6 7 8 9]  Test_ix: [0 1 3]
    Train_ix: [0 1 2 3 4 6 9]  Test_ix: [5 7 8]


## StratifiedKFold


```python
# notice the 30% weight for class '1' in y (i.e., index 0, 1, 2)
# is preserved for both test and train folds through strtification
s_kf = StratifiedKFold(n_splits=3, random_state= 1)
print_index_for_folds(s_kf, X, y)
```
    Train_ix: [1 2 6 7 8 9]  Test_ix: [0 3 4 5]
    Train_ix: [0 2 3 4 5 8 9]  Test_ix: [1 6 7]
    Train_ix: [0 1 3 4 5 6 7]  Test_ix: [2 8 9]



```python
s_kf = StratifiedKFold(n_splits=3, shuffle=True, random_state= 1)
print_index_for_folds(s_kf, X, y)
```
    Train_ix: [1 2 3 6 7 8]  Test_ix: [0 4 5 9]
    Train_ix: [0 1 4 5 6 8 9]  Test_ix: [2 3 7]
    Train_ix: [0 2 3 4 5 7 9]  Test_ix: [1 6 8]


## ShuffleSplit


```python
ss = ShuffleSplit(n_splits=3, test_size=0.3, random_state=1)
print_index_for_folds(ss, X)
```
    Train_ix: [4 0 3 1 7 8 5]  Test_ix: [2 9 6]
    Train_ix: [0 8 4 2 1 6 7]  Test_ix: [9 5 3]
    Train_ix: [9 0 6 1 7 4 2]  Test_ix: [8 3 5]


```python
ss = ShuffleSplit(n_splits=3, test_size=0.3, train_size = 0.6, random_state=1)
print_index_for_folds(ss, X)
```
    Train_ix: [4 0 3 1 7 8]  Test_ix: [2 9 6]
    Train_ix: [0 8 4 2 1 6]  Test_ix: [9 5 3]
    Train_ix: [9 0 6 1 7 4]  Test_ix: [8 3 5]


## StratifiedShuffleSplit
= StratifiedKFold + ShuffleSplit


```python
# notice the distribution of index 0, 1, 2 preserve the 30% class weight in y
s_ss = StratifiedShuffleSplit(n_splits=3, test_size=0.3, train_size=0.6, random_state=1)
print_index_for_folds(s_ss, X, y)
```

    Train_ix: [8 5 9 2 6 0]  Test_ix: [3 1 4]
    Train_ix: [8 3 1 0 4 6]  Test_ix: [9 2 7]
    Train_ix: [5 6 7 3 0 1]  Test_ix: [2 8 9]


## train_test_Split

**Useful one line wrapper for trian/test split:**
1. shuffle by default,
2. NOT stratify by default,
3. NO iterations.


```python
X_train, X_test = train_test_split(X, random_state = 1)
print "Train: ", X_train, " Test: ", X_test
```

    Train:  [4, 0, 3, 1, 7, 8, 5]  Test:  [2, 9, 6]



```python
X_train, X_test, y_train, y_test = train_test_split(X, y, random_state = 9)
print "X_train: ", X_train, " X_test: ", X_test
print "y_train: ", y_train, " y_test: ", y_test
```

    X_train:  [2, 1, 9, 3, 0, 6, 5]  X_test:  [8, 4, 7]
    y_train:  ['A', 'A', 'B', 'B', 'A', 'B', 'B']  y_test:  ['B', 'B', 'B']



```python
X_train, X_test, y_train, y_test = train_test_split(X, y, stratify = y, random_state = 9)
print "X_train: ", X_train, " X_test: ", X_test
print "y_train: ", y_train, " y_test: ", y_test
```

    X_train:  [6, 3, 7, 1, 4, 5, 0]  X_test:  [9, 8, 2]
    y_train:  ['B', 'B', 'B', 'A', 'B', 'B', 'A']  y_test:  ['B', 'B', 'A']


## Reference

* [sklearn.model_selection](http://scikit-learn.org/stable/modules/classes.html#module-sklearn.model_selection)

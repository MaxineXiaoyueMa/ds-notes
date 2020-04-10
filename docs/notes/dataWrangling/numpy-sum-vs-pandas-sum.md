
# numpy sum vs. pandas sum
> `axis ` parameter specifies the dimension:
*  that collapses due to the sum operation;
*  that its index is used to to perform the sum.

**Memorize: column sum (axis = 0), row sum(axis = 1)**


```python
import numpy as np
import pandas as pd
```


```python
np.random.seed(0)
X = np.random.randint(1,5, size = (3,4) )
print "X shape: ", X.shape, 'or 3 rows and 4 columns\n'
print X
```

    X shape:  (3, 4) or 3 rows and 4 columns

    [[1 4 2 1]
     [4 4 4 4]
     [2 4 2 3]]


## np.sum Column Sum


```python
X_colsum = np.sum(X, axis=0)
print "Column sum sums each column, thus collapsing the row dimension which is represted with axis = 0. "
print "Notice the row number 3 is gone.\n"
print "X_colsum shape: ", X_colsum.shape, "\n"
print X_colsum
```

    Column sum sums each column, thus collapsing the row dimension which is represted as axis = 0.
    Notice the row number 3 is gone.

    X_colsum shape:  (4,)

    [ 7 12  8  8]


## np.sum Row Sum


```python
X_rowsum = np.sum(X, axis=1)
print "Row sum sums up each row, thus collapsing the column dimension which is represted with axis = 1. "
print "Notice the column number 4 is gone.\n"
print "X_rowsum shape: ", X_rowsum.shape, "\n"
print X_rowsum
```

    Row sum sums up each row, thus collapsing the column dimension which is represted with axis = 1.
    Notice the row number 4 is gone.

    X_rowsum shape:  (3,)

    [ 8 16 11]



```python
X_df = pd.DataFrame(X)
X_df.shape
```

    (3, 4)



## pandas sum Column Sum


```python
X_df_colsum = X_df.sum(axis = 0)
print "Column sum sums up each column, which is the same as saying summing over the row index,"
print "thus collapsing the row dimension or axis = 0. Notice the row number 3 is gone.\n"
print "Colum sum shape: ", X_df_colsum.shape, "\n"
print X_df_colsum
```

    Column sum sums up each column, which is the same as saying summing over the row index,
    thus collapsing the row dimension or axis = 0. Notice the row number 3 is gone.

    Colum sum shape:  (4,)

    0     7
    1    12
    2     8
    3     8
    dtype: int64


## pandas sum Row Sum


```python
X_df_rowsum = X_df.sum(axis = 1)
print "Row sum sums up each row, which is the same as saying summing over the column index, "
print "thus collapsing the column dimension or axis = 1. Notice the column number 4 is gone.\n"
print "Row sum shape: ", X_df_rowsum.shape, "\n"
print X_df_rowsum
```

    Row sum sums up each row, which is the same as saying summing over the column index,
    thus collapsing the column dimension or axis = 1. Notice the column number 4 is gone.

    Row sum shape:  (3,)

    0     8
    1    16
    2    11
    dtype: int64

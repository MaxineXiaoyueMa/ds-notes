
Sample file structure:

- folder/folder1/**script.py**
- folder/folder1/**data1.csv**
- folder/folder1/**data/data2.csv**
- folder/**data3.csv**
- folder/folder2/**data4.csv**

Suppose the script or notebook is **script.py**, pandas uses **folder1** as its starting point to go up (**'..'**) or down (**'/'**) to searh for data files.


```python
import pandas as pd
```


```python
# reach data1
pd.read_csv('data1.csv')
```


```python
# reach data2
pd.read_csv('data/data2.csv')
```


```python
# reach data3
pd.read_csv('../data3.csv')
```


```python
# reach data4
pd.read_csv('../folder2/data4.csv')
```

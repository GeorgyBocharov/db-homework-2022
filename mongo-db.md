```python
import pymongo
import numpy as np
from sklearn import datasets
import pandas as pd
import time
```


```python
myclient = pymongo.MongoClient("mongodb://george:mongo@localhost:27017/")
```


```python
print(myclient.list_database_names())
```

    ['admin', 'config', 'iris', 'local']
    


```python
iris_data = datasets.load_iris()
df = pd.DataFrame(data=iris_data.data, columns=iris_data.feature_names)
df = df.rename(columns={"sepal length (cm)": "sepal_length", "sepal width (cm)": " sepal_width", "petal length (cm)": "petal_length", "petal width (cm)": "petal_width"})
data_dict = df.to_dict('records')
```


```python
mydb = myclient["iris"]
mycol = mydb["flowers_info"]
```


```python
x = mycol.insert_many(data_dict)
```


```python
sepal_length_greater = { "sepal_length": { "$gt": 5 } }
sepals_more_5 = mycol.find(sepal_length_greater)
```


```python
start = time.time()
sepals_more_5 = mycol.find(sepal_length_greater)
end = time.time()
print("without indicies:")
print(end - start)
```

    without indicies:
    0.00043582916259765625
    


```python
mycol.create_index([("sepal_length", pymongo.ASCENDING)])
```


```python
start = time.time()
sepals_more_5 = mycol.find(sepal_length_greater)
end = time.time()
print("with indicies:")
print(end - start)
```

    with indicies:
    0.0003418922424316406
    

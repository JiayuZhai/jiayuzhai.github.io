---
layout: post
title: Dataframe Operators
---
Dateframe operators for both pd.dataframe and pyspark.dataframe

## Dataframe operator cheat sheet for pd.dataframe and pyspark.dataframe

### sort  
pd.dataframe
```python
df.sort_values("col")
```
pyspark.dataframe
```python
df.sort(desc(col))
```


### tocsv
pd.dataframe
```python
df.to_csv(file_name)
```
pyspark.dataframe
```python
df.repartition(1).write.mode('overwrite').option("header","true").csv(file_name)
```

### tojson  
pd.dataframe
```python
df.to_json(file_name,orient='records',lines=True)
```
pyspark.dataframe
```python
df.repartition(1).write.mode('overwrite').option("header","true").json(file_name)
```

### column_rename
pd.dataframe
```python
df.rename('old','new')
```

pyspark.dataframe
```python
df.withColumnRenamed('old','new')
```



### readcsv
pd.dataframe
```python
pd.read_csv('file',sep=',')
```

pyspark.dataframe
```python
spark.read.csv('file',sep=',')
```



### readjson
pd.dataframe
```python
pd.read_json('file',lines=True)
```

pyspark.dataframe
```python
spark.read.json('file',lines=True)
```



### num_row
pd.dataframe
```python
df.shape[0]
```

pyspark.dataframe
```python
df.count()
```



### num_col
pd.dataframe
```python
df.shape[1]
```

pyspark.dataframe
```python
len(df.columns)
```



### string not contain
pd.dataframe
```python
df[~df['col'].contains('pattern')]
```

pyspark.dataframe
```python
df.filter("col not like '%pattern%'")
```



### not in 
pd.dataframe
```python
df[df['col'].isin([a,b,c])]
```

pyspark.dataframe
```python
from pyspark.sql.function import col; df.filter(~col('bar').isin(['a','b']))
```



### new col
pd.dataframe
```python
df['new_col']= 'abc'
```

pyspark.dataframe
```python
from pyspark.sql.function import lit; df.withColumn('new_col',lit('abc'))
```



### multi select
pd.dataframe
```python
df[['a','b']] 
```

pyspark.dataframe
```python
df[['a','b']]
```



### distinct count of a column
pd.dataframe
```python
df['col'].nunique()
```

pyspark.dataframe
```python
df.select('col').distinct()
```



### set ops-subtract
pyspark.dataframe
```python
df1.select("sentence").subtract(df2.select("sentence")).distinct()
```



### set ops-intersect
pyspark.dataframe
```python
df1.select("sentence").intersect(df2.select("sentence")).distinct()
```



### set ops-union
pyspark.dataframe
```python
df1.select("sentence").union(df2.select("sentence")).distinct()
```



### str_bool to int
pd.dataframe
```python
(df['col'] == 'TRUE').astype('i2')
```

pyspark.dataframe
```python
(df['col'] == 'TRUE').astype(int)
```



### time difference
pyspark.dataframe
```python
spark.sql('SELECT datediff(all.timestamp2,all.timestamp1)*24*60*60 + (hour(all.timestamp2)- hour(all.timestamp1))*60*60 + (minute(all.timestamp2) - minute(all.timestamp1))*60 + (second(all.timestamp2) - second(all.timestamp1)) as tol_time_diff from df')
```

### groupby+sum(str)
pd.dataframe
```python
def test_sum(series):
	l = series.values.tolist()
	new_l = [en for en in l if en!='']
	return ';'.join(new_l)
target = x.groupby('uid').agg({'str':test_sum})
```

### column to list
pd.dataframe
```python
df['col'].tolist()
```


---
layout: post
title: Dataframe Operators
---

## Dataframe operator cheat sheet for pd.dataframe and pyspark.dataframe

|functions  |  pd.dataframe | pyspark.dataframe  |
|:------------:|---|---|
|sort  | ```df.sort_values("col")```  | ```df.sort(desc(col))```  | 
|tocsv  | ```df.to_csv()```  | ```df.repartition(1).write.csv()```  |
|tojson  | ```df.to_json()```  | ```df.repartition(1).write.json()```  |
|column_rename|```df.rename('old','new')```| ```df.withColumnRenamed('old','new')```|
|readcsv|```pd.read_csv('file',sep=',')```|```spark.read.csv('file',sep=',')```|
|readjson|```pd.read_json('file',lines=True)```|```spark.read.json('file',lines=True)```|
|num_row|```df.shape[0]```|```df.count()```|
|num_col|```df.shape[1]```|```len(df.columns)```|
|string not contain|```df[~df['col'].contains('pattern')]```|```df.filter("col not like '%pattern%'")```|
|not in |```df[df['col'].isin([a,b,c])]```|```from pyspark.sql.function import col; df.filter(~col('bar').isin(['a','b']))```|
|new col|```df['new_col']= 'abc'```|```from pyspark.sql.function import lit; df.withColumn('new_col',lit('abc'))```|
|multi select|```df[['a','b']] ```|```df[['a','b']]```|
|distinct count of a column|`df['col'].nunique()`|`df.select('col').distinct()`|
|set ops-subtract||`df1.select("sentence").subtract(df2.select("sentence")).distinct()`|
|set ops-intersect||`df1.select("sentence").intersect(df2.select("sentence"))`|
|set ops-union||`df1.select("sentence").union(df2.select("sentence")).distinct()`|
|str_bool to int|`(df['col'] == 'TRUE').astype('i2')`|`(df['col'] == 'TRUE').astype(int)`|
|time difference||`spark.sql('SELECT datediff(all.timestamp2,all.timestamp1)*24*60*60 + (hour(all.timestamp2)- hour(all.timestamp1))*60*60 + (minute(all.timestamp2) - minute(all.timestamp1))*60 + (second(all.timestamp2) - second(all.timestamp1)) as tol_time_diff from df')`|
---
layout: post
title: Dataframe Operators
---

## Dataframe operator cheat sheet for pd.dataframe and pyspark.dataframe

|functions  |  pd.dataframe | pyspark.dataframe  |
|:---:|---|---|
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

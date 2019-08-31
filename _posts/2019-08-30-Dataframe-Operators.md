---
layout: post
title: Dataframe Operators
---

## Dataframe operator cheat sheet for pd.dataframe and pyspark.dataframe


|functions  |  pd.dataframe | pyspark.dataframe  |
|---|---|---|
|sort  | ```df.sort_values("col")```  | ```pythondf.sort(desc(col))```  | 
|tocsv  | ```df.to_csv()```  | ```df.repartition(1).write.csv()```  |
|tojson  | ```df.to_json()```  | ```df.repartition(1).write.json()```  |
|column_rename|```df.rename('old','new')```| ```df.withColumnRenamed('old','new')```|
|readcsv|```spark.read.csv('file',sep=',')```|```pd.read_csv('file',sep=',')```|
|readjson|```spark.read.json('file',lines=True)```|```pd.read_json('file',lines=True)```|
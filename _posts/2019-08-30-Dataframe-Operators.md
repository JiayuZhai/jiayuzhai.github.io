---
layout: post
title: Dataframe Operators
---

## Dataframe operator cheat sheet for pd.dataframe and pyspark.dataframe

<table>
   <tr>
      <td>functions</td>
      <td>pd.dataframe</td>
      <td>pyspark.dataframe</td>
   </tr>
   <tr>
      <td>sort</td>
      <td>df.sort_values("col")</td>
      <td>pythondf.sort(desc(col))</td>
   </tr>
   <tr>
      <td>tocsv</td>
      <td>df.to_csv()</td>
      <td>df.repartition(1).write.csv()</td>
   </tr>
   <tr>
      <td>tojson</td>
      <td>df.to_json()</td>
      <td>df.repartition(1).write.json()</td>
   </tr>
   <tr>
      <td>column_rename</td>
      <td>df.rename('old','new')</td>
      <td>df.withColumnRenamed('old','new')</td>
   </tr>
   <tr>
      <td>readcsv</td>
      <td>spark.read.csv('file',sep=',')</td>
      <td>pd.read_csv('file',sep=',')</td>
   </tr>
   <tr>
      <td>readjson</td>
      <td>spark.read.json('file',lines=True)</td>
      <td>pd.read_json('file',lines=True)</td>
   </tr>
</table>
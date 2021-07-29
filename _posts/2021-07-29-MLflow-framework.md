---
layout: post
title: MLflow framework
---
最近做了MLflow [https://mlflow.org/docs/latest/index.html]和公司内部有监督建模流程的集成工作。记录一些关键信息。

## MLflow simple use
```python
import mlflow

with mlflow.start_run() as run:
    # Some Training
```

## Get or Create Experiment
```python
mlflow.set_experiment(EXPERIMENT_NAME)
experiment_id = mlflow.get_experiment_by_name(EXPERIMENT_NAME).experiment_id
```

## Download artifact
```python
import json
client = MlflowClient()
previous_run_id = "dbc4eab36cba4b97b1b194fa555c7d94"
_ = client.download_artifacts(previous_run_id, "data/dataset_loc_map.json",".")
dataset_loc_map = json.load(open("data/dataset_loc_map.json"))
```

## Log after run
```python
client = MlflowClient()
client.log_metric(run.info.run_id, "test_metric",0.5)
client.log_param(run.info.run_id, "test_param",0.5)
```


## Start tracking server
`127.0.0.1`只有localhost访问。`0.0.0.0`可以用本机ip访问，然后可以做nodeport with k8s。
```shell script
mlflow server --backend-store-uri sqlite:////Users/jiayuzhai/Documents/Trial/sml_project/mlflow2.db --default-artifact-root s3://some-bucket/mlflow/mlruns  --host 127.0.0.1
```

## Log model
```python
mlflow.xgboost.log_model(bst,artifact_path="model",registered_model_name="SML model A")
```


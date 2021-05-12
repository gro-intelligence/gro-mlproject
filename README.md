# gro-mlproject
The goal of this project is to demo what we want to achieve with this POC.

## Problem description
We want to run thousands of experimentations to tweak a parameter - alpha. To run one experiment locally, you can run in command line
```
python mlflowtest/train.py 0.5
``` 
, which is not scalable if we want to run the training script with 1000 different values for alpha. 

Alternatively, we can send the training script to Databricks, with something like the following
```
mlflow run ../gro-mlproject -b databricks --backend-config cluster-spec.json --experiment-id 4069866474349730 -P alpha=0.5
```
In order for Databricks to to run the script, one needs to specify the enviroment, using one of the three options [here](https://www.mlflow.org/docs/latest/projects.html#project-environments). Specifically,
1. conda: mlflow run works when we specify conda_env in MLproject. However, it is not a feasible option because our model requires more complicated dependencies than a conda.yaml file can hold. For example, we might require certain system packages to be installed. 
2. docker container: mlflow run does not work with the current setup. Got the following error message ```ERROR mlflow.cli: === Running docker-based projects on Databricks is not yet supported. ===```
3. system: not an option. We want to run experiments on Databricks.

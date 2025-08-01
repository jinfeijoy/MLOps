# MLOps Tools: MLflow and Hugging Face


### MLflow
1. start with dependencies
```
conda create --name exploratory python=3.8
conda activate exploratory
conda env export --name exploratory > conda_env.yml
conda env update --file conda_env.yml --prune # The command will look into any new (or different) dependencies and install them. The `--prune` flag will remove anything that is no longer defined in the _conda_env.yml_ file. In this case, you didn't remove anything, but it is still a good idea to keep using it.

```
3. 

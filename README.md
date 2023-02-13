# MLOps-practice-1 

*****************************************************
****************************************************** 
                                                                        First Session
******************************************************
******************************************************

## Project: Wafer

### Docs at: [Wafer mlops docs](https://c17hawke.github.io/wafer_mlops_docs/)

### Main project repository [mlops main](https://github.com/FraidoonOmarzai/wafer)

## Tools used in this projects:
* DVC
* MlFlow
* cookiecutter


## Useful links
* [mlops-continuous-delivery-and-automation-pipelines-in-machine-learning](https://cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning)

* [mlflow](https://mlflow.org/)


## Steps ([Link](https://c17hawke.github.io/wafer_mlops_docs/)):



### STEP 1 
* Create a new conda environment
```bash
    conda create -n <your_env_name> python=3.7 -y
```
* Activate the environment 
```bash
    conda activate <your_env_name>
```



### STEP 2 

* Create a default structure ()
```bash
    pip install cookiecutter
```
* Start a new project
```bash
    cookiecutter https://github.com/drivendata/cookiecutter-data-science
```



### Step 3
* Download the [dataset](https://github.com/iNeuron-Pvt-Ltd/wafer-dataset/archive/main.zip)



### Step 4
* Initialize git in Current working directory in your terminal, command prompt or git bash.

```bash 
    git init
```


### Step 5
* Install DVC and its gdrive extension

```bash 
    pip install dvc
    pip install dvc[gdrive]
```


### Step 6

* Initialize DVC

```bash 
    dvc init
```


### Step 7

* Add data into dvc for tracking

```bash 
    dvc add Training_Batch_Files/*.csv Prediction_Batch_files/*.csv
```

### Step 8

* Do the first commit and push to the remote repository
run below commands on by one

```bash 
    git add . && git commit -m "first commit and added raw data"
    git branch -M main
    git remote add origin https://github.com/<USERNAME>/<REPONAME>.git
    git push -u origin main
```

### Step 9

* Create and checkout a development branch for our development

```bash
    git checkout -b dev
```


### Step 10

* Add remote storage

```bash
    dvc remote add -d storage gdrive://<DRIVE ID>

    git add .dvc/config && git commit -m "Configure remote storage"
```

### Step 11
* Push the data to the remote storage

```bash
    dvc push
```


### Step 12

* Add Gdrive credential secrets in github repo secrets
* Find this credentials in the given path -
```bash
.dvc >> temp >> gdrive-user-credentials.json
```
* Now to add the secrets in your github repo -

    * Go to settings
    * secrets
    * Click on add secrets
    * Give name of secretes
    * Paste the json file content from **gdrive-user-credentials.json**

* To retrieve data anytime
```bash
    dvc pull
```


### Step 13

* Install full requirements.txt as given in the repository
``` bash
    pip install -r requirements.txt
```
* push to dev branch-
```bash
git add . && git commit -m "updated" && git push origin dev
```


### Step 14

* create a python file
```bash
touch src/pipeline_01_data_preparation.py
```

* Adding code to pipeline_01_data_preparation.py
```bash
import os
import argparse
import yaml
import logging

    
if __name__=="__main__":
    args = argparse.ArgumentParser()
    args.add_argument("--config", default="default")
    args.add_argument("--datasource", default=None)

    parsed_args = args.parse_args()
    print(parsed_args.config , parsed_args.datasource)
```

* run pipeline_01_data_preparation.py
```bash
python src/pipeline_01_data_preparation.py
python src/pipeline_01_data_preparation.py --config="demo"
```

* make dir config and inside it create params.yaml file
```bash
mkdir config
touch config/params.yaml
```

* add code to params.yaml


* create config/schema_training.json and data to it
```bash
touch config/schema_training.json
```

* create config/schema_prediction.json and data to it
```bash
touch config/schema_prediction.json
```

* push to dev branch-
```bash
git add . && git commit -m "config added" && git push origin dev
```

* After creating config and files inside it we alter our code inside pipeline_01_data_preparation.py
```bash
import os
import argparse
import yaml
import logging


def read_params(config_path):
    with open(config_path) as yaml_file:
        config = yaml.safe_load(yaml_file)
    return config

def main(config_path, datasource):
    config = read_params(config_path)
    print(config)
    
if __name__=="__main__":
    args = argparse.ArgumentParser()
    default_config_path = os.path.join("config", "params.yaml")
    args.add_argument("--config", default=default_config_path)
    args.add_argument("--datasource", default=None)

    parsed_args = args.parse_args()
```

* push changes to dev branch-
```bash
git add . && git commit -m "read config" && git push origin dev
```

*****************************************************
****************************************************** 
                                                                        First Session Completed
******************************************************
******************************************************
























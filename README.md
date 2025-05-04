# MLE COURSE 

Here we can learn how to do ML Engeneering Stuff.
Based on https://github.com/alexeygrigorev/ml-engineering-contsructor-workshop 

## how to install UV 
run: curl -LsSf https://astral.sh/uv/install.sh | sh

## Day 1

- create folder named 'day_1'
- in console run 'cd day_1'
- run 'uv init --python 3.10' and 'uv sync'

### install dependencies
- run 'uv add scikit-learn==1.2.2 pandas pyarrow'
- run 'uv add --dev jupyter seaborn'
- run 'uv add numpy==1.26.4' to fix issue with sklearn

### convert nb to script
- run 'uv run jupyter nbconvert --to=script notebooks/duration-prediction.ipynb'

### make script nicer
see the git commits
- remove top level statements
- make function parameterized
- introduce argparse 
    - make it run via 'uv run python duration_prediction/train.py --train-date 2022-01 --val-date 2022-02 --model-save-path models/2022-01.bin'
- create docstring (use chatgpt and/or autodicstring extension)
- add logging


### makefile
- create makefile -> run training via 'make train'

### add test
- run 'uv add pytest'
- create a tests folder
    - create file 'test_train.py'
- in folders 'duration_prediction' and 'tests' create empty files named '__init__.py'
- run 'uv run pytest'

### make it a module
- move code to main.py file
- run it via 'uv run python -m duration_prediction.main' instead of 'uv run python duration_prediction/main.py'



## Day 2

### create project

- run 'uv init --lib --python 3.10 duration_pred_serve'
- add dependencies from day 1: 'uv add scikit-learn==1.2.2 numpy==1.26.4'
- add flask: 'uv add flask'
- add pytest 'uv add pytest'
- add requests: 'uv add --dev requests'
- copy over model from day 1
- add loguru


### ping example
- can be run via 'uv run python src/duration_pred_serve/ping.py'
- open in browser: 'http://127.0.0.1:9696/ping'
    also: 'curl 127.0.0.1:9696/ping'

### implement serve 
- run it via 'uv run python src/duration_pred_serve/serve.py'
- or via requests: 'uv run python duration-tests/predict-test.py'

- run via makefile:
    - make run
    - make predict-test 

### use environment variables 
- have a look into export
- on the python side use os.getenv


### add loggong with loguru 
- added via 'uv add loguru'
- use via 'from loguru import logger' 


### use docker 
add commands to the makefile: 
    - 'make docker_build'
    - 'make docker_run'

### gunicorn -> for production
- uv add gunicorn
- run via 'uv run gunicorn --bind=0.0.0.0:9696 src.duration_pred_serve.serve:app' but we just update the entrypoint


### fly.io for deployment 
- account 
- install flyctl: 'curö -L https://fly.io/install.sh | sh'
- run 
'''
export FLYCTL_INSTALL="/home/codespace/.fly"
export PATH="$FLYCTL_STALL/bin:$PATH"
'''
- also copy these to ~/.bashrc 
- run 'flyctl launch'
- put new flyio url into predict-test.py and run 'make predict_test'











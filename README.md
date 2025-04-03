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
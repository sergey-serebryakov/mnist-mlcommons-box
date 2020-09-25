# MNIST MLCommons-Box without docker build

This now works only with new functionality available in multiple PRs.

```
source ./env/bin/activate
export PYTHONPATH=$(pwd)/mlcommons_box:$(pwd)/runners/mlcommons_box_singularity:$(pwd)/runners/mlcommons_box_docker:$(pwd)/runners/mlcommons_box_ssh
```

```
# Clone MNIST MLCommons-Box
git clone https://github.com/sergey-serebryakov/mnist-mlcommons-box.git
cd ./mnist-mlcommons-box

# Configure MLBox
python -m mlcommons_box_docker configure --mlbox=. --platform=./platforms/docker.yaml

# Run 'download' task.
python -m mlcommons_box_docker run --mlbox=. --platform=./platforms/docker.yaml --task=./run/download.yaml

# Run 'train' task.
python -m mlcommons_box_docker run --mlbox=. --platform=./platforms/docker.yaml --task=./run/train.yaml
```


### Possible improvements:

1. The `--platform` can be made optional in case an MLBox provides just one platform file.
   ```
   python -m mlcommons_box_docker configure --mlbox=.
   ``` 
2. The `--mlbox` can be made optional. Current path is used instead:
   ```
   python -m mlcommons_box_docker configure
   ```
3. MLCommons-Box runners can treat task as a string if it does not end with `.yaml`. In this case it is a file in the
   `run` directory:  
   ```
   python -m mlcommons_box_docker run --task=download
   python -m mlcommons_box_docker run --task=train
   ```
4. Default task can be `run`, and `configure` can be part of every `run` run:
   ```
   python -m mlcommons_box_docker --task=download
   python -m mlcommons_box_docker --task=train
   ```
5. In certain combinations of command line arguments, we can omit `--task` parameter:
   ```
   python -m mlcommons_box_docker download
   python -m mlcommons_box_docker train
   ```
6. MLCommons-Box should be able to use runner compatible with a platform configuration file:
   ```
   python -m mlcommons_box download
   python -m mlcommons_box train
   ```

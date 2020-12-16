# Jupyter Lab Docker image

A ready-to-run Docker image containing Jupyter Lab and data analysis computing tools.

## Python dependencies

To maintain reproducability, it's important to keep track of all the Python requirements 
needed to run the processing. To do so, all active dependencies and their versions are
listed in [requirements.txt]. These requirements are also installed whenever the image
is built.

To update the requirements list (after a new install):

```bash
pip freeze > requirements.txt
```

To reinstall all dependencies (should never really be needed):

```sh
pip install --requirement requirements.txt
```


## Docker image

To do all the processing in a reproducible way, Docker is used to have a completely
portable, cross-platform system that encapsulates all dependencies. The docker container
is centered around JupyterLab and Python3.

### Building the Docker image

Run this from the repository root directory, this will then build the docker image and
install all the dependencies from requirements.txt

```sh
docker build -t cleverfranke/jupyterlab-geo .
```

### Running the Docker container

Run this from the repository root directory

```sh
docker run -v "$pwd\:/notebooks" -p 10000:10000 --env-file docker.env cleverfranke/jupyterlab-base:latest
```

You can now find the link to the Jupyter Notebooks in the output of the container (with the 
required token)

### Environment variables file

The command above assumes that there's a docker.env file next to the Dockerfile. The
use of this file is to pass environment variables to the container. Because it can 
contain confidential information (access tokens and such) this file should *NOT* be 
included in the repo (hence why it's in the gitigore). 

To use it, create a plaintext 'docker.env' file according to the format below and
add the sensitive information as needed. If the file changes, it requires you to rerun 
the container to make those changes effective.

```
SOME_ENV_VAR=THE_VALUE_OF_SOME_ENV_VAR
```

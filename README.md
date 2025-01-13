# MlFlow Docker

## Description

This repository contains a dockerfile to build a docker image with mlflow server installed, also we provide a docker-compose file to run the mlflow server with a postgres and minio server.

We've posted a blog post about this repository, you can check it out [here](https://ruhyadi.github.io/blog/mlflow-docker/).

## Getting Started

### Start MlFlow Server

Please make sure you have [Docker](https://docs.docker.com/engine/install/) installed on your machine.

You can start the mlflow server by running the following command:

```bash
docker compose up
```

You can access the mlflow server by opening your browser and go to `http://localhost:5000`.

### Create an Experiment

We provide a script to create an experiment in the mlflow server, you can run the following command:

```bash
# build experiment docker image
docker build -t dockerfile.python -f dockerfile.python .

docker run \
    --rm -v $(pwd):/app -w /app \
    --network mlflow-network \
    --env AWS_ACCESS_KEY_ID=mlflow \
    --env AWS_SECRET_ACCESS_KEY=mlflow123 \
    --env MLFLOW_S3_ENDPOINT_URL=http://minio:9000 \
    dockerfile.python python mlflow_experiment.py
```

You can access the experiment by opening your browser and go to `http://localhost:5000`.
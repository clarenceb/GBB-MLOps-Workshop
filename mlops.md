# MLOps Guide - operationalising our machine learning process

## Introduction

Part 2 of this workshop will focus on operationalising our ML model via CI/CD pipelines so that we have an end-to-end, automated, repeatable process.  Much of this process is described in the [MLOps with Azure ML](https://github.com/microsoft/MLOpsPython) GitHub repository.  We'll use this approach as a basis for our workshop.

## (Optional) Test our Docker Image ML model locally

If you have [Docker Desktop](https://www.docker.com/products/docker-desktop) installed locally (or if you have access to an Azure VM with [Docker Engine](https://azure.microsoft.com/en-au/resources/templates/docker-simple-on-ubuntu/) installed) then you can directly test the digbreeds ML model via the package Docker image artefact created in Part 1.

### Retrieve your Docker credentials from ACR

From the Azure Portal, access the `DogBreeds` Resource Group you created created in Part 1.

Select the Container Registry resource which containers your Docker Image ML models.

![ContainerRegistry](screenshots/part2-container-registry.PNG)

Select **Settings** / **Access keys**  to retrieve the Docker credentials needed to login to your Azure Container Registry from the commandline.

![DockerCredentials](screenshots/part2-docker-credentials.PNG)

### Pull the Docker image locally

Login to your Azure Container Registry:

```sh
docker login <login-server> -u <username> -p <password>
```

Verify the container image repository name and version from the **Services** / **Repositories** menu:

![ImageRepo](screenshots/part2-image-repo.PNG)

Pull the model image from the container registry:

```sh
docker pull <login-server>/dobgreeds:1
```

Output:
```
1: Pulling from dogbreedsvc
9ff7e2e5f967: Already exists
59856638ac9f: Already exists
...snip...
42ac7d80edd4: Pull complete
Digest: sha256:7e5fbdbc3a3511530e3e767bf2a363f6887705496540813d2b0ffdb37accd274
Status: Downloaded newer image for dogbreedsXXXXXXXXXX.azurecr.io/dogbreedsvc:1
```

### Run the container locally

```sh
docker run -d --name dogbreedsvc -p 5001:5001 dogbreedsXXXXXXXXXX.azurecr.io/dogbreedsvc:1
```

Verify the container has started:

```sh
docker container ls
```

Output:

```
CONTAINER ID        IMAGE                                        COMMAND                 CREATED             STATUS              PORTS                              NAMES
b08964681242        dogbreedsXXXXXXXXXX.azurecr.io/dogbreedsvc:1   "runsvdir /var/runit"   40 seconds ago      Up 38 seconds       0.0.0.0:5001->5001/tcp, 8883/tcp   dogbreedsvc
```

The dogbreed ML service should be `Healthy`:

```sh
curl localhost:5001                                                                             # ==> Healthy
```

Now test the model by posting a dog image to the endpoint (assumes a `Bash` shell):

```sh
cd <GBB-MLOps-Workshop-dir>
(echo -n '{"data": "'; base64 breeds-10/val/n02091032-Italian_greyhound/n02091032_2687.jpg; echo '"}') | curl -sX POST -H "Content-Type: application/json" -d @-  http://localhost:5001/score

# ==> "{\"label\": \"Italian_greyhound\", \"probability\": \"0.5147553\"}"
```

### Stop and remove running Docker container

```sh
docker rm -f dogbreedsvc
```

## Creating our AKS cluster

## Deploying to AKS

## Create Azure DevOps orgnization and project

## Setup Azure Repos

## Setup Azure Pipelines

TODO

## References

* [MLOps using Azure ML Services and Azure DevOps](https://github.com/microsoft/MLOpsPython)
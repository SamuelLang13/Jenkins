# Installation
## Build Docker image

```
docker build . -t myjenkins
```
    "docker" is the command to interact with the Docker engine.
    "build" is the command to build a Docker image.
    "." specifies that the build context is the current directory.
    "-t myjenkins" tags the resulting image with the name "myjenkins".

## Create the network 'jenkins'
```
docker network create jenkins
```



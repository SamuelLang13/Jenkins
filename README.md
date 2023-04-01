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

## Run the container
```
docker run --name myjenkins --restart=on-failure --detach   --network jenkins --env DOCKER_HOST=tcp://docker:2376   --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1   --publish 8080:8080 --publish 50000:50000   --volume jenkins-data:/var/jenkins_home   --volume jenkins-docker-certs:/certs/client:ro  myjenkins
```
    "docker run" is the command to start a Docker container.
    "--name myjenkins" assigns a name "myjenkins" to the container.
    "--restart=on-failure" configures the container to automatically restart on failure.
    "--detach" runs the container in detached mode, meaning it runs in the background and doesn't block the terminal.
    "--network jenkins" attaches the container to a Docker network named "jenkins".
    "--env DOCKER_HOST=tcp://docker:2376" sets the Docker daemon host to "tcp://docker:2376".
    "--env DOCKER_CERT_PATH=/certs/client" specifies the path to the directory containing the Docker client TLS certificates within the container.
    "--env DOCKER_TLS_VERIFY=1" enables TLS verification for the Docker client within the container.
    "--publish 8080:8080" maps port 8080 on the container to port 8080 on the host machine.
    "--publish 50000:50000" maps port 50000 on the container to port 50000 on the host machine. This port is used for Jenkins agents to communicate with the master.
    "--volume jenkins-data:/var/jenkins_home" creates a Docker volume named "jenkins-data" and mounts it to the "/var/jenkins_home" directory in the container. This volume will persist the Jenkins data across container restarts.
    "--volume jenkins-docker-certs:/certs/client:ro" creates a Docker volume named "jenkins-docker-certs" and mounts it to the "/certs/client" directory in the container as read-only. This volume contains the Docker client TLS certificates.
    "myjenkins" specifies the name of the image to run.


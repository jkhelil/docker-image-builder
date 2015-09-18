# Context

*IN ORDER TO* be able to reproduce the build of Docker images

*AS A* Docker developpers,

*I WANT* to be able to relaunch build of all my images and push them inner registry

# Short description of the solution

We choose to use `bashbrew` which is a little script used by DockerInc to build there "official" images.
This script will read some configuration files which you could found inner `library` directory.
Thos files contains the name of the image to build (define by he name of the configuration file), the tag of image, on which git repository/branch we vould found the projet; and th path to the Dockerfile

You could have severals images/tag in same configuration files.

To get more inforamtion about [BashBrew](https://github.com/docker-library/official-images/tree/master/bashbrew), you could go on https://github.com/docker-library/official-images/tree/master/bashbrew/ .

# Who build
Now, we build our images from the following Jenkins : http://10.98.81.200

# Getting started with docker

## Docker project

### Dockerfile

Docker images are build from the *Dockerfile* manifest. 

*Dockerfile*

```
# FROM: Base image
FROM centos:6

# MAINTAINER: one or many maintainers (Optional)
MAINTAINER John Doe john.doe@example.com

CMD echo "Hello world"
```

See [Dockerfile documentation](https://docs.docker.com/reference/builder/#dockerfile-reference) to learn about Dockerfile syntax.

### Available hooks
Three hooks are provided to manage custom requirements. 
Those are scripts executed if present in the same directory than Dockerfile.

- docker-prebuild : executed before `docker build`
- docker-build : executed **instead of** `docker build`
- docker-postbuild : executed after `docker build`

Each hook receives the image name as first argument ( ex : *vsct/jenkins:latest* ). Check [sample directory](sample) for details

Continue by reading [Docker best pratices](Docker-BestPractices.md)

## Reference the Dockerfile to be build

For a docker project to be build by bashbrew, it must be referenced within the docker-images repository, in the *library* directory
As docker images have namespace, those are represented by a directory with the same name. New namespaces can be added by creating a new directory.

Ex : dockerregistry.socrate.vsct.fr:5000/vsct/jenkins

```
docker-images
|- library
   |- vsct
      |- jenkins
```

Each project refers to one single file. For more information, see the [sample definition](library/sample/template).
# docker-image-builder

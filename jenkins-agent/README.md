# Python agent Docker images for Jenkins
Openshift Jenkins does not have Python enabled images tagged for being used as nodes out of the box. This directory shows how such images can be built.

This repository contains Dockerfiles for a Jenkins Agent Docker image intended for use with OpenShift v3.

To build an image: `docker build -t jenkins-agent-python-rhel7 -f Dockerfile.rhel7 .`

## Docker Registry
The image can be pushed to a registry from where it can be accesses.

Tag: `docker tag jenkins-agent-python-rhel7 docker.io/dav1dli/jenkins-agent-python-rhel7`

Push: `docker push docker.io/dav1dli/jenkins-agent-python-rhel7`

## Jenkins
Jenkins can use a published image as a Kubernetes pod template.

Required parameters:
* Name: python
* Labels: python
* Containers template Name: jnlp
* Docker image: docker.io/dav1dli/jenkins-agent-python-rhel7
* Always pull: yes
* Working directory: /tmp
* Arguments: ${computer.jnlpmac} ${computer.name}

In Jenkins pipelines use
```
agent {
  node {
    label 'python'
  }
}
```
so Jenkins auto-provisions python slave node created from the specified container image.

## Minishift
Providing that Minishift is up and running to push an image to internal Minishift registry execute:
```
eval $(minishift docker-env)
oc login -u developer
docker login -u `oc whoami` -p `oc whoami -t` 172.30.1.1:5000
docker tag jenkins-agent-python-rhel7 172.30.1.1:5000/myproject/jenkins-agent-python-rhel7
docker push 172.30.1.1:5000/myproject/jenkins-agent-python-rhel7
```

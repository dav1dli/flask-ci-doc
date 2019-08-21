# Python agent Docker images for Jenkins
Openshift Jenkins does not have Python enabled images tagged for being used as nodes out of the box. This directory shows how such images can be built.
This repository contains Dockerfiles for a Jenkins Agent Docker image intended for use with OpenShift v3.

To build an image: `docker build -t jenkins-agent-python-rhel7 -f Dockerfile.rhel7 .`

## Minishift
Providing that Minishift is up and running to push an image to internal Minishift registry execute:
```
eval $(minishift docker-env)
oc login -u developer
docker login -u `oc whoami` -p `oc whoami -t` 172.30.1.1:5000
docker tag jenkins-agent-python-rhel7 172.30.1.1:5000/myproject/jenkins-agent-python-rhel7
docker push 172.30.1.1:5000/myproject/jenkins-agent-python-rhel7
```

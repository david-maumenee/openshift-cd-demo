# Local OpenShift Origin

Download and install [Container Development Kit (CDK)](https://developers.redhat.com/products/cdk/download/)

Clone this repo and Start up an OpenShift cluster:

## profile

```
minishift profile set ocp310-cicd
minishift config set vm-driver virtualbox
minishift config set cpus 2
minishift config set memory 11GB
minishift config set disk-size 30GB
minishift config set ocp-tag v3.10.127
minishift addon enable anyuid
minishift config set image-caching true

```
## start

```
minishift start --skip-registration --skip-registry-check


```

## Pre-pull the images and fix access to volume


```
minishift ssh

sudo chmod 777 -R /var/lib/minishift/

docker pull openshiftdemos/gogs:0.11.34
docker pull openshiftdemos/sonarqube:7.0
docker pull sonatype/nexus3:3.12.1
docker pull registry.access.redhat.com/openshift3/jenkins-2-rhel7:v3.10
docker pull registry.access.redhat.com/openshift3/jenkins-2-rhel7:v3.10.127
docker pull registry.access.redhat.com/openshift3/jenkins-slave-maven-rhel7:v3.10.127
docker pull registry.access.redhat.com/openshift3/jenkins-agent-maven-35-rhel7:v3.10.127
docker pull registry.access.redhat.com/jboss-eap-7/eap70-openshift:1.5



exit

```

## fix jboss-eap70-openshift image stream issue

```
oc login -u system:admin

oc delete is jboss-eap70-openshift -n openshift

oc create -f jboss-eap70-openshift-rhel7.json -n openshift

oc describe is/jboss-eap70-openshift -n openshift
```
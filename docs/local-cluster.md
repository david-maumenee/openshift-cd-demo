# Local OpenShift Container Platform

Download and install [Container Development Kit (CDK)](https://developers.redhat.com/products/cdk/download/)

Start up an OpenShift cluster:

```
minishift addons enable xpaas
minishift start --memory=10240 --vm-driver=virtualbox
oc login -u developer
```

Pre-pull the images to make sure the deployments go faster:

```
minishift ssh 

docker pull openshiftdemos/gogs:0.11.34
docker pull openshiftdemos/sonarqube:7.0
docker pull sonatype/nexus3:3.7.1
docker pull registry.access.redhat.com/openshift3/jenkins-2-rhel7
docker pull registry.access.redhat.com/openshift3/jenkins-slave-maven-rhel7
docker pull registry.access.redhat.com/jboss-eap-7/eap70-openshift
docker pull openshift/origin:v3.7.0

exit
```
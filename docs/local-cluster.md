# Local OpenShift Origin

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

```
oc login -u system:admin

oc delete is jboss-eap70-openshift -n openshift

oc create -f jboss-eap70-openshift-rhel7.json -n openshift

oc describe is/jboss-eap70-openshift -n openshift
```
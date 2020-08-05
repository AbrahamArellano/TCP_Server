# REST_OpenShift_Fuse
Camel REST application deployed on OpenShift using Fuse

## Prerequisites
Please read and follow the instructions on README_OCP_Preparation.md

## Create project (only as a reference - do not use this step)
mvn org.apache.maven.plugins:maven-archetype-plugin:2.4:generate \
  -DarchetypeCatalog=https://maven.repository.redhat.com/ga/io/fabric8/archetypes/archetypes-catalog/2.2.0.fuse-sb2-760038-redhat-00001/archetypes-catalog-2.2.0.fuse-sb2-760038-redhat-00001-archetype-catalog.xml \
  -DarchetypeGroupId=org.jboss.fuse.fis.archetypes \
  -DarchetypeArtifactId=spring-boot-camel-rest-sql-archetype \
  -DarchetypeVersion=2.2.0.fuse-sb2-760038-redhat-00001
  
## Deploy OpenShift
oc project redhat-router-longlasting

cd /home/aarellan/git/TCP_Server

mvn fabric8:deploy -Popenshift

## Undeploy OpenShift
mvn fabric8:undeploy -Popenshift

## Check logs
On each pod the logs display the HAProxy port which represents the connection used from the HAProxy to application POD

## Check connection on Router Node
watch -n 0.2 "netstat -atlnp | grep -E '172.17.0.10|172.17.0.9'"

-n: refresh time in seconds


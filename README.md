# spark-on-kubernetes

Simple repository to deploy Spark on Kubernetes along with Zeppelin for learning.

## Docker
Involves two docker images:-
1. [vivekkumar2696/zeppelin](https://hub.docker.com/repository/docker/vivekkumar2696/zeppelin) - Docker Image for Apache Zeppelin 0.8.2
    
    It is an upgrade for gcr.io/google-containers/zeppelin:v0.5.6_v1 image updated spark version as well (2.3.2).

2. [vivekkumar2696/spark](https://hub.docker.com/repository/docker/vivekkumar2696/spark) - Apache Spark Docker Image 2.3.2.

    It is an updated version of the gcr.io/google_containers/spark:1.5.2_v1 image. 

## Kubernetes
Deploying Spark master and worker nodes followed by Zeppelin 

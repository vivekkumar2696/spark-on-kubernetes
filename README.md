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


```
$ kubectl create -f kubernetes/spark/namespace-spark-cluster.yaml
$ kubectl create -f kubernetes/spark/spark-master-controller.yaml
$ kubectl create -f kubernetes/spark/spark-master-service.yaml
$ kubectl create -f kubernetes/spark/spark-ui-proxy-controller.yaml
$ kubectl create -f kubernetes/spark/spark-ui-proxy-service.yaml
$ kubectl create -f kubernetes/spark/spark-worker-controller.yaml
$ kubectl create -f kubernetes/spark/zeppelin-controller.yaml
$ kubectl create -f kubernetes/spark/zeppelin-service.yaml
```
```
$ kubectl exec zeppelin-controller-abc123 -it pyspark
Python 2.7.9 (default, Mar  1 2015, 12:57:24)
[GCC 4.9.2] on linux2
Type "help", "copyright", "credits" or "license" for more information.
Welcome to
      ____              __
     / __/__  ___ _____/ /__
    _\ \/ _ \/ _ `/ __/  '_/
   /__ / .__/\_,_/_/ /_/\_\   version 1.5.1
      /_/

Using Python version 2.7.9 (default, Mar  1 2015 12:57:24)
SparkContext available as sc, HiveContext available as sqlContext.
>>> from math import sqrt; from itertools import count, islice
>>>
>>> def isprime(n):
...     return n > 1 and all(n%i for i in islice(count(2), int(sqrt(n)-1)))
...
>>> nums = sc.parallelize(xrange(10000000))

>>> print nums.filter(isprime).count()
664579
```



For Spark UI:

`kubectl proxy --port=8001`

Then visit http://localhost:8001/api/v1/proxy/namespaces/spark-cluster/services/spark-ui-proxy/.

For Zeppelin:

`kubectl port-forward zeppelin-controller-abc123 8080:8080 &`

Then visit http://localhost:8080/.


If you liked it and it was helpful, then
<a href="https://www.buymeacoffee.com/vivekkumar2696" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy Me A Coffee" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>

# Fess Helm Chart
This chart uses a Docker image of Fess provided by [codelibs](https://codelibs.org/).


## TL;DR;

```
$ helm repo add elastic https://helm.elastic.co
$ helm dependency update
$ helm install fess .
```






```
$ kc get all
NAME                               READY   STATUS    RESTARTS   AGE
pod/elasticsearch-master-0         1/1     Running   0          2m
pod/elasticsearch-master-1         1/1     Running   0          2m
pod/elasticsearch-master-2         1/1     Running   0          2m
pod/fess-858fdd7c88-nhtm2          1/1     Running   0          2m
pod/fess-kibana-7759798779-6ktzj   1/1     Running   0          2m


NAME                                    TYPE           CLUSTER-IP     EXTERNAL-IP       PORT(S)             AGE    
service/elasticsearch-master            ClusterIP      10.0.12.252    <none>            9200/TCP,9300/TCP   2m    
service/elasticsearch-master-headless   ClusterIP      None           <none>            9200/TCP,9300/TCP   2m
service/fess                            LoadBalancer   10.0.146.68    xxx.xxx.xxx.xxx   80:32235/TCP        2m    
service/fess-kibana                     ClusterIP      10.0.209.146   <none>            5601/TCP            2m    


NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/fess          1/1     1            1           2m
deployment.apps/fess-kibana   1/1     1            1           2m

NAME                                     DESIRED   CURRENT   READY   AGE
replicaset.apps/fess-858fdd7c88          1         1         1       2m
replicaset.apps/fess-kibana-7759798779   1         1         1       2m

NAME                                    READY   AGE
statefulset.apps/elasticsearch-master   3/3     2m
```
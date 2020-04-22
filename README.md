# Fess Helm Chart
This helm chart uses a [Docker image of Fess](https://hub.docker.com/r/codelibs/fess/) provided by [codelibs](https://github.com/codelibs).

![dashboard](https://user-images.githubusercontent.com/34591767/79941762-feef8d00-849f-11ea-9562-9e5f560bb414.png)


## TL;DR;

```
$ helm repo add elastic https://helm.elastic.co
$ helm dependency update
$ helm install fess .
```


## Getting Started

### Installing the Chart
Clone the git repo:
```
$ git clone git@github.com:eternity1984/helm-fess.git
```

Add the `elastic` helm charts repo:
```
$ helm repo add elastic https://helm.elastic.co
```

Fetch related charts:
```
$ helm dependency update
```

To install the chart with the release name `fess`:
```
$ helm install fess .
```

### Installed Components
You can use `kubectl get` to view all of the installed components.

```
$ kubectl get all
NAME                               READY   STATUS    RESTARTS   AGE
pod/elasticsearch-master-0         1/1     Running   0          2m
pod/elasticsearch-master-1         1/1     Running   0          2m
pod/elasticsearch-master-2         1/1     Running   0          2m
pod/fess-858fdd7c88-nhtm2          1/1     Running   0          2m
pod/fess-kibana-7759798779-6ktzj   1/1     Running   0          2m


NAME                                    TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)             AGE    
service/elasticsearch-master            ClusterIP   10.0.12.252    <none>        9200/TCP,9300/TCP   2m    
service/elasticsearch-master-headless   ClusterIP   None           <none>        9200/TCP,9300/TCP   2m
service/fess                            ClusterIP   10.0.146.68    <none>        80:32235/TCP        2m    
service/fess-kibana                     ClusterIP   10.0.209.146   <none>        5601/TCP            2m    


NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/fess          1/1     1            1           2m
deployment.apps/fess-kibana   1/1     1            1           2m

NAME                                     DESIRED   CURRENT   READY   AGE
replicaset.apps/fess-858fdd7c88          1         1         1       2m
replicaset.apps/fess-kibana-7759798779   1         1         1       2m

NAME                                    READY   AGE
statefulset.apps/elasticsearch-master   3/3     2m
```

### Uninstalling the Chart
To uninstall/delete the `fess` release:
```
$ helm uninstall fess
```

## Configuration

| Parameter                 | Description                                                                                                       | Default                                                             |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `elasticsearchHosts`      | The URLs used to connect to Elasticsearch.                                                                        | `http://elasticsearch-master:9200`                                  |
| `replicaCount`            | Kubernetes replica count for the deployment (i.e. how many pods).                                                 | `1`                                                                 |
| `image.repository`        | The Fess docker image.                                                                                            | `codelibs/fess`                                                     |
| `service.type`            | Type of fess service.                                                                                             | `ClusterIP`                                                         |
| `service.port`            | The http port that Kubernetes will use for the service.                                                           | `80`                                                                |
| `kibana`                  | [kibana](https://github.com/elastic/helm-charts/blob/7.6.2/kibana/README.md#configuration) entries.               |                                                            |
| `elasticsearch`           | [elasticsearch](https://github.com/elastic/helm-charts/blob/7.6.2/elasticsearch/README.md#configuration) entries. |                                                                     |
| `elasticsearch.image`     | The Elasticsearch docker image.  (provided by codelibs)                                                           | `codelibs/fess-elasticsearch`                                       |
| `elasticsearch.extraEnvs` | Extra environment variables which will be appended to the `env:` definition for the container.                    | `FESS_DICTIONARY_PATH = /usr/share/elasticsearch/config/dictionary` |
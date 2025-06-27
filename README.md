---
# mars helm chart
-  install mars on k8s cluster.

## Configuration

| Parameter | Description | Default |
|:-----------|:-------------|:---------|
| `global.repoPrefix` | Prefix string for image repository | ""<br></br>ex: "k8s.gcr.io" |
| `pvc.mars.size` | PVC size used by mars container | "4Gi" |
| `pvc.es.size` | PVC size used by elasticsearch container | "4Gi" |
| `resource.mars.requests.cpu` | CPU resource used by mars container | "2000m" |
| `resource.mars.requests.memory` | MEM resource used by mars container | "8Gi" |
| `resource.lgs.requests.cpu` | CPU resource used by logstash container | "1000m" |
| `resource.lgs.requests.memory` | MEM resource used by logstash container | "2Gi" |
| `resource.es.requests.cpu` | CPU resource used by elasticsearch container | "1000m" |
| `resource.es.requests.memory` | MEM resource used by elasticsearch container | "2Gi" |
| `resource.web.requests.cpu` | CPU resource used by nginx container | "512m" |
| `resource.web.requests.memory` | MEM resource used by nginx container | "1Gi" |
| `license.file` | License file for mars | |
| `license.overwrite` | Overwrite the old license file found in PVC. | false |

## Usage:
[Helm](https://helm.sh) must be installed to use the charts.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

1. Creating a copy of the default values.yaml.
```
helm show values {repo/chart} > values.yaml
```
2. Modify your custom configuration parameters.
```
vi values.yaml
```
3. Apply new values.yaml for installation.
```
helm install -f values.yaml {release} -n {namespace} {repo/chart}
```
4. Or apply deafult values for installation.
```
helm install {release} -n {namespace} {repo/chart}
```
5. Apply license file for installation.
```
helm install {release} -n {namespace} --set-file license.file=./{lic} {repo/chart}
```
6. Apply license file and overwrite the old one for installation.
```
helm install {release} -n {namespace} \
  --set-file license.file=./{lic} --set license.overwrite {repo/chart}
```
7. Install a cluster with 3 mars controller.
```
Prerequisite: need to use calico's ip pool.

a. kubectl apply -f env-values/ippool.yaml
b. kubectl apply -f env-values/ipreserv.yaml
c. helm install {release} -n {namespace} \
    -f env-values/values-mars-cluster.yaml {repo/chart}
```
8. Install a mars controller ver sia.
```
helm install {release} -n {namespace} \
  -f env-values/values-sia.yaml {repo/chart}
```
9. Install a mars controller with an elasticsearch cluster.
```
helm install {release} -n {namespace} \
  -f env-values/values-es-cluster.yaml {repo/chart}
```


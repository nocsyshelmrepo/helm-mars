
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
| `license.file` | License file for mars | |
| `license.overwrite` | Overwrite the old license file found in PVC. | false |

## Usage:
[Helm](https://helm.sh) must be installed to use the charts.  
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

1. Creating a copy of the default values.yaml.
```
helm show values {repo/chart} > test.yaml
```
2. Modify your custom configuration parameters.
```
vi test.yaml
```
3. Apply new values.yaml for installation.
```
helm install -f test.yaml {release} -n {namespace} {repo/chart}
```
4. Or apply deafult values for installation.
```
helm install {release} -n {namespace} {repo/chart}
```
5. Apply license file for installation.
```
helm install {release} -n {namespace} --set-file license.file=./{lic} {repo/chart}
```

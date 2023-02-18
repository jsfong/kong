### Create namespace
kubectl create namespace kong

### Install kong
helm repo add kong https://charts.konghq.com
helm repo update
helm install kong -n kong kong/kong -f values.yaml

### Install db for konga
helm install konga-db -n kong bitnami/postgresql -f values.yam

### Install konga
helm install konga ./ -n kong -f values.yaml

### Connect to konga
use http://<kong admin cluster ip>:8001

### Other
//Password change
Remember to delete PVC after helm uninstall

//Turning on DB cause KIC not working
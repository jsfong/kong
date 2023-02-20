### Create namespace
kubectl create namespace kong

### Install kong
helm repo add kong https://charts.konghq.com
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm install kong -n kong kong/kong -f values.yaml

### Install db for konga
helm install konga-db -n kong bitnami/postgresql -f values.yam

### Install konga
helm install konga ./ -n kong -f values.yaml

### Connect to konga
use http://<kong admin cluster ip>:8001

## Deploy servce
### Deploy sample service
kubectl apply -f 01_deployment.yaml
kubectl apply -f 02_service.yaml
kubectl apply -f 03_ingress.yaml

### Update default lb to consistent hashing
kubectl apply -f 04_kong_ingress.yaml
kubectl patch service models-service --patch-file 05_patch_service.yaml

### Other
//Password change
Remember to delete PVC after helm uninstall

//Turning on DB cause KIC not working
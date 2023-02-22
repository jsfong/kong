### Create namespace
kubectl create namespace kong

### Install kong
helm repo add kong https://charts.konghq.com
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm install kong -n kong kong/kong -f with_db_value.yaml

### Install db for konga
cd /konga/db
helm install konga-db -n kong bitnami/postgresql -f values.yaml

### Install konga
cd /konga
helm install konga ./ -n kong -f values.yaml

### Connect to konga
use http://<kong admin cluster ip>:8001

## Deploy servce
### Deploy sample service
cd /sample_services/models-service
kubectl apply -f 00_full_uri.yaml

### Other
//Password change
Remember to delete PVC after helm uninstall

//Turning on DB cause KIC not working
//Create namespace
kubectl create namespace kong

//Install kong
helm repo add kong https://charts.konghq.com
helm repo update
helm install kong -n kong kong/kong -f values.yaml

//Portforward DB
//Create user konga and DB konga

//Install konga
cd konga-helm-chart
helm install konga ./ -n kong -f values.yaml


//Connect to konga
use http://<cluster ip>:8001

//Other
//Password change
Remember to delete PVC after helm uninstall


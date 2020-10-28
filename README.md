wget https://get.helm.sh/helm-v3.3.1-linux-amd64.tar.gz
tar -zxvf helm-v3.3.1-linux-amd64.tar.gz
sudo mv linux-amd64/helm /usr/local/bin/helm
helm version 


cd k8s-postgresql/charts
helm install postgres-operator postgres-operator -f postgres-operator/values.yaml
helm ls 

cd k8s-postgresql/

k create -f manifests/minimal-postgres-manifest.yaml

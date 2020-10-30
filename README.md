#Installing Helm 

wget https://get.helm.sh/helm-v3.3.1-linux-amd64.tar.gz
tar -zxvf helm-v3.3.1-linux-amd64.tar.gz
sudo mv linux-amd64/helm /usr/local/bin/helm
helm version 


#Deploying Postgresql cluster on K8s

cd k8s-postgresql/charts
helm install postgres-operator postgres-operator -f postgres-operator/values.yaml
helm ls 


# check the deployed cluster
kubectl get postgresql

# check created database pods
kubectl get pods -l application=spilo -L spilo-role

# check created service resources
kubectl get svc -l application=spilo -L spilo-role

#Retreive Password From Secret 

export PGPASSWORD=$(kubectl get secret postgres.acid-minimal-cluster.credentials.postgresql.acid.zalan.do -o 'jsonpath={.data.password}' | base64 -d)
echo $PGPASSWORD

#checking postgres connection 

Run client k8s pod to connect with master postgres 
k run pclient --image=centos/postgresql-12-centos7  -- sleep 36000
k exec -it pclient -- /bin/bash

connect to master node 
psql -U postgres -h acid-minimal-cluster -p 5432 

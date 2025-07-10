eksctl create cluster \
--name mycluster \
--region us-east-1 \
--nodegroup-name mynodes \
--node-type t3.micro \
--nodes 2 \
--nodes-min 2 \
--nodes-max 2 \
--managed


>> wsl 

touch script.sh
nano script.sh 

chmod +x script.sh 
./script.sh

exec 
touch/ New-Item 

cd Downloads
git clone https://github.com/atulkamble/eks-nginx-app.git
cd eks-nginx-app

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

kubectl get deployments
kubecl get nodes
kubecl get pods
kubectl get services

// paste url in browser 

ab48aada9bf2b42ae847d730d8fbf546-556919796.us-east-1.elb.amazonaws.com

// on minikube 
minikube tunnel

eksctl delete cluster --name mycluster

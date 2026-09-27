# Kubernetes

## [[minikube]]

可以使用 minikube 来创建一个单节点集群，用于本地学习

## kubectl

```shell
# get node
kubectl get nodes
# get service
kubectl get svc
# get pod
kubectl get pod
# get pod with other specific information
kubectl get pod nginx -o wide
# describe pod
kubectl describe pod nginx
# get namespace
kubectl get namespace
# or
kubectl get ns
# get all
kubectl get all

# start a container
kubectl run nginx --image=nginx
# create a deployment
kubectl create deployment nginx-deployment --image=nginx

# log analytics
kubectl logs nginx

# execute command
kubectl exec -it nginx -- /bin/bash

# delete resource
kubectl delete deployment nginx-deployment
```

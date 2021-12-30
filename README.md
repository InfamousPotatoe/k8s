# k8s
Kubernetes dev/test environment for learning.

# Installation
Requires homebrew

## Docker
Install Docker desktop: https://docs.docker.com/desktop/mac/install/
This is preferred over using homebrew

## Minikube
brew install minikube
minikube config set driver docker

## Start cluster
minikube start

### Route to the cluster - when needed
minikube tunnel

# Cluster Resources

## SealedSecrets


## ArgoCD
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
minikube tunnel
#Get password: kubectl get secret example-argocd-cluster -n argocd -o jsonpath='{.data.admin\.password}' | base64 -d

## Istio
brew install istioctl
istioctl install


kubectl config set-context $(kubectl config current-context) --namespace=argocd

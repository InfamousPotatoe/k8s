# k8s
Kubernetes dev/test environment for learning.

# Installation
Requires homebrew

## Helm
    brew install helm

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

## OLM
    curl -sL https://github.com/operator-framework/operator-lifecycle-manager/releases/download/v0.19.1/install.sh | bash -s v0.19.1

## SealedSecrets
    brew install kubeseal
    kubectl apply -f install/sealed-secrets-controller.yaml


## ArgoCD
    kubectl create namespace argocd
    kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
    kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
    minikube tunnel
#Get password: kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath='{.data.password}' | base64 -d

### Add repo
Add repo to ArgoCD and export the repo secret as yaml
Use kubeseal to create a SealedSecret and deploy via 
    kubectl apply -f install/argo-repo-sealed-secret.yaml

## Istio
    brew install istioctl
    istioctl install


kubectl config set-context $(kubectl config current-context) --namespace=argocd

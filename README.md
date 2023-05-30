## ArgoCD Demo

## Deploy a Ghost Blogging Application with ArgoCD

### Deployment

```
kubectl apply -k ghost/
```

### Deployment with ArgoCD
```
kubectl create namespace argocd

kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

kubectl port-forward svc/argocd-server -n argocd 8080:443

argocd admin initial-password -n argocd

argocd login localhost:8080

argocd app create ghost --repo https://github.com/cloudhonk/argocd-demo.git --path ghost --dest-server https://kubernetes.default.svc --dest-namespace default

argocd app get ghost

```

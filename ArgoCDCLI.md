
Using ArgoCD CLI
```
argocd app list
argocd app get helm-gitops-example
argocd app history helm-gitops-example
```

delete the app
```
argocd app delete helm-gitops-example
```
deploy
```
argocd app create demo \
--project default \
--repo https://github.com/codefresh-contrib/gitops-certification-examples \
--path "./helm-app/" \
--sync-policy auto \
--dest-namespace default \
--dest-server https://kubernetes.default.svc
```

```
kubectl get all
```

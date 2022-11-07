# Deploy Simple App on Argo CD using CLI

Deploy app with below parameter:

```
argocd app create demo2 \
--project default \
--repo https://github.com/codefresh-contrib/gitops-certification-examples \
--path "./simple-app" \
--dest-namespace default \
--dest-server https://kubernetes.default.svc
```

Now sync it with:

```
argocd app sync demo2
```

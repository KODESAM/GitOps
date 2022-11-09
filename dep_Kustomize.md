# Deploying with Kustomize

You can generate a customized YAML file:
```
kustomize build name_of_application
```
This file/resources can then be applied to a cluster:
```
kustomize build name_of_application | kubectl apply -k or --kustomize
```
Create a namespace in the cluster:
```
kubectl create ns kustomize
```
Reference the Git repository with the Kustomize file to create an Argo CD app:
```
argocd app create name_of_application --repo repo_url --revision kustomize --path path_for_your_kustomize_files --dest-server server-url --dest-namespace kustomize
```
Sync deployment managed by Argo CD:
```
argocd app sync application_name
```
Check status of deployment:
```
argocd app get application_name
```
Each time a new kustomize.yaml file is created or the file changes, Argo CD can detect those and make updates to the deployment.

### Install Argo CD

```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Download Argo CD CLI

```
brew install argocd
```
### Access The Argo CD API Server

Service Type Load Balancer

Change the argocd-server service type to LoadBalancer:

```
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

Port Forwarding

Kubectl port-forwarding can also be used to connect to the API server without exposing the service.
```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
Login Using The CLI

```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
argo CLI login
```
argocd login <ARGOCD_SERVER>
```
Change the password using the command:
```
argocd account update-password
```

### Register A Cluster To Deploy Apps To

This step registers a cluster's credentials to Argo CD, and is only necessary when deploying to an external cluster. When deploying internally (to the same cluster that Argo CD is running in), https://kubernetes.default.svc should be used as the application's K8s API server address.

First list all clusters contexts in your current kubeconfig:

```
kubectl config get-contexts -o name
```
Choose a context name from the list and supply it to argocd cluster add CONTEXTNAME. For example, for docker-desktop context, run:

```
argocd cluster add docker-desktop
```

Creating Apps Via CLI

First we need to set the current namespace to argocd running the following command:

```
kubectl config set-context --current --namespace=argocd
```
Create the example guestbook application with the following command:
```
argocd app create guestbook --repo https://github.com/argoproj/argocd-example-apps.git --path guestbook --dest-server https://kubernetes.default.svc --dest-namespace default
```

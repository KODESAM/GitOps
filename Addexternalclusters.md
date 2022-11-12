# Add external clusters

We have created two more Kubernetes clusters for you that are completely independent from the one that has Argo CD. 
All clusters are running on different Virtual Machines (VMs).

kubernetes-vm is a cluster that has ArgoCD installed
kubernetes-vm2 is a second cluster on another VM.
kubernetes-vm3 is a third cluster on another VM.

To add the clusters as external deployment targets you need to run the following command on the terminal for "Cluster 2" and Cluster 3

kubernetes-vm2
```
argocd login kubernetes-vm:30443 --insecure --username admin --password <admin-password>
```
kubernetes-vm3
```
argocd login kubernetes-vm:30443 --insecure --username admin --password <admin-password>
```
This command authenticates the Argo CD cli that is running on cluster2 against the main cluster (that has ArgoCD). Run this command on both Cluster 2 and Cluster 3
```
argocd cluster add default --name cluster-2
```
```
argocd cluster add default --name cluster-3
```

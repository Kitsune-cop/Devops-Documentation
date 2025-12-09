# Setup Control plane server

### Install Kubernetes
install in every server

```
sudo snap install microk8s --classic
```
On machine you assign as main for control plane
* check microk8s status
```
sudo microk8s status
```
add other node
```
sudo microk8s add-node
```
It's will show output like this
```
#From the node you wish to join to this cluster, run the following:
microk8s join <your-server-ip>:25000/255adbce9874ffab93e93be3475eb8fc/f44d4636903b 
##Copy this line and paste && run in every control plane server

#Use the --worker' flag to join a node as a worker not running the control plane, eg:
microk8s join <your-server-ip>:25000/255adbce9874ffab83e93be3475eb8fc/f44d4636903b --worker
##Copy this line and paste && run in every worker server

#If the node you are adding is not reachable through the default interface you can use one of the following:
microk8s join <your-server-ip>:25000/255adbce9874ffab93e93be3475eb8fc/f44d4636903b
```
Check node
```
sudo microk8s kubectl get node
```

Get Config
```
sudo microk8s config
# copy config
```
On your device
* `C:\Users\<user>\.kube` (recommend)
* create file `<server-name>.yml`
* paste config in `<server-name>.yml`

> windows (CMD)
```
set KUBECONFIG=C:\Users\<user>\.kube\<server-name>.yml
```
> windows (Powershell)
```
$Env:KUBECONFIG = "C:\Users\YourUser\.kube\config"
```
> Linux and MacOs
```
export KUBECONFIG="/path/to/your/kubeconfig.yaml"
```
#### Enable feature
```
sudo microk8s enable metrics-server

sudo microk8s enable dashboard

sudo microk8s enable storage

sudo microk8s enable metallb
```
#### Get kubernetes token
```
kubectl describe secret -n kube-system microk8s-dashboard-token
```
#### Launch Dashboard
```
kubectl port-forward -n kube-system service/kubernetes-dashboard 10443:443
```
##### Access via:
`https://localhost:10443`

#### Set Loadbalancer
```
sudo microk8s enable metallb:<ip-address>- <ip-address>
```
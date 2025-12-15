# Set up Jenkins Server

### Install kubectl

```
sudo snap install kubectl --classic
```

### Install microk8s

```
sudo snap install microk8s --classic
```
### Check microk8s status

```
sudo microk8s status
```

### Get microk8s config
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

sudo microk8s enable dns

sudo microk8s enable storage
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

#### Deploy Jenkins
> in jenkins folder
```
    kubectl apply -f <file-name>.yml
```

#### Set Loadbalancer
```
sudo microk8s enable metallb:<ip-address>- <ip-address>
```

##### Plugins
* Pipeline: Stage View
* Kubernetes
* SonarQube Scanner
* Build Monitor View

##### Create Cloud

> Go to setting -> Clouds -> New cloud (name same as in jenkins config file)

##### Create Pod template
> Clouds -> setting -> Pod template -> add pod template (name same as in jenkins config file)
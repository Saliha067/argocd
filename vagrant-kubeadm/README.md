## For MAC Users

Latest version of Virtualbox for Mac/Linux can cause issues because you have to create/edit the /etc/vbox/networks.conf file and add:
<pre>* 172.42.42.0/24</pre>

or run below commands
```sh
sudo mkdir -p /etc/vbox/
echo * 172.42.42.0/24 | sudo tee -a /etc/vbox/networks.conf
```

So that the host only networks can be in any range, not just 192.168.56.0/21 as described here:
https://discuss.hashicorp.com/t/vagrant-2-2-18-osx-11-6-cannot-create-private-network/30984/23
 
## Usage/Examples

To provision the cluster, execute the following commands.

```shell
git clone https://github.com/scriptcamp/vagrant-kubeadm-kubernetes.git
cd vagrant-kubeadm-kubernetes
vagrant up
```

## Set Kubeconfig file varaible.

```shell
cd vagrant-kubeadm-kubernetes
cd configs
export KUBECONFIG=$(pwd)/config
```

or you can copy the config file to .kube directory.

```shell
cp config ~/.kube/
```

## Kubernetes Dashboard URL

```shell
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/overview?namespace=kubernetes-dashboard
```

## Kubernetes login token

Vagrant up will create the admin user token and saves in the configs directory.

```shell
cd vagrant-kubeadm-kubernetes
cd configs
cat token
```

## To shutdown the cluster, 

```shell
vagrant halt
```

## To restart the cluster,

```shell
vagrant up
```

## To destroy the cluster, 

```shell
vagrant destroy -f
```


kubectl patch deployments.apps -n argocd argocd-repo-server --type='json' -p '[{ "op": "replace", "path": "/spec/template/spec/containers/0/image", "value": "kubeshop/argocd-testkube:v1" }]'

kubectl patch deployments.apps -n argocd argocd-repo-server --type='json' -p '[{ "op": "replace", "path": "/spec/template/spec/initContainers/0/image", "value": "kubeshop/argocd-testkube:v1" }]'


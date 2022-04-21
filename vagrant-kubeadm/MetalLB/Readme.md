
## https://metallb.universe.tf/#requirements

sipcalc 172.17.0.1/16

## https://metallb.universe.tf/installation/

curl -s https://raw.githubusercontent.com/metallb/metallb/v0.11.0/manifests/namespace.yaml | less

kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.11.0/manifests/namespace.yaml

curl -s https://raw.githubusercontent.com/metallb/metallb/v0.11.0/manifests/metallb.yaml | less

kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.11.0/manifests/metallb.yaml

kubectl create -f metallb_cm.yml

kubectl get cm -n metallb-system

kubectl create deploy nginx --image=nginx --port=80 --dry-run=client -o yaml > deploy_nginx.yml

kubectl expose deploy nginx --port=80 --type=LoadBalancer --dry-run=client -o yaml > svc_nginx.yml

kubectl -n metallb-system get all

sipcalc 172.42.42.1/24
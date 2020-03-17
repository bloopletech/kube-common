## Monitoring

### metrics-server

````
cd ~
git clone git@github.com:kubernetes-incubator/metrics-server.git
cd metrics-server/deploy/kubernetes
````

Per https://github.com/digitalocean/digitalocean-cloud-controller-manager/issues/150#issuecomment-450499337

Edit metrics-server-deployment.yaml to insert after:

````
imagePullPolicy: IfNotPresent
args: 
````

Add:

````
- --kubelet-preferred-address-types=InternalIP
````

Then:

````
kubectl apply -f .
````

### kube-state-metrics

Per: https://www.digitalocean.com/docs/kubernetes/how-to/monitor-advanced/

````
cd ~
git clone git@github.com:kubernetes/kube-state-metrics.git
kubectl create -f kube-state-metrics/examples/standard/
````

### kubernetes-dashboard


DigitalOcean now provides kubernetes-dashboard built-in, accessible from the Control Panel.
So manual install is not needed.

## ingress-nginx

````
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/f1f90ef4954effb122412d9cd2d48e02063038a4/deploy/static/mandatory.yaml
kubectl apply -f nginx-ingress-cloud-generic.yaml
````

## cert-manager

````
kubectl create namespace cert-manager
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.14.0/cert-manager.yaml
````

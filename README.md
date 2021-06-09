## Prerequisites

1. Install doctl: https://github.com/digitalocean/doctl#downloading-a-release-from-github
2. Login to your account with `doctl auth init`.
3. Install kubectl: https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-using-native-package-management.
4. Configure kubectl to access your cluster with `doctl kubernetes cluster kubeconfig save <cluster name>`.
5. Configure docker to be able to access your DigitalOcean container registry with `doctl registry login`.

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

Per: https://kubernetes.github.io/ingress-nginx/deploy/#digital-ocean

````
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.34.1/deploy/static/provider/do/deploy.yaml
````

## cert-manager

Per: https://cert-manager.io/docs/installation/kubernetes/#installing-with-regular-manifests

````
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.3.1/cert-manager.yaml
````

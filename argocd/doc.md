# ArgoCD 

Argo CD is a declarative continuous delivery tool for Kubernetes. It can be used as a standalone tool or as a part of your CI/CD workflow to deliver needed resources to your clusters.

<img src="../img/argocd.png">

## deploy argocd in a cluster
https://argo-cd.readthedocs.io/en/stable/getting_started/

apply a yaml file
```bash
apply -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/core-install.yaml
```

list pods and wait for all pods to start
```bash
kubectl get pod -w
```

list all services
```bash
kubectl get svc
```

### define ingress rule

[yaml file](argocd_ingress.yaml)

```bash
kubectl apply -f argocd_ingress.yaml
```

problem: when visiting argocd.127.0.0.1.nip.io i get 'too many redirects'

https://github.com/argoproj/argo-cd/issues/2953 <br>
"The problem is that by default Argo-CD handles TLS termination itself and always redirects HTTP requests to HTTPS. Combine that with an ingress controller that also handles TLS termination and always communicates with the backend service with HTTP and you get Argo-CD's server always responding with a redirects to HTTPS."

#### solution

would be to terminate ssl on ingress controller as described [here](https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/#option-2-multiple-ingress-objects-and-hosts) but it didnt work so far
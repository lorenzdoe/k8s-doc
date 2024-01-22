# Cluster with ingress controller and http-echo

## Create multi node cluster with custom config

create a cluster using [config.yaml](config.yaml). This configuration sets up a multi node cluster whth one control-plane and to worker nodes. It also defines port mappings

```bash
kind create cluster --config config.yaml
```

`ingress-ready=true` indicates that this node is ready for ingress traffic. This could be used by an ingress controller

## ingress NGINX controller

Deploy the Kubernetes supported ingress NGINX controller to work as load balancer and reverse proxy

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```

## deploy a service

using the simple http-echo web server as docker image

[service.yaml](service.yaml)

```bash
kubectl apply -f service.yaml
```

### Pod
The pod is the smallest instance, running the http-echo docker image

### Service 
A Service in Kubernetes is an abstraction that defines a logical set of Pods and a policy for accessing them. Services allow to expose a set of Pods as a network service with a stable IP address and DNS name. This abstraction enables other parts of the application to access the service without needing to know the specific IP addresses of the individual Pods.

### Ingress
An Ingress is an API object that provides HTTP and HTTPS routing to services based on rules defined in the configuration. It acts as an entry point for external traffic into cluster, allowing to define how requests should be directed to different services. Ingress controllers, which are typically implemented by third-party providers or cloud platforms, manage the actual routing and load balancing based on the rules specified in the Ingress resource.

## Test

list running services
```bash
kubectl get services
```

see if it worked
```bash
curl localhost/app
```

## Explore the cluster

```bash
kubectl get <nodes/pods/services/etc.>
```

To determine specific nodes where the pod is scheduled 
```bash
kubectl get pods -o wide
```


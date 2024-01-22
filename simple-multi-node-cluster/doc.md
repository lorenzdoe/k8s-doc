# Multi Node Cluster with ingress controller and simple webserver

https://www.baeldung.com/ops/kubernetes-kind

## Create multi node cluster with custom config

### Custom config.yml
create a cluster using [config.yaml](config.yaml). This configuration sets up a multi node cluster whth one control-plane and to worker nodes. It also defines port mappings

This [config.yaml](config.yaml) will create a cluster with a control-plane node that has the following properties:
- a node label of ingress-ready=true
- a static mapping of container port 80 to host port 9080
- a static mapping of container port 443 to host port 9443

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

The `spec: selector:` field is used to determine which Pods will be targeted by this Service. In this case, the Service will target all Pods that have a label of `app` with the value `my-app`. This is how the Service knows which Pods to send network traffic to.

The `ports:` field under `spec:` defines the ports that this Service will listen on. In this case, it's listening on port 5678. Any network traffic that hits this Service on port 5678 will be forwarded to the Pods selected by the `app: my-app` selector, on their respective ports.

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
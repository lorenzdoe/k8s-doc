# Kubernetes in Docker (KIND)

## Installation
Prerequisites:
- Docker or Podman

[Documentation](https://kind.sigs.k8s.io/docs/user/quick-start/)

## Commands

create cluster
```bash
kind create cluster
```

delete cluster
```bash
kind delete cluster --name <cluster-name>
```

pass a custom config
```bash
kind create cluster --config custom-config.yml
```

list clusters
```bash
kind get clusters
```

list nodes
```bash
kind get nodes
```

## Kubectl

Any kubectl command interacts with a kubernetes cluster. The cluster that kubectl interacts with is determined by the kubeconfig file, located in '$HOME\cube\config'. The kubeconfig file contains the address of the cluster and the credentials to access it.

View current active context
```bash
kubectl config current-context
```

Switch between contexts
```bash
kubectl config use-context <context-name>
```

Apply a configuration to a cluster
```bash
kubectl apply -f <config-file>
```

## Custom config.yml
multi-node cluster:
https://kind.sigs.k8s.io/docs/user/quick-start/#multi-node-clusters

Single node cluster with custom config:
Configuration for Ingress Controller
```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
name: dev
nodes:
- role: control-plane
  kubeadmConfigPatches:
  - |
    kind: InitConfiguration
    nodeRegistration:
      kubeletExtraArgs:
        node-labels: "ingress-ready=true"
  extraPortMappings:
  - containerPort: 80
    hostPort: 9080 
    protocol: TCP
  - containerPort: 443
    hostPort: 9443
    protocol: TCP
```

This will create a cluster with a control-plane node that has the following properties:
- a node label of ingress-ready=true
- a static mapping of container port 80 to host port 9080
- a static mapping of container port 443 to host port 9443

## Kubernetes Components
- <b>[Overview](https://kubernetes.io/docs/concepts/overview/components/)</b><br>
- <b>[Glossary](https://kubernetes.io/docs/reference/glossary/?all=true)</b><br>

A kubernetes cluster consists of a set of worker machines, called nodes, that run containerized applications. Every cluster has at least one worker node.

<img src='img/components-of-kubernetes.svg' style="background-color:white;border-radius:5%; max-width:70%;">

### control-plane node
The control-plane node is a Kubernetes node with a control-plane role A control-plane role means that the node runs the Kubernetes control plane components. The control plane components include:
- kube-apiserver
- kube-controller-manager
- kube-scheduler
- etcd
- kube-proxy
- CoreDNS


### worker node
The worker node is a Kubernetes node with a worker role. A worker role means that the node can run application workloads.

## kubernetes kind hands on
https://www.baeldung.com/ops/kubernetes-kind


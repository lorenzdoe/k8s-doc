# Kubernetes in Docker (KIND)

## Installation
Prerequisites:
- Docker or Podman

[Documentation](https://kind.sigs.k8s.io/docs/user/quick-start/)

## Commands
some basic commands to get started with kind

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

## Hands on - Create a cluster
Create a simple multi node cluster with ingress controller and web server
[Hands on](simple-multi-node-cluster/doc.md)

## Hands On - ArgoCD
Argo CD is a declarative continuous delivery tool for Kubernetes. It can be used as a standalone tool or as a part of your CI/CD workflow to deliver needed resources to your clusters.
[Hands on](argocd/doc.md)
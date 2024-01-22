# Ingress Controller, Webserver, Pod volumeMounts, ConfigMap

Create a simple multi-node cluster and create ingress controller like in this [setup](../simple-multi-node-cluster/doc.md)

## Deploy a service

```bash
kubeclt apply -f service.yaml
```
deploys a pod running an nginx container, a service and a ingress resource
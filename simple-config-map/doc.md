# Ingress Controller, Webserver, Pod volumeMounts, ConfigMap

Create a simple multi-node cluster and create ingress controller like in this [setup](../simple-multi-node-cluster/doc.md)

## Config Map

Many applications rely on configuration which is used during either application initialization or runtime. Most times, there is a requirement to adjust values assigned to configuration parameters. ConfigMaps are a Kubernetes mechanism that let you inject configuration data into application pods.

```bash
kubectl apply -f configmap.yaml
```

## Deploy a service

```bash
kubeclt apply -f service.yaml
```
Deploys a pod running an nginx container, a service and a ingress resource that is configured using nip.io

my-webserver.127.0.0.1.nip.io will resolve to the IP address 127.0.0.1. Any traffic that is sent to this host will be handled by the Ingress rule in the configuration. The traffic will be forwarded to the service named my-service on port 80.

## Test

Visit https://my-webserver.127.0.0.1.nip.io in your browser. This should show the nginx landing page

This should show the own index.html from the config map
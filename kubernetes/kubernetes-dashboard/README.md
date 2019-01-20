# kubernetes-dashboard

This chart is created by fetching and customzing `stable/kubernetes-dashboard`.

## Main Changes

1. Enable Ingress
2. Enable Cluster Admin

## Steps

```console
$ kubectl create namespace dashboard
$ kubectl create secret tls kubernetes-dashboard-tls --key ~/Downloads/k8s_imulab_io.key --cert ~/Downloads/k8s_imulab_io.crt --namespace dashboard
$ helm install stable/kubernetes-dashboard --namespace dashboard --name kubernetes-dashboard
```

## Login

```console
$ kubectl get secrets -n dashboard
$ kubectl describe secret kubernetes-dashboard-token-xxxx -n dashboard
```
# Docker Registry Helm Chart

This chart is customized based on the upstream `stable/docker-registry` chart.

## Updates

- Add `REGISTRY_STORAGE_DELETE_ENABLED=true` environment variable
- Requested for 20G of `gluster-heketi-retain` storage
- Enabled ingress

## Installing the Chart

To install the chart, use the following:

```console
$ kubectl create ns registry
$ kubectl create secret tls registry-tls --key registry_imulab_io.key --cert registry_imulab_io.crt --namespace registry
$ helm install stable/docker-registry --name registry --namespace registry
```

## Problems

It seems using minio as the s3 backend will still cause a redirect issue which prevents pushing from completing.
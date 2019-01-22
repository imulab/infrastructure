Minio
=====

This chart is modified by fetching upstream `stable/minio` chart.

Main Modifications
------------

- Everything installed in `minio` namespace.
- Enabled dynamic provisioning by asking for a claim from `gluster-heketi-retain` storage class.
- Enabled ingress to `s3.imulab.io`

Prerequisites
-------------

- SSL certificates for `s3.imulab.io`
- DNS entry of `s3.imulab.io` set of the ip of ingress controller

Installing the Chart
--------------------

Install this chart using:

```bash
$ kubectl create namespace minio
$ kubectl create secret tls minio-tls --key s3_imulab_io.key --cert s3_imulab_io.crt --namespace minio
$ helm install ./minio --name minio --namespace minio --set accessKey=myKey --set secretKey=mySecret
```

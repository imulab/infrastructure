# metrics-server

- Manifest taken from [official repo](https://github.com/kubernetes-incubator/metrics-server/tree/master/deploy)
- Updated with deployment commands below to resolve [this issue](https://github.com/kubernetes-incubator/metrics-server/issues/167)

```
command:
- /metrics-server
- --v=2
- --kubelet-insecure-tls
- --kubelet-preferred-address-types=InternalIP
```

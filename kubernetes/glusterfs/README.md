# GlusterFS

This directory contains the files necessary to recreate dynamic provisioning capabilities backed by a GlusterFS cluster.

## Topology

The configuration files `topology-sample.json` here reflects a GlusterFS topology of three nodes:
1. 300GB /dev/sdb on `k8s-worker-1` with ip `192.168.100.28`
2. 300GB /dev/sdb on `k8s-worker-2` with ip `192.168.100.29`
3. 300GB /dev/sdb on `k8s-worker-3` with ip `192.168.100.30`

## Preparation

On each nodes, do

```bash
sudo -s
ufw disable
apt-get install glusterfs-client
modprobe dm_thin_pool
```

## Install

From client

```bash
# create daemonset
kubectl create -f glusterfs-daemonset.json

# label nodes
kubectl label node k8s-worker-1 storagenode=glusterfs
kubectl label node k8s-worker-2 storagenode=glusterfs
kubectl label node k8s-worker-3 storagenode=glusterfs

# verify pods on running
kubectl get pods

# create service account
kubectl create -f heketi-service-account.json
kubectl create clusterrolebinding heketi-gluster-admin --clusterrole=edit --serviceaccount=default:heketi-service-account

# create secret configuration
kubectl create secret generic heketi-config-secret --from-file=./heketi.json

# create heketi and then port forward so we can configure topology on the client
kubectl create -f heketi-bootstrap.json
kubectl port-forward deploy-heketi-xxxx 8080:8080

# verify heketi is running
curl http://localhost:8080/hello

# configure topology
export HEKETI_CLI_SERVER=http://localhost:8080
heketi-cli topology load --json=topology-sample.json

# setup storage (will generate heketi-storage.json)
heketi-cli setup-openshift-heketi-storage
kubectl create -f heketi-storage.json

# create storage class
kubectl apply -f storage_class.yml

# test
kubectl apply -f test.yml
kubectl delete -f test.yml
```

## Resources

- [https://github.com/heketi/heketi/blob/master/docs/admin/install-kubernetes.md](https://github.com/heketi/heketi/blob/master/docs/admin/install-kubernetes.md)
- [https://github.com/gluster/gluster-kubernetes/blob/master/docs/examples/hello_world/README.md](https://github.com/gluster/gluster-kubernetes/blob/master/docs/examples/hello_world/README.md)
- [https://jimmysong.io/kubernetes-handbook/practice/using-heketi-gluster-for-persistent-storage.html](https://jimmysong.io/kubernetes-handbook/practice/using-heketi-gluster-for-persistent-storage.html)

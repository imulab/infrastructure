# Rook-Ceph

- Installation is performed with v0.9.3
- We had a 500G single disk and uses *hostDataDir* method

## Installation
```
kubectl create -f operator.yaml
kubectl create -f cluster.yaml
kubectl create -f toolbox.yaml
```

## Configure
```
kubectl -n rook-ceph exec -it $(kubectl -n rook-ceph get pod -l "app=rook-ceph-tools" -o jsonpath='{.items[0].metadata.name}') bash
ceph dashboard set-login-credentials <username> <password>

# make sure metallb has been installed
kubectl edit service ceph-mgr-dashboard	# change type to LoadBalancer
```

## Storage Class
```
kubectl create -f storageclass.yaml
```
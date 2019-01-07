# Image Gallery

List of all custom built images.

### ubuntu-bionic-gocd-master/agent.json

A basic ubuntu bionic64 cloud image, installed with gocd master or agent package, following the installation instructions [here](https://docs.gocd.org/current/installation/).

Output format is `qcow2`. To import on Proxmox, consult [Proxmox cloud init documentation](https://pve.proxmox.com/wiki/Cloud-Init_Support).

### ubuntu-bionic-docker.json

A basic ubuntu bionic64 cloud image, custom provisioned to install `docker`.

Output format is `qcow2`. To import on Proxmox, consult [Proxmox cloud init documentation](https://pve.proxmox.com/wiki/Cloud-Init_Support).

### ubuntu-bionic-k8s-basic

A basic ubuntu bionic64 cloud image, custom provisioned to install `docker`, `kubeadm`, `kubelet` and `kubectl`. Designed to quickly bootstrap a non-HA kubernetes cluster without having to wait for software installation.

Output format is `qcow2`. To import on Proxmox, consult [Proxmox cloud init documentation](https://pve.proxmox.com/wiki/Cloud-Init_Support).

### bionic64-cloud-init-seed.img

Cloud init seed created using `cloud-utils`. Packer need this file to init cloud image and SSH into it.

```
sudo apt-get install -y cloud-utils

cat >> EOF << /tmp/cloud.cfg
password: ubuntu
ssh_pwauth: true
chpasswd:
  expire: false
EOF

cloud-localds /tmp/seed.img /tmp/cloud.cfg
```

### proxmox using qcow2

```
# create template
qm create 1000 --memory 512 --net0 virtio,bridge=vmbr0
qm importdisk 1000 custom.img local-data
qm set 1000 \
	--scsihw virtio-scsi-pci \
	--scsi0 local-data:vm-1000-disk-1 \
	--ide2 local-data:cloudinit \
	--boot c --bootdisk scsi0 \
	--serial0 socket --vga serial0
qm template 1000

# clone template and set cloud init in UI.
```

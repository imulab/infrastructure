# Images

Packer builders for images used in server environment.

## Provision using Vagrant

```
vagrant up
vagrant ssh
cd /packer
packer build foo.json
```

The Vagrant image automatically installs `Packer` and `QEMU`. However, because free version of Vagrant uses Virtualbox as the default provider, KVM support is simply not there. QEMU builder used by Packer has to run without acceleration, which could take
quite some time. Nonetheless, using a virtual machine to create images is still the cleanest way to go.

## Provision on OS X

Make sure QEMU for OS X is download, then:

```
sudo mv QEMU/ /usr/local/lib
export PATH=$PATH:/usr/local/lib/QEMU/Programs
sudo packer build foo.json
```
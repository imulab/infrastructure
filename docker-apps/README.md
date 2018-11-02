# Docker Apps

A series of docker app running on FreeNas Docker VM.

## VM Setup

- Create docker VM
- Attach zvol to VM
- Set VM mac address to `00:a0:98:23:be:bb`, reserve `192.168.100.222` for it in router.
- (Optional) If zvol is new, assuming is `/dev/sdb`, do `fdisk /dev/sdb`
- (Optional) If zvol is new, assuming is `/dev/sdb`, do `mkfs.ext4 /dev/sdb1`
- (Optional) If not mounted, do `mount /dev/sdb1 /data`

## Software Setup

```
# Install docker-compose, rancher os does not ship with docker-compose
sudo wget -O /usr/bin/docker-compose "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)"
sudo chmod +x /usr/bin/docker-compose

# Install local-persist plugin
docker run -d --restart=unless-stopped --name local_persist_daemon -v /run/docker/plugins/:/run/docker/plugins/ -v /data/.config/:/var/lib/docker/plugin-data/ -v /data/volumes/:/data/volumes/ cwspear/docker-local-persist-volume-plugin

# Create app_net
docker network create --driver=bridge --subnet=172.21.0.0/16 --gateway=172.21.0.1 app_net
```
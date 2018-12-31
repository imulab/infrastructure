# drone

Drone CI deployment.

This installation has been enhanced by [Drone Web Hook Proxy](https://github.com/imulab-x/drone-webhook-proxy) so Drone can receive web hook events from outside the private network.

## Dependencies

- `drone.imulab.io.crt` and `drone.imulab.io.key` placed in `/etc/certs/` on master, with permission `444`
- `imulab.io.crt` placed in `/usr/local/share/ca-certificates/` on both master and workers, with permission `444`.
- `update-ca-certificates`

## Memo

- Fill in `DRONE_GITHUB_CLIENT_ID`, `DRONE_GITHUB_CLIENT_SECRET` and `DRONE_RPC_SECRET`
- Generate `DRONE_RPC_SECRET` by `openssl rand -hex 16`.
- Deploy a web hook proxy in the cloud.
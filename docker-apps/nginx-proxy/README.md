# nginx-proxy

A dynamic reverse proxy in front of all other apps.

## Dependency

- externally configured `app_net`.
- `/data/certs` containing all certificates.
- `/data/volumes/nginx-proxy/config/vhost` containing all vhost specific nginx configurations.
# registry

docker container management platform

## Dependencies

- externally configured network `app_net`.
- `/data/volumes/registry` containing managed data.
- certificates for `registry.imulab.io` put in `/data/certs`.

## V-Host setting

```
client_body_in_file_only clean;
client_body_buffer_size 32K;
client_max_body_size 5G;
sendfile on;
send_timeout 3600s;
```
# minio

standalone minio app serving as image and chart repository

## Dependencies

- externally configured network `app_net`.
- `/data/volumes/minio/data` containing managed data.
- `/data/volumes/minio/config` cotaining minio configurations.
- certificates for `minio.imulab.io` put in `/data/certs`.

## V-Host setting

```
# TODO This does not work very well, change this.
client_body_in_file_only clean;
client_body_buffer_size 32K;
client_max_body_size 5G;
sendfile on;
send_timeout 3600s;
```

## Client setup

```
mc config host add imulab https://minio.imulab.io $MINIO_ACCESS_KEY $MINIO_ACCESS_SECRET
mc config host add imulabp http://$ip_address:$port $MINIO_ACCESS_KEY $MINIO_ACCESS_SECRET
```
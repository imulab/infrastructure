# artifactory

artifactory oss with postgresql installation

## Dependencies

- externally configured network `app_net`.
- access to directory `/data/volumes/artifactory`
- certifactes for `artifactory.imulab.io` put in `/data/certs`

## Installation

```
cd /data/blueprint/artifactory

# prepare environment
git clone git@github.com:jfrog/artifactory-docker-examples.git
chmod +x ./docker-compose/artifactory/prepareHostEnv.sh
./docker-compose/artifactory/prepareHostEnv.sh -t oss -c /data/volumes/artifactory

# start
docker-compose up -d
```

## V-Host setting

```
client_body_in_file_only clean;
client_body_buffer_size 32K;
client_max_body_size 5G;
sendfile on;
send_timeout 3600s;
```

## Client side setting

We need to import the CA certification to Java

```
cd $JAVA_HOME/jre/bin
./keytool -import -trustcacerts -alias imulab -file /path/to/your/ca.crt -keystore ../lib/security/cacerts
# Java's default store password is 'changeit'
```
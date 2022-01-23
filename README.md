# Elasticsearch & Kibana docker configuration
Basic configuration for stand alone Elasticsearch cluster.


## Installation

Fill variables in conf_file:

```sh
TAG=7.13.1
ES_DATA=./es_data
CERTS=./certs
KIBANA_DATA=./kibana_data
SETUP_DIR=./setup
# Configure certs
CA_PASSWORD=
ELASTICSEARCH01_CERT_PASSWORD=
KIBANA_CERT_PASSWORD=
# ====================
# Configure services
ES_CLUSTER_NAME=
# password for user elastic (default)
ELASTIC_PASSWORD=
# setup kibana user
ELASTICSEARCH_USERNAME=
# setup saved objects enc key
XPACK_ENCRYPTEDSAVEDOBJECTS_ENCRYPTIONKEY= 
```
### Generate certs:
``` 
docker-compose --env-file conf_env -f docker-compose-setup.yml up
```
### Copy generated certs to certs dir:
```sh
   for ca -> certs/ca
   For elasticsearch instanse -> certs/es
   For kibana instance ->  certs/kibana
```
### Start Elasticsearch and Kibana:
```
docker-compose --env-file conf_env -f docker-compose.yml up
```
### Testing:

 Just visit https://{your_ip}:5601/ 
 
 log in by typing your **elastic**  and **ELASTIC_PASSWORD** (see **Instalation**)
 
 
### Create Client Cert
```
openssl x509 -req -days 365000 -set_serial 01    -in client-req.pem    -out client-cert.pem    -CA ./ca/ca.crt    -CAkey ./ca/ca.key
```
## Validate Client Cert
```
openssl verify -CAfile ./ca/ca.crt    ca-cert.pem    client-cert.pem
```

 
 




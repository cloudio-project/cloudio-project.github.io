# Cloudio properties

This file describes where the gateway has to connect and where are the certificates needed for the MQTTs connection establishement.

### Properties

|Name|Type|Description|Required|
|----|----|-----------|--------|
|**ch.hevs.cloudio.endpoint.hostUri**|`string`|Cloud.iO server hostname|yes|
|**ch.hevs.cloudio.endpoint.ssl.version**|`string`|TLS version<br/>|yes|
|**ch.hevs.cloudio.endpoint.ssl.authorityCert**|`string`|Relative path to the CA cert file|yes|
|**ch.hevs.cloudio.endpoint.ssl.clientCert**|`string`|Relative path to the client certificate|yes|
|**ch.hevs.cloudio.endpoint.ssl.clientKey**|`string`|Relative path to the client secret key|yes|
|**ch.hevs.cloudio.endpoint.ssl.verifyHostname**|`string`|Verify the host authority cert.<br/>(true or false, default to true)|no|
|**ch.hevs.cloudio.endpoint.messageFormat**|`string`|Message format of the MQTT payloads.<br/>(json or cbor, default to cbor)|no|
|**ch.hevs.cloudio.endpoint.persistence**|`string`|MQTT persistence type.<br/>(none, memory or file)|yes|


### Example
``` properties
ch.hevs.cloudio.endpoint.hostUri: my-cloudio-server.example.com 
ch.hevs.cloudio.endpoint.ssl.version: "tlsv1.2"  
ch.hevs.cloudio.endpoint.ssl.authorityCert: "../settings/certs/example-ca-cert.pem"  
ch.hevs.cloudio.endpoint.ssl.clientCert: "../settings/certs/example-client-cert.pem"  
ch.hevs.cloudio.endpoint.ssl.clientKey: "../settings/certs/example-client-key.pem"  
ch.hevs.cloudio.endpoint.ssl.verifyHostname: 'false'  
ch.hevs.cloudio.endpoint.messageFormat: "json"  # or "cbor"
  
# Either none, memory or file  
ch.hevs.cloudio.endpoint.persistence: memory
```


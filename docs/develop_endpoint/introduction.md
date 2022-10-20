# Introduction

The cloudio endpoints can be programmed in **Java** or **Python**. The Python version does not support all the features:

|Features|Java|Python|
|---|---|---|
|Update|:heavy_check_mark:|:heavy_check_mark:|
|Set|:heavy_check_mark:|:heavy_check_mark:|
|Transactions|:heavy_check_mark:|:heavy_check_mark:|
|Delayed|:heavy_check_mark:|:heavy_check_mark:|
|JSON serialization|:heavy_check_mark:|:heavy_check_mark:|
|CBOR serialization|:heavy_check_mark:|:heavy_check_mark:|
|Token provisioning|:heavy_check_mark:|:x:|
|Logs|:heavy_check_mark:|:x:|
|Jobs|:heavy_check_mark:|:x:|

## Endpoint library features

### Update
Endpoint can send data to the cloud.

### Set
Endpoint can receive data from the cloud.

### Transaction
Endpoint can send a collection of updates in a single *transaction* MQTT message.

### Delayed
When loosing the connection with the cloud, the endpoints stores the messages locally and sends them in a single *delayed* MQTT message when the connection is restored.

### JSON serialization
JSON serialized MQTT messages payload.

### CBOR serialization
CBOR (Concise Binary Object Representation) serialized MQTT messages payload.

### Token provisioning
Endpoint can download and configure its certificates and connection informations from a *host url* and a *provisioning token*.

### Logs
Endpoint logs are send to the cloud.

### Jobs
Endpoint can execute local shell scripts on cloud demand.


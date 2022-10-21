# Introduction

This section describes how to read and write the **endpoint's data**. It also describes how to create **cloud.iO applications** as their role is to read, process data and write setpoints.

The data can be accessed using, HTTP, Websocket or MQTT.

The HTTP interface provides access to the history data, the last measured values and the endpoints data model.

Every attribute change can be read on event. There are 2 options for this, **STOMP** over **Websocket** and **MQTT**. 
For a basic use case, it is recommended to use STOMP/Websocket instead of MQTT. By using MQTT, the message received can be either in a CBOR or a JSON message format. (unless all the endpoints use a unique message format).
When using STOMP/Websocket, all the messages are in a JSON format.

If you want to access cloud.iO data within a **python** script, the [cloudio-connector-python](https://pypi.org/project/cloudio-connector-python/) library can be used.
